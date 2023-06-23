# Incremental Static Generation

Cập nhật nội dung tĩnh sau khi bạn đã build website.

- [Code mẫu](#code-mẫu)
  - [Thêm các trang mới](#thêm-các-trang-mới)
  - [Cập nhật các trang hiện có](#cập-nhật-các-trang-hiện-có)
- [Những ưu điểm](#những-ưu-điểm)

---

Static Generation (SSG) giải quyết hầu hết các vấn đề của CSR và SSR nhưng sử dụng để render nội dung tĩnh là chủ yếu. Nó đặt ra những hạn chế khi nội dung được render là nội dung động hoặc thường xuyên thay đổi.

Hãy nghĩ về sự phát triển của một blog với nhiều bài viết. Bạn sẽ không muốn build và deloy lại trang web chỉ vì muốn sữa lỗi chính tả ở một trong các bài đăng. Tương tự, một bài viết mới cũng không nên yêu cầu build lại những trang hiện có. Do đó, chỉ riêng SSG là không đủ để render các website hay ứng dụng lớn.

Incremental Static Generation (iSSG) pattern được giới thiệu là một bản nâng cấp của SSG, giúp giải quyết vấn đề về dữ liệu động và giúp các trang web tĩnh mở rộng quy mô cho một lượng lớn dữ liệu thay đổi thường xuyên. iSSG cho phép bạn cập nhật các trang đã tồn tại và thêm trang mới bằng cách render trước một tập hợp con các trang chạy ngầm trong nền ngay cả khi có request mới cho các trang.

## Code mẫu

iSSG hoạt động trên hai phương diện để từng bước cập nhật cho một trang web tĩnh hiện có ngay sau khi nó được build.

1. Cho phép thêm các trang mới
2. Cho phép cập nhật các trang hiện có còn được gọi là Incremental Static "Re"generation

### Thêm các trang mới

Khái niệm lazy load được sử dụng để bao gồm các trang mới trên website sau khi build. Điều này có nghĩa là các trang mới được tạo ngay trong request đầu tiên. Trong khi quá trình tạo diễn ra, một trang dự phòng hoặc một thông báo loading có thể được hiển thị cho người dùng ở front-end. So sánh điều này với kịch bản SSG đã thảo luận trước đó cho từng trang chi tiết sản phẩm. Trang 404 được hiển thị ở đây dưới dạng trang dự phòng cho các trang không tồn tại.

Bây giờ chúng ta hãy xem xét code Next.js cần thiết để lazy load một trang không tồn tại với iSSG.

**pages/products/[id].js**

```js
// Trong getStaticPaths(), bạn cần trả về danh sách id
// của các trang sản phẩm (/products/[id]) mà bạn muốn
// render trước tại lúc build. Để làm vậy, bạn có thể
// fetch dữ liệu tất cả sản phẩm từ database.
export async function getStaticPaths() {
  const products = await getProductsFromDatabase();

  const paths = products.map((product) => ({
    params: { id: product.id },
  }));

  // fallback: true có nghĩa các trang bị thiếu sẽ không
  // chuyển qua trang 404 thay vào đó hiển trị trang dự phòng
  return { paths, fallback: true };
}

// params sẽ chứa id cho mỗi trang được tạo.
export async function getStaticProps({ params }) {
  return {
    props: {
      product: await getProductFromDatabase(params.id),
    },
  };
}

export default function Product({ product }) {
  const router = useRouter();

  if (router.isFallback) {
    return <div>Loading...</div>;
  }

  // Render sản phẩm
}
```

Ở đây chúng ta đã sử dụng `fallback: true`. Bây giờ nếu trang tương ứng với sản phẩm cụ thể không có sẵn, chúng ta hiển thị một phiên bản dự phòng của trang, ví dụ một thông báo loading được hiển thị như trong function `Product` ở trên. Trong khi đó, Next.js sẽ tạo trang ở chế độ nền. Sau khi được tạo, nó sẽ được cache và hiển thị thay vì trang dự phòng. Giờ đây phiên bản được cache sẽ hiển thị cho bất kỳ truy cập nào tiếp theo ngay khi có yêu cầu. Đối với cả trang mới và trang hiện có, chúng ta có thể đặt thời gian hết hạn để khi nào Next.js nên xác thực lại (revalidate) và cập nhật nó. Điều này có thể đạt được bằng cách sử dụng thuộc tính `revalidate` như trong phần sau.

### Cập nhật các trang hiện có

Để render lại một trang hiện có, một timeout phù hợp được xác định cho trang. Điều này đảm bảo rằng trang sẽ được xác thực lại bất cứ khi nào hết timeout. Timeout có thể đặt thấp nhất 1 giây. Người dùng sẽ tiếp tục nhìn thấy phiên bản trước đó của trang cho đến khi trang được xác thực lại. Do đó iSSG sử dụng chiến lược [**stale-while-revalidate**](https://web.dev/stale-while-revalidate/) trong đó người dùng sẽ nhận được phiên bản cache hoặc cũ khi quá trình xác thực lại diễn ra. Việc xác thực lại diễn ra trong nền mà không cần build lại toàn bộ.

Chúng ta hãy quay lại ví dụ tạo trang danh sách tĩnh cho các sản phẩm dựa trên dữ liệu trong database. Để làm cho nó cung cấp một danh sách các sản phẩm động, chúng ta sẽ thêm code đặt timeout để build lại trang. Đây là code sau khi thêm timeout.

**pages/products/[id].js**

```js
// Function này sẽ chạy khi build trên build server
export async function getStaticProps() {
  return {
    props: {
      products: await getProductsFromDatabase(),
      revalidate: 60, // Buộc cho trang xác thực lại sau 60 giây
    },
  };
}

// Page component nhận products prop từ getStaticProps khi build
export default function Products({ products }) {
  return (
    <>
      <h1>Products</h1>
      <ul>
        {products.map((product) => (
          <li key={product.id}>{product.name}</li>
        ))}
      </ul>
    </>
  );
}
```

Đoạn code xác thực lại trang sau 60 giây được thêm vào trong function `getStaticProps()`. Khi một request tới, trang tĩnh hiện có sẽ được cung cấp trước. Cứ sau một phút trang tĩnh sẽ được làm mới trong nền với dữ liệu mới. Sau khi được tạo, phiên bản mới của trang tĩnh sẽ được cung cấp cho bất kỳ yêu cầu mới nào trong một phút tiếp theo. Tính năng này có trong Next.js 9.5 trở lên.

## Những ưu điểm

iSSG cung cấp tất cả những ưu điểm của SSG và một số tính năng khác. Danh sách dưới đây là chi tiết mỗi ưu điểm.

1. **Dữ liệu động**: Ưu điểm đầu tiên là lý do iSSG được nghĩ tới. Khả năng hỗ trợ dữ liệu động mà không cần build lại trang web.

2. **Tốc độ**: iSSG ít nhất nhanh bằng SSG vì quá trình truy xuất dữ liệu và render vẫn diễn ra ở chế độ nền. Có ít yêu cầu xử lý trên client hay server.

3. **Tính khả dụng**: Một phiên bản gần nhất của bất kỳ trang nào luôn tồn tại sẵn sàng cho người dùng truy cập. Ngay cả khi quá trình tạo lại không thành công thì phiên bản cũ cũng không thay đổi.

4. **Tính nhất quán**: Khi quá trình tạo lại diễn ra trên máy chủ từng trang một, load trên database và backend thấp và hiệu suất được đảm bảo. Do đó không có thay đổi về độ trễ.

5. **Dễ phân bổ**: Cũng giống như các trang web SSG, các trang web iSSG cũng có thể được phân bổ qua các mạng lưới CDN được sử dụng cho các trang web được render trước.
