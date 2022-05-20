# Phương thức

Ta đã dùng phương thức rồi---phương thức là cách mà ta tương tác với đối tượng.
Ở chương này ta sẽ học cách tự viết các phương thức.

Các tên cho phép ta khái quát hoá những biểu thức.
Phương thức cho pháp ta khái quát hoá và *tổng quát* những biểu thức.
Nói tổng quát nghĩa là khả năng diễn đạt một nhóm những thức có liên quan, như trong trường hợp này là các biểu thức.
Phương thức thể hiện một bản mẫu của một biểu thức, và cho phép mã lệnh gọi nó điền vào các phần của bản mẫu đó bằng cách truyền đến các tham số phương thức.

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


