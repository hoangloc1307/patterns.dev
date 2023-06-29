# React Server Components

Server Components bổ sung cho SSR bằng cách thực hiện render một intermediate abstraction mà không cần thêm vào gói JavaScript.

---

React team đang làm việc với [**zero-bundle-size React Server Components**](https://legacy.reactjs.org/blog/2020/12/21/data-fetching-with-react-server-components.html), mục tiêu của nó là cho phép **UX hiện đại với mô hình tư duy dựa trên server**. Điều này khác hoàn toàn với Server-Side Rendering (SSR) của các component và có thể dẫn đến các gói JavaScript ở client [**nhỏ hơn**](https://twitter.com/sophiebits/status/1341098388062756867) đáng kể.

Hướng đi của công việc này rất thú vị và mặc dù nó chưa sẵn sàng cho production nhưng nó đáng để bạn theo dõi. Các tài nguyên sau đây có thể bạn quan tâm:

- [**RFC**](https://github.com/reactjs/rfcs/blob/bf51f8755ddb38d92e23ad415fc4e3c02b95b331/text/0000-server-components.md) đáng để đọc cũng như [**cuộc trò chuyện của Dan và Lauren**](https://www.youtube.com/watch?v=TQQPAU21ZUw) đáng để xem.
- [**React 18 status for Next.js**](https://nextjs.org/docs/getting-started/react-essentials) và [**Server Components roadmap for Next.js**](https://github.com/vercel/next.js/discussions/31263)
- [**React 18 beta status**](https://twitter.com/reactjs/status/1460380211262930948)
- [**Shopify Hydrogen and Server Components**](https://shopify.dev/docs/custom-storefronts/hydrogen/framework/react-server-components)

## Những giới hạn của server-side rendering

Server-side rendering của client client-side JavaScript hiện nay có thể không tối ưu. JavaScript cho các component của bạn được render trên server thành một chuỗi HTML. HTML này được chuyển tới trình duyệt, điều này có thể khiến FCP và LCP nhanh.

Tuy nhiên, JavaScript vẫn cần được fetch để có tính tương tác, điều này có thể đạt được thông qua bước hydrate. Server-side rendering thường được sử dụng cho lần tải trang đầu tiên, do đó sau quá trình hydrate bạn sẽ không thấy nó được sử dụng lại.

**Note:**
Đúng là bạn có thể xây dựng ứng dụng React chỉ chạy trên server (server-only) tận dụng SSR và hoàn toàn tránh được việc hydrate trên client. Tuy nhiên khi có sự tương tác phức tạp trong ứng dụng, thường cần phải vượt ra khỏi React. Mô hình kết hợp mà Server Components sẽ cho phép bạn quyết định điều này trên cơ sở từng component.

Với React Server Component, các component của chúng ta có thể refetch thường xuyên. Một ứng dụng có các component rerender mỗi khi có dữ liệu mới có thể chạy trên server, hạn chế lượng code cần gửi tới client.

> [RFC]: Các developer phải liên tục đưa ra lựa chọn về việc sử dụng các package của bên thứ ba. Sử dụng một package để render một vài markdown hoặc định dạng ngày để thuận tiện cho chúng ta với tư cách là developer, nhưng nó làm tăng kích thước code và ảnh hưởng đến hiệu suất của người dùng của chúng ta.

**NoteWithMarkdown.js**

```js
// Trước khi sử dụng Server Components
import marked from "marked"; // 35.9K (11.2K gzipped)
import sanitizeHtml from "sanitize-html"; // 206K (63.3K gzipped)

function NoteWithMarkdown({text}) {
  const html = sanitizeHtml(marked(text));
  return (/* render */);
}
```

## Server Components

Server Components mới của React bổ sung cho Server-Side Rendering, cho phép render thành một định dạng intermediate abstraction mà không cần thêm gói JavaScript. Điều này vừa cho phép hợp nhất server-tree với client-tree mà không làm mất trạng thái và cho phép mở rộng quy mô cho nhiều component hơn.

Server Components không phải là sự thay thế cho SSR. Khi được kết nối với nhau, chúng hỗ trợ render nhanh chóng ở định dạng trung gian, sau đó cơ sơ hạ tầng Server-side rendering render định dạng này thành HTML cho phép các lần paint sớm vẫn nhanh.
