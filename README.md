# Creative Scala - Scala sáng tạo

Tác giả: [Dave Gurnell](http://twitter.com/davegurnell) và
[Noel Welsh](http://twitter.com/noelwelsh).
Bản quyền 2015--2020.

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Giấy phép Creative Commons" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.

## Tổng quan

Scala sáng tạo là một ebook miễn phí dành cho lập trình viên
chưa có kinh nghiệm với Scala từ trước.
Cuốn sách được sắp xếp để cho bạn trải nghiệm đầu tiên nhưng mấu chốt về lập trình hàm.
Chúng tôi coi như bạn đã quen biết một ngôn ngữ lập trình khác
nhưng lại rất ít hoặc không có kinh nghiệm với Scala hay ngôn ngữ lập trình hàm nói chung.

Đây là phiên bản 2 của Scala Sáng tạo, cuốn này vẫn đang được phát triển.
Để xem phiên bản thứ nhất, hãy xem nhánh `master`.

Mục đích của chúng tôi là nhằm biểu diễn các khối dựng mà lập trình viên Scala 
dùng để lập chương trình theo cách rõ ràng, gọn ghẽ, đặc tả.
Bạn cần từ 2 đến 3 giờ để hoàn thành các bài tập trong sách này,
sau đó chúng tôi hi vọng rằng bạn có cảm giác về những gì Scala có thể giúp bạn viết các trình ứng dụng.

Các bài tập trong Scala Sáng tạo đều dựa trên 
một thư viện đồ họa hàm có tên [Doodle][doodle].
Dù Doodle được thiết kế chủ yếu là nhằm khiến cho việc lập trình thú vị và sáng tạo,
nó vẫn dựa trên các khái niệm tổng quát, áp dụng được cho các ứng dụng trong kinh doanh.

## Dựng nội dung tài liệu

Scala sáng tạo [hệ thống dựng ebook của Underscore][ebook-template].

Cách đơn giản nhất để dựng cuốn sách này là dùng [Docker Compose](http://docker.com):

- hãy cài đặt Docker Compose (`brew install docker-compose` trên nền OS X; hay tải về từ [docker.com](http://docker.com/)); rồi
- chạy `go.sh` (hay `docker-compose run book bash` nếu `go.sh` không hoạt động).

Việc này sẽ mở ra một dòng lệnh `bash` shell chạy trong hộp chứa Docker (container) trong đó có tất cả những công cụ phụ thuộc (dependencies) cần để dựng cuốn sách này. Từ dòng lệnh, hãy chạy:

- `npm install`; rồi
- `sbt`.

Bên trong `sbt` bạn có thể gõ các lệnh `pdf`, `html`, `epub`, hay `all` để dựng các phiên bản sách mong muốn. Các mục tiêu được đặt trong thư mục `dist`:

[doodle]: https://github.com/creativescala/doodle
[ebook-template]: https://github.com/underscoreio/underscore-ebook-template

