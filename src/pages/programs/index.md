# Viết các chương trình lớn hơn

Ta đã đến chỗ bắt đầu bất tiện khi phải gõ cả chương trình vào dấu nhắc console. 
Ở chương này ta sẽ tìm hiểu thêm hai công cụ để viết các chương trình lớn hơn:

- lưu chương trình vào file để ta không phải gõ đi gõ lại mã lệnh;
- đặt tên cho các giá trị để ta có thể sử dụng lại chúng.

<div class="callout callout-info">
Nếu bạn chạy các ví dụ từ dòng lệnh SBT console bên trong Doodle thì chúng sẽ tự hoạt động. Nếu không, bạn sẽ cần phải mở đầu mã lệnh với những câu lệnh nhập import sau để Doodle dùng được.

```scala mdoc:silent
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```
</div>

