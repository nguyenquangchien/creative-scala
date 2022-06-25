## Phương thức lồng ghép

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Phương thức là một lời khai báo.
Phần thân phương thức có thể chứa những lời khai báo cùng biểu thức.
Do vậy, một phương pháp khai bấo có thể chứa những lời khai báo phương thức khác.

Để thấy được tại sao điều này hữu ích, ta hãy cùng xem phương thức đã viết trước đây:

```scala mdoc:silent
def cross(count: Int): Image = {
  val unit = Image.circle(20)
  count match {
    case 0 => unit
    case n => unit.beside(unit.above(cross(n-1)).above(unit)).beside(unit)
  }
}
```

Ta đã khai báo `unit` bên trong phương thức `cross`.
Điều này nghĩa là lời khai báo `unit` chỉ có phạm vi bên trong phần thân của `cross`.
Một quy tắc thực hành hay, đó là hạn chế phạm vi khai báo ở mức tối thiểu, để tránh tình cờ phủ bóng vào những lời khai báo khác. 
Dù vậy, hãy cùng xét động thái của `cross` trong lúc thực thi và ta sẽ thấy rằng nó có một số đặc tính không như mong muốn.

Ta sẽ dùng mô hình thay thế đã đề cập để khai triển `cross(1)`.

```scala
cross(1)
// Khai triển thành 
{
  val unit = Image.circle(20)
  1 match {
    case 0 => unit
    case n => unit.beside(unit.above(cross(n-1)).above(unit)).beside(unit)
  }
}
// Khai triển thành 
{
  val unit = Image.circle(20)
  unit.beside(unit.above(cross(0)).above(unit)).beside(unit)
}
// Khai triển thành 
{
  val unit = Image.circle(20)
  unit.beside(unit.above
  {
    val unit = Image.circle(20)
    0 match {
      case 0 => unit
      case n => unit.beside(unit.above(cross(n-1)).above(unit)).beside(unit)
    }
  }
  .above(unit)).beside(unit)
}
// Khai triển thành 
{
  val unit = Image.circle(20)
  unit.beside(unit.above
  {
    val unit = Image.circle(20)
    unit
  }
  .above(unit)).beside(unit)
}
```

Lý do để dẫn ra đây toàn bộ khai triển dài dòng là nhằm cho thấy ta đang tạo lại `unit` mỗi lần ta đệ quy bên trong `cross`.
Ta có thể chứng minh điều này là đúng bằng cách mỗi lần tạo nên `unit` sẽ in thứ gì đó ra màn hình.

```scala mdoc:reset:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```
```scala mdoc
def cross(count: Int): Image = {
  val unit = {
    println("Tạo unit")
    Image.circle(20)
  }
  count match {
    case 0 => unit
    case n => unit.beside(unit.above(cross(n-1)).above(unit)).beside(unit)
  }
}

cross(1)
```

Điều này không có gì đáng kể với `unit` vì ở đây nó rất nhỏ, song trong trường hợp ta phải làm tác vụ nào chiếm nhiều bộ nhớ hay mất nhiều thời gian thì việc lặp lại không cần thiết như vậy thật không phải điều mong muốn.

Ta có thể giải quyết vấn đề này bằng việc chuyển `unit` ra ngoài `cross`.

```scala mdoc:reset:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
```
```scala mdoc
val unit = {
  println("Tạo unit")
  Image.circle(20)
}

def cross(count: Int): Image = {
  count match {
    case 0 => unit
    case n => unit beside (unit above cross(n-1) above unit) beside unit
  }
}

cross(1)
```

Điều này lại không như mong muốn vì giờ đây `unit` lại có một phạm vi lớn hơn cần thiết. 
Một giải pháp hay hơn là dùng phương thức lồng ghép hay nội tại.

```scala mdoc:reset:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```
```scala mdoc
def cross(count: Int): Image = {
  val unit = {
    println("Tạo unit")
    Image.circle(20)
  }
  def loop(count: Int): Image = {
    count match {
      case 0 => unit
      case n => unit beside (unit above loop(n-1) above unit) beside unit
    }
  }

  loop(count)
}

cross(1)
```

Cách này có động thái mà ta muốn hướng tới, chỉ tạo `unit` đúng một lần đồng thời hạn chế tối thiểu phạm vi của nó.
Phương thức nội tại `loop` dùng đệ quy cấu trúc hệt như trước đây.
Ta chỉ cần đảm bảo gọi đến nó bên trong `cross`.
Tôi thường gọi những phương thức nội tại như vậy là `loop` (vòng lặp) hoặc `iter` (gọi tắt iterate: lặp) để chỉ định rằng chúng đang thực hiện một vòng lặp.

Kĩ thuật này chỉ là một biến thể nỏ của những gì ta đã làm trước đây, song hãy cùng làm ít bài tập để đảm bảo rằng ta nắm được dạng mẫu lập trình.


### Bài tập {-}

#### Bàn cờ {-}

Hãy viết lại `chessboard` (bàn cờ) bằng một phương thức lồng ghép sao cho `blackSquare` (ô đen), `redSquare` (ô đỏ), và `base` (phần cơ sở) chỉ được tạo ra một lần khi `chessboard` được gọi tới.

```scala mdoc
def chessboard(count: Int): Image = {
  val blackSquare = Image.square(30) fillColor Color.black
  val redSquare   = Image.square(30) fillColor Color.red

  val base =
    (redSquare   beside blackSquare) above (blackSquare beside redSquare)
  count match {
    case 0 => base
    case n =>
      val unit = cross(n-1)
      (unit beside unit) above (unit beside unit)
  }
}
```

<div class="solution">

Dưới đây là cách làm của chúng tôi. Nó có đúng kiểu dạng mẫu mà ta đã áp dụng cho `boxes`.

```scala mdoc:reset:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```
```scala mdoc
def chessboard(count: Int): Image = {
  val blackSquare = Image.square(30) fillColor Color.black
  val redSquare   = Image.square(30) fillColor Color.red
  val base =
    (redSquare   beside blackSquare) above (blackSquare beside redSquare)
  def loop(count: Int): Image =
    count match {
      case 0 => base
      case n =>
        val unit = loop(n-1)
        (unit beside unit) above (unit beside unit)
    }

  loop(count)
}
```
</div>

#### Boxing Clever {-}

Hãy viết lại `boxes`, như dưới đây, sao cho `aBox` chỉ có trong phạm vi của `boxes` và chỉ được tạo nên một lần khi `boxes` được gọi tới.

```scala mdoc:silent
val aBox = Image.square(20).fillColor(Color.royalBlue)

def boxes(count: Int): Image =
  count match {
    case 0 => Image.empty
    case n => aBox.beside(boxes(n-1))
  }
```

<div class="solution">

Ta có thể làm điều này theo hai giai đoạn, đầu tiên là chuyển `aBox` vào trong `boxes`.

```scala mdoc:reset:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```
```scala mdoc:silent
def boxes(count: Int): Image = {
  val aBox = Image.square(20).fillColor(Color.royalBlue)
  count match {
    case 0 => Image.empty
    case n => aBox beside boxes(n-1)
  }
}
```

Sau đó ta có thể dùng một phương thức nội tại để tránh tạo lại `aBox` ở mỗi lượt đệ quy.

```scala mdoc:reset:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```
```scala mdoc:silent
def boxes(count: Int): Image = {
  val aBox = Image.square(20).fillColor(Color.royalBlue)
  def loop(count: Int): Image =
    count match {
      case 0 => Image.empty
      case n => aBox beside loop(n-1)
    }

  loop(count)
}
```
</div>
