## Viết mã lệnh bên ngoài console

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Mã lệnh mà ta đã viết trong console sẽ rắc rỗi khi chạy ngoài console. Chẳng hạn, đưa mã lệnh sau vào file `Example.scala` trong đường dẫn `src/main/scala`.

```scala mdoc:silent
Image.circle(100).fillColor(Color.paleGoldenrod).strokeColor(Color.indianRed)
```

Bây giờ hãy khởi động lại SBT và thử vào console. Bạn sẽ thấy một lỗi giống như

```bash
[error] src/main/scala/Example.scala:1: expected class or object definition
[error] circle(100) fillColor Color.paleGoldenrod strokeColor Color.indianRed
[error] ^
[error] one error found
```

Bạn cũng sẽ thấy tương tự khi sử dụng môi trường IDE.

Vấn đề là ở chỗ:

- Scala đang cố gắng biên dịch tất cả mã lệnh trước khi console khởi động, và
- có những hạn chế đối với mã lệnh viết trong file vốn lại không ảnh hưởng đến mã lệnh viết trực tiếp vào console.

Ta cần biết về những hạn chế này và thay đổi cách viết mã lệnh trong file một cách tương ứng.

Thông báo lỗi cho ta lời gợi ý: `expected class or object definition` (trông đợi một định nghĩa lớp hoặc đối tượng). Ta chưa biết lớp là cái gì, song ta đã biết về đối tượng---mọi giá trị đều là đối tượng. Trong Scala, tất cả mã lệnh viết trong một file phải nằm trong một đối tượng hoặc một lớp. Ta có thể dễ dàng định nghĩa một đối tượng bằng cách bao bọc lấy biểu thức theo cách dưới đây.

```scala mdoc:silent
object Example {
  Image.circle(100).fillColor(Color.paleGoldenrod).strokeColor(Color.indianRed).draw()
}
```

Bây giờ mã lệnh lại không biên dịch vì một lí do khác. Ta sẽ thấy rất nhiều lỗi kiểu như 

```bash
[error] doodle/shared/src/main/scala/doodle/examples/Example.scala:1: not found: value Image
[error]   Image.circle(100).fillColor(Color.paleGoldenrod).strokeColor(Color.indianRed).draw()
[error]   ^
```

Trình biên dịch nói rằng ta đã dùng một cái tên, `circle`, song trình biên dịch không biết tên này chỉ tới giá trị nào.
Nó sẽ có vấn đề tương tự với `Color` ở mã lệnh bên trên.
Chúng tôi sẽ nói kĩ hơn về tên sau.
Ngay bây giờ ta hãy bảo trình biên dịch có thể tìm các tên này ở đâu bằng cách thêm vài câu lệnh `import`.
Cái tên `Color` được tìm thấy trong một *gói* có tên `doodle.core`, và tên `circle` nằm trong đối tượng `Image` đến lượt nó lại nằm trong `doodle.image`.
Ta có thể bảo trình biên dịch dùng tất cả các tên trong `doodle.core`, và tất cả tên trong `doodle.image` bằng cách viết

```scala mdoc:silent
import doodle.core._
import doodle.image._
```

Còn có vài tên gọi khác mà trình biên dịch sẽ cần tìm kiếm để chạy được mã lệnh hoàn chỉnh ta viết.
Ta có thể nhập các tên này bằng những dòng lệnh

```scala mdoc:silent
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Ta có thể đặt tất cả những câu lệnh nhập import này ở đầu file, như vậy mã lệnh hoàn chỉnh sẽ như sau

```scala
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._

object Example {
  Image.circle(100).fillColor(Color.paleGoldenrod).strokeColor(Color.indianRed).draw()
}
```

Với tất cả đã xong xuôi, mã lệnh sẽ biên dịch được mà không vấn đề gì.

Bây giờ khi ta vào console trong SBT, ta có thể gọi đến mã lệnh đã viết bằng cái tên `Example` mà ta đã đặt cho nó.

```scala
Example // vẽ hình
```

### Bài tập {-}

Nếu bạn chưa làm, hãy lưu mã lệnh trên vào file `src/main/scala/Example.scala` rồi kiểm tra để đảm bảo rằng mã lệnh biên dịch và bạn có thể truy cập được nó từ console.
