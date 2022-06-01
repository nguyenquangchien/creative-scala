## Bàn cờ

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Ở bài tập này và bài tiếp theo, ta sẽ cố gắng luyện sự tinh nhanh để phát hiện ra cấu trúc đệ quy.

Hình thứ nhất là một bàn cờ. Dù có ý kiến cho rằng đó không phải phân dạng, song bàn cờ quả thật có chứa chính nó: một bàn cờ 4x4 có thể thép từ 4 bàn cờ 2x2, một bàn cờ 8x8 từ 4 bàn cờ 4x4, va cứ như vậy. Bức tranh [@fig:fractals:chessboards] thể hiện điều này.

![Bàn cờ phát sinh bằng `count` từ 0 đến 2.](./src/pages/fractals/chessboards.pdf+svg){#fig:fractals:chessboards}

Nhiệm vụ của bạn ở bài tập này là nhận diện cấu trúc đệ quy trong bàn cờ, rồi triển khai một phương thức để vẽ bàn cờ. Khung mã lệnh phương thức này là 

```scala mdoc:silent
def chessboard(count: Int): Image =
  ???
```

Hãy triển khai `chessboard`. Nhớ rằng ta có thể dùng khung mã lệnh đệ quy cấu trúc và kĩ thuật suy luận để dẫn dắt việc triển khai này.

<div class="solution">
`chessboard` là đệ quy cấu trúc trên các số tự nhiên, bởi vậy ta có thể viết ngay khung mã lệnh cho dạng mẫu này.

```scala
def chessboard(count: Int): Image =
  count match {
    case 0 => resultBase
    case n => resultUnit add chessboard(n-1)
  }
```

Cũng như lần trước, ta phải quyết định trường hợp cơ sở base, đơn vị unit, và phép bổ sung để thu được kết quả.
Chúng tôi đã gợi ý bạn bằng cách cho thấy tiến triển của bàn cờ ở [@fig:recursion:chessboards].
Từ đây, ta có thể thấy rằng trường hợp cơ sở là bàn cờ 2x2.

```scala mdoc:silent
val blackSquare = Image.rectangle(30, 30).fillColor(Color.black)
val redSquare   = Image.rectangle(30, 30).fillColor(Color.red)

val base =
  (redSquare.beside(blackSquare)).above(blackSquare.beside(redSquare))
```

Bây giờ hãy xác định đơn vị unit và phép bổ sung.
Ở đây ta thấy được sự thay đổi khác những ví dụ trước.
Đơn vị là giá trị mà ta nhận được từ lời gọi đệ quy `chessboard(n-1)`.
Phép bổ sung là `(unit beside unit) above (unit beside unit)`.

Tổng hợp tất cả lại ta có

```scala mdoc:reset:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```
```scala mdoc:silent
def chessboard(count: Int): Image = {
  val blackSquare = Image.rectangle(30, 30).fillColor(Color.black)
  val redSquare   = Image.rectangle(30, 30).fillColor(Color.red)

  val base =
    (redSquare.beside(blackSquare)).above(blackSquare.beside(redSquare))
  count match {
    case 0 => base
    case n =>
      val unit = chessboard(n-1)
      (unit.beside(unit)).above(unit.beside(unit))
  }
}
```
</div>

Nếu bạn đã có kinh nghiệm lập trinh từ trước, bạn có thể nghĩ ngay đến việc lập bàn cờ bằng hai vòng lặp lồng nhau.
Ở đây ta tiếp cận theo cách khác bằng việc định nghĩa một bàn cờ lớn ghép từ các bàn cờ nhỏ.
Nắm được những cách tiếp cận riêng này nhằm phân tách vấn đề chính là khâu then chốt để thành thạo lập trình hàm.


## Tam giác Sierpinkski

Tam giác Sierpinkski, thể hiện trên [@fig:fractals:sierpinski], là một phân dạng nổi tiếng. (Chặt chẽ mà nói, [@fig:fractals:sierpinski] cho thấy một hình tam giác Sier*pink*ski màu hồng.)

![Tam giác Sierpinkski.](./src/pages/fractals/sierpinski.pdf+svg){#fig:recursion:sierpinski}

Dù trông có vẻ phức tạp nhưng ta có thể phân chia cấu trúc này dưới dạng cho phép ta phát sinh bằng đệ quy cấu trúc trên các số tự nhiên.
Hãy triển khai một phương thức theo khung mã lệnh sau

```scala mdoc
def sierpinski(count: Int): Image =
  ???
```

Lần này thì không có gợi ý nữa.
Ta đã thấy tất cả mọi thứ cần biết rồi.

<div class="solution">
Khâu then chốt là nhận thấy được đơn vị cơ bản của tam giác Sierpinski chính là `triangle above (triangle beside triangle)`.
Một khi phân tích được thế này, mã lệnh sẽ có cấu trúc giống hệt như `chessboard`.
Sau đây là cách triển khai của chúng tôi.

```scala mdoc:reset:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```
```scala mdoc
def sierpinski(count: Int): Image = {
  val triangle = Image.triangle(10, 10).strokeColor(Color.magenta)
  count match {
    case 0 => triangle.above(triangle.beside(triangle))
    case n =>
      val unit = sierpinski(n-1)
      unit.above(unit.beside(unit))
  }
}
```
</div>


