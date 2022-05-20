## Phương thức

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Ở một chương trước ta đã tạo nên hình như trên [@fig:methods:sequential-boxes] bằng chương trình

![Năm ô tô màu Royal Blue](./src/pages/programs/sequential-boxes.pdf+svg){#fig:methods:sequential-boxes}

```scala mdoc:silent
val box =
  Image.rectangle(40, 40).
    strokeWidth(5.0).
    strokeColor(Color.royalBlue.spin(30.degrees)).
    fillColor(Color.royalBlue)

box beside box beside box beside box beside box
```

Hãy hình dung ta muốn đổi màu các ô này.
Ngay bây giờ ta có thể viết lại những biểu thức với các màu được chọn khác nhau.

```scala mdoc:silent
val paleGoldenrod = {
  val box =
    Image.rectangle(40, 40).
      strokeWidth(5.0).
      strokeColor(Color.paleGoldenrod.spin(30.degrees)).
      fillColor(Color.paleGoldenrod)

  box beside box beside box beside box beside box
}

val lightSteelBlue = {
  val box =
    Image.rectangle(40, 40).
      strokeWidth(5.0).
      strokeColor(Color.lightSteelBlue.spin(30.degrees)).
      fillColor(Color.lightSteelBlue)

  box beside box beside box beside box beside box
}

val mistyRose = {
  val box =
    Image.rectangle(40, 40).
      strokeWidth(5.0).
      strokeColor(Color.mistyRose.spin(30.degrees)).
      fillColor(Color.mistyRose)

  box beside box beside box beside box beside box
}
```

Làm vậy thì chán chết.
Mỗi biểu thức chỉ khác nhau rất ít.
Sẽ tốt bao nhiêu nếu ta có thể nắm được dạng mẫu chung này và cho phép đổi màu.
Ta có thể thực hiện điều đó bằng cách khai báo một phương thức.

```scala mdoc:silent
def boxes(color: Color): Image = {
  val box =
    Image.rectangle(40, 40).
      strokeWidth(5.0).
      strokeColor(color.spin(30.degrees)).
      fillColor(color)

  box beside box beside box beside box beside box
}

// Create boxes with different colors
boxes(Color.paleGoldenrod)
boxes(Color.lightSteelBlue)
boxes(Color.mistyRose)
```

Bạn hãy tự tay thử xem có thu được kết quả tương tự không: khi dùng phương thức và khi viết ra tất tần tật.

Bây giờ khi đã thấy một ví dụ về khai báo phương thức, ta cần giải thích cú pháp của phương thức. Tiếp theo, ta sẽ xem xét cách viết phương thức, ngữ nghĩa của lời gọi phương thức, và cách hoạt động của phép thay thế ra sao.
