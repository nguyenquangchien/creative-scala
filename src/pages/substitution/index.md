# Mô hình thay thế để ước lượng

Ta cần thiết lập mô hình tư duy về cách ước lượng các biểu thức Scala, để từ đó hiểu được chương trình ta viết sẽ làm gì.
Đến giờ, ta đang dùng một mô hình không chính thức.
Ở mục này ta sẽ làm cho mô hình "bài bản" hơn bằng cách tìm hiểu về *mô hình thay thế* để ước lượng.
Cũng như nhiều thứ trong lập trình, ta hay dùng từ đao to búa lớn để chỉ khái niệm đơn giản.
Trường hợp này, có lẽ bạn đã nghe về phép thay thế trong môn học đại số ở bậc phổ thông, và giờ ta chỉ là nói về những khái niệm đó trong một ngữ cảnh mới.

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
