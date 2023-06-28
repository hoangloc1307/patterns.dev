##### Build server

Build server là một môi trường trong quá trình phát triển phần mềm nơi mã nguồn được biên dịch, xây dựng và tạo ra phiên bản cuối cùng của ứng dụng hoặc trang web. Trong một số trường hợp, quá trình render có thể xảy ra trên build server để tạo ra các tệp HTML hoặc tệp tĩnh đã được render trước. Sau đó, các tệp này được triển khai lên web server để phục vụ cho trình duyệt.

---

##### Bundle

Trong lĩnh vực phát triển phần mềm, "bundle" là một thuật ngữ để chỉ một tập hợp các tệp tin (files) hoặc mã nguồn được đóng gói lại thành một đơn vị độc lập để sử dụng trong quá trình triển khai hoặc chạy ứng dụng. Thường thì "bundle" được sử dụng để chỉ các tệp tin JavaScript, CSS và các tệp tin tài nguyên (như hình ảnh, video, âm thanh) mà được gộp lại thành một tệp tin duy nhất hoặc một nhóm tệp tin để tăng tốc quá trình tải và cung cấp ứng dụng cho người dùng

---

##### Cold boot

Cold boot là quá trình khởi động một serverless function trong môi trường serverless. Khi một serverless function không được sử dụng trong một khoảng thời gian, nhà cung cấp dịch vụ cloud có thể ngừng hoạt động của nó để tiết kiệm tài nguyên. Khi có yêu cầu mới đến, function cần phải khởi động lại từ trạng thái "lạnh", gọi là cold boot. Thời gian khởi động lại từ trạng thái "lạnh" có thể mất nhiều thời gian hơn so với khởi động từ trạng thái "nóng" (khi function vẫn đang hoạt động và sẵn sàng để xử lý yêu cầu). Điều này có thể gây ra sự chậm trễ trong việc xử lý yêu cầu đầu tiên sau một khoảng thời gian không hoạt động.

---

##### Edge

Edge trong kiến trúc mạng đề cập đến các máy chủ lưu trữ dữ liệu và phần mềm phân phối nội dung (CDN - Content Delivery Network) được đặt tại các vị trí gần người dùng cuối trên mạng. Trong trường hợp render tại Edge, quá trình render xảy ra tại các máy chủ Edge gần người dùng. Điều này giúp giảm độ trễ và cải thiện hiệu suất bằng cách đưa gần nhất nội dung đã được render đến người dùng.

---

##### FCP (First Contentful Paint)

FCP đo thời gian từ khi trang web bắt đầu tải đến khi trình duyệt hiển thị nội dung đầu tiên lên màn hình. Nó đại diện cho thời gian mà người dùng thấy được nội dung đầu tiên xuất hiện trên trang web. Thời gian FCP được tính từ khi trình duyệt bắt đầu tải tệp HTML đến khi nội dung đầu tiên được vẽ trên màn hình, bao gồm cả văn bản, hình ảnh, và các thành phần giao diện người dùng khác. Nó không phụ thuộc vào việc tải xong toàn bộ trang, chỉ quan tâm đến sự xuất hiện nhanh chóng của nội dung ban đầu.

---

##### Hydrate

Trong ngữ cảnh phát triển web, "hydrate" là một thuật ngữ để chỉ quá trình kết hợp (render) mã HTML tĩnh đã được tải về từ máy chủ với các thành phần tương tác (interactive components) trên một trang web hoặc ứng dụng. Quá trình hydrate xảy ra sau khi mã HTML tĩnh đã được tải xuống và hiển thị ban đầu trên máy khách (client). Thông thường, mã HTML tĩnh được tạo ra từ quá trình Server-Side Rendering (SSR) hoặc quá trình Static Site Generation (SSG). Mã HTML này chứa dữ liệu tĩnh và các thành phần giao diện người dùng (UI components) mà chưa có tính năng tương tác. Khi hydrate được thực hiện, trình duyệt sẽ xử lý các thành phần tương tác trong mã HTML tĩnh và kết hợp chúng với mã JavaScript và CSS để tạo ra các thành phần tương tác hoạt động trên trang web hoặc ứng dụng. Quá trình hydrate thường bao gồm việc gắn kết các sự kiện (event binding), quản lý trạng thái (state management) và cập nhật giao diện người dùng theo sự tương tác của người dùng.

---

##### Layout shift

Là một chỉ số đo lường sự thay đổi bố cục trên trang web. Nó đo lường mức độ sự di chuyển và thay đổi vị trí của các phần tử trên trang trong quá trình tải trang. Khi trang web được tải, các phần tử như hình ảnh, quảng cáo, hoặc nội dung động có thể thay đổi vị trí hoặc kích thước của chúng. Layout shift đo lường mức độ thay đổi này và tính toán điểm số dựa trên diện tích và khoảng cách di chuyển của các phần tử.

---

##### LCP (Largest Contentful Paint)

LCP đo thời gian mà trình duyệt mất để vẽ lên màn hình phần tử nội dung lớn nhất (bao gồm văn bản, hình ảnh, video) trong khung nhìn (viewport) hiện tại. Nó cho thấy thời gian mà người dùng phải chờ đợi để thấy được nội dung quan trọng nhất xuất hiện trên trang web. Thời gian LCP được tính từ khi trang web bắt đầu tải cho đến khi phần tử nội dung lớn nhất được vẽ lên màn hình. Đối với trang web động, LCP thường là hình ảnh, video hoặc phần tử giao diện người dùng quan trọng. Đối với trang web tĩnh, LCP thường là phần tử văn bản đầu tiên.

---

##### Rehydration

Rehydration là quá trình tái tạo hoặc khôi phục trạng thái và hành vi của một ứng dụng web sau khi nó đã được tải lần đầu. Trong ngữ cảnh của ứng dụng web đơn trang (Single-Page Application - SPA), rehydration đề cập đến việc đính kèm lại các sự kiện và trạng thái của ứng dụng sau khi nó đã được tải lần đầu. Khi một trang SPA được tải lần đầu, trình duyệt chỉ nhận được một tệp HTML cơ bản và tệp JavaScript chứa mã nguồn của ứng dụng. Quá trình rendering ban đầu trên trình duyệt chỉ tạo ra một giao diện tĩnh không có tính năng tương tác. Sau khi trang đã được tải, mã JavaScript sẽ chạy và gắn kết các sự kiện, liên kết dữ liệu và khôi phục trạng thái ban đầu của ứng dụng để biến giao diện tĩnh thành một ứng dụng tương tác đầy đủ.

---

##### Render

Trong ngữ cảnh của phát triển web, render thường được sử dụng để chỉ quá trình chuyển dữ liệu, code thành giao diện người dùng. Khi trình duyệt nhận được mã HTML, CSS và JavaScript từ máy chủ web, nó sẽ thực hiện quá trình render để hiển thị nội dung lên màn hình cho người dùng xem. Render cũng có thể liên quan đến việc tạo ra các phần tử động bằng cách sử dụng các công cụ phía server hoặc phía client như React, Angular hoặc Vue. Trong trường hợp này, render có nghĩa là tạo ra các thành phần UI hoặc các giao diện người dùng được xây dựng bằng mã JavaScript và sau đó được hiển thị trên trình duyệt web.

---

##### Render all at once

Dịch ra là render toàn bộ cùng một lúc. Khi sử dụng phương pháp này, quá trình render được thực hiện cho toàn bộ nội dung của trang web hoặc một phần tử lớn trong một lần. Kết quả render hoàn chỉnh được gửi tới trình duyệt và hiển thị cho người dùng cùng một lúc. Điều này có nghĩa là người dùng sẽ phải chờ đợi cho đến khi quá trình render hoàn tất trước khi thấy bất kỳ nội dung nào.

---

##### Render partially

Dịch ra là render một phần. Phương pháp này tập trung vào việc hiển thị một phần nội dung của trang web ngay từ đầu, trong khi các phần còn lại được xử lý sau đó. Điều này đồng nghĩa với việc người dùng sẽ thấy một phần trang web được hiển thị và có thể tương tác, nhưng có thể có các phần chưa được render hoặc tải về. Các phần chưa render sẽ được xử lý và hiển thị sau khi dữ liệu hoặc tài nguyên tương ứng được tải về.

---

##### Render progressively

Dịch ra là render dần dần. Phương pháp này tạo ra một hiệu ứng hiển thị dữ liệu dần dần trên trang web trong quá trình tải trang. Thay vì chỉ hiển thị một phần của trang web ban đầu, trình duyệt sẽ hiển thị dữ liệu ngay khi nó được tải về từ server. Trình duyệt sẽ tiếp tục hiển thị và cập nhật nội dung ngay khi dữ liệu mới được tải về, cho phép người dùng nhìn thấy nội dung mới nhất trong quá trình tải trang.

---

##### Rendering pattern

Có thể hiểu "rendering pattern" như một cách thức hay mẫu thiết kế được sử dụng để thực hiện quá trình render nội dung trên một giao diện người dùng.

---

##### Rollback

Trong lĩnh vực phát triển phần mềm và quản lý dự án, "rollback" (cũng được gọi là "revert") đề cập đến quá trình hoặc hành động quay lại trạng thái hoặc phiên bản trước đó của một hệ thống, ứng dụng hoặc dự án. Khi thực hiện các thay đổi, cập nhật hoặc triển khai mới trong hệ thống, có thể xảy ra các vấn đề như lỗi, hỏng hóc hoặc phản hồi không tốt từ người dùng. Trong trường hợp này, rollback được sử dụng để hoàn nguyên hoặc quay lại một trạng thái hoặc phiên bản trước đó đã được xác định là ổn định và không gặp vấn đề.

---

##### Serverless function

Còn được gọi là Functions as a Service (FaaS), là một mô hình điện toán đám mây trong đó nhà cung cấp đám mây quản lý hoàn toàn việc triển khai và quản lý các hàm (functions) của ứng dụng. Trong mô hình này, bạn không cần phải quản lý các máy chủ hoặc hạ tầng cơ sở hạ tầng. Thay vào đó, bạn chỉ cần tập trung vào việc viết mã cho các hàm và nhà cung cấp đám mây sẽ tự động quản lý việc chạy và mở rộng chúng. Một serverless function là một khối mã đơn giản, thường được thiết kế để thực hiện một tác vụ cụ thể hoặc xử lý một yêu cầu HTTP. Các serverless function được triển khai lên đám mây và có thể được gọi bất kỳ khi nào có yêu cầu, mà không cần phải duy trì một máy chủ hoạt động liên tục.

---

##### Skeleton

Trong ngữ cảnh phát triển web và ứng dụng di động, skeleton (hoặc skeleton screen) là một phương pháp hiển thị tạm thời để đại diện cho nội dung thực tế đang được tải. Skeleton thường được thiết kế với một hình dạng và cấu trúc tương tự như nội dung thực sự sắp được tải. Thông qua việc sử dụng skeleton, người dùng có thể thấy được hình dạng và bố cục tổng thể của nội dung sẽ xuất hiện, điều này giúp tránh cảm giác chờ đợi và giữ cho người dùng có sự tương tác liền mạch. Skeleton có thể được hiển thị trong thời gian ngắn trước khi dữ liệu thực sự được tải xong hoặc được dùng để tạo ra cảm giác chờ đợi mượt mà trong quá trình tải trang.

---

##### TTFB (Time To First Byte)

Nó là một thước đo thời gian từ khi máy khách (client) gửi một yêu cầu HTTP đến máy chủ (server) cho đến khi máy chủ trả về byte đầu tiên của phản hồi.

---

##### User-centric metrics

Khi nói về "user-centric metrics", đó là các tiêu chí hoặc thông số được sử dụng để đo lường, đánh giá và cải thiện trải nghiệm người dùng. Các user-centric metrics thường tập trung vào cách người dùng tương tác với ứng dụng và cảm nhận của họ về chất lượng trải nghiệm. Ví dụ về user-centric metrics có thể bao gồm:

- **Thời gian phản hồi (response time)**: Thời gian mà hệ thống mất để phản hồi sau khi người dùng thực hiện một hành động. Đo lường thời gian phản hồi giúp đánh giá khả năng đáp ứng nhanh chóng và hiệu quả của ứng dụng.
- **Tốc độ tải trang (page load time)**: Thời gian mà trang web hoặc ứng dụng mất để hiển thị hoàn chỉnh trên trình duyệt của người dùng. Tốc độ tải trang là một yếu tố quan trọng trong việc tạo trải nghiệm tốt và giữ chân người dùng.
- **Tỷ lệ thoát (bounce rate)**: Tỷ lệ người dùng rời khỏi trang web hoặc ứng dụng sau khi chỉ xem một trang duy nhất. Tỷ lệ thoát thường được sử dụng để đo lường mức độ hấp dẫn của trang hoặc ứng dụng và xác định xem liệu người dùng có tiếp tục tương tác hay không.
- **Satisfaction ratings (đánh giá sự hài lòng)**: Phản hồi hoặc đánh giá của người dùng về trải nghiệm của họ trên ứng dụng hoặc trang web. Đánh giá sự hài lòng giúp đo lường mức độ hài lòng của người dùng và nhận xét về chất lượng trải nghiệm.

---

##### Web server

Web server là máy chủ (server) chịu trách nhiệm xử lý yêu cầu từ trình duyệt web và phản hồi bằng cách trả về nội dung tương ứng. Trong trường hợp render trên web server, trình duyệt gửi yêu cầu tới web server, web server sẽ thực hiện quá trình render dữ liệu và mã nguồn thành HTML hoặc giao diện người dùng hoàn chỉnh trước khi trả về cho trình duyệt.

---

##### Webhook

Webhook là một phương thức giao tiếp tự động giữa các ứng dụng thông qua HTTP. Nó cho phép một ứng dụng gửi thông tin hoặc sự kiện (event) tới một URL cụ thể (endpoint) trên một ứng dụng hoặc dịch vụ khác. Khi một sự kiện xảy ra trong nguồn thông tin (source), ví dụ như một hành động của người dùng hoặc một cập nhật trong cơ sở dữ liệu, nguồn thông tin này sẽ gửi một HTTP POST request chứa dữ liệu liên quan đến sự kiện tới endpoint của webhook. Ứng dụng hoặc dịch vụ nhận được webhook sẽ xử lý dữ liệu và thực hiện các hành động tương ứng.
