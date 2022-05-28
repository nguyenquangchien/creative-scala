## Số tự nhiên 

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
val aBox = Image.square(20).fillColor(Color.royalBlue)
```

Số tự nhiên là các số nguyên lớn hơn hoặc bằng không. Nói các khác, đó là các số 0, 1, 2, 3, ... (Có người lại định nghĩa số tự nhiên bắt đầu từ 1 thay vì 0. Với vấn đề hiện đang xét thì bắt đầu từ 0 hay 1 chẳng hề quan trọng, nhưng ta sẽ coi như chúng bắt đầu từ 0.)

Một trong những thuộc tính của số nguyên là ta có thể định nghĩa chúng theo cách đệ quy. Nghĩa là, có thể định nghĩa chúng theo bản thân chúng. Cách định nghĩa vòng tròn này dường như sẽ dẫn đến vô nghĩa. Để tránh điều này, ta sẽ kèm thêm trong lời định nghĩa một *trường hợp cơ sở* để kết thúc đệ quy. Cụ thể, định nghĩa là:

Một số tự nhiên `n` là

- 0; hoặc
- 1 + `m`, trong đó `m` là số tự nhiên.

Trường hợp 0 là trường hợp cơ sở, còn những trường hợp khác là đệ quy vì nó định nghĩa số tự nhiên `n` theo số tự nhiên `m`. Vì `m` luôn nhỏ hơn `n`, và vì trường hợp cơ sở là số tự nhiên nhỏ nhất có thể, nên định nghĩa này đã xác định mọi số tự nhiên.

Cho trước một số tự nhiên, chẳng hạn, 3, ta có thể phân tách nó bằng định nghĩa nêu trên như sau:

3 = 1 + 2 = 1 + (1 + 1) = 1 + (1 + (1 + 0))

Ta dùng quy tắc đệ quy để khai triển phương trình này đến khi không thể dùng đệ quy được nữa. Khi đó, ta dùng trường hợp cơ sở để kết thúc đệ quy.


## Đệ quy cấu trúc

Bây giờ tới lượt đệ quy cấu trúc. Dạng mẫu đệ quy cấu trúc với số tự nhiên cho ta hai điều:

- một khung dàn ý mã để xử lý bất kì số tự nhiên nào; và 
- sự đảm bảo rằng ta có thể dùng khung dàn ý này để viết *bất kì* tính toán nào đối với số tự nhiên.

Hãy nhớ lại rằng ta đã viết `boxes` như sau

```scala mdoc:silent
def boxes(count: Int): Image =
  count match {
    case 0 => Image.empty
    case n => aBox.beside(boxes(n-1))
  }
```

Khi pháp triển `boxes`, dường như ta đã đụng chạm đến dạng mẫu này. 
Ở đây ta thấy rằng dạng mẫu trực tiếp đi theo định nghĩa các số tự nhiên. 
Hãy nhớ lại rằng lời định nghĩa đệ quy về các số tự nhiên: một số tự nhiên `n` là

- 0; hoặc
- 1 + `m`, trong đó `m` là số tự nhiên.

Dạng mẫu trong biểu thức `match` khớp đúng với lời định nghĩa này. Biểu thức 

```scala
count match {
  case 0 => ???
  case n => ???
}
```

nghĩa là ta đang kiểm tra `count` cho hai trường hợp, trường hợp khi `count` bằng 0, và trường hợp khi `count` là bất kì số tự nhiên `n` nào khác (vốn bằng `1 + m`).

Vế phải của biểu thức `match` nói rằng ta sẽ làm gì trong mỗi trường hợp. Trường hợp với số 0 là `Image.empty`. Trường hợp với số `n` là  `aBox.beside(boxes(n-1))`.

Bây giờ tới điều thực sự quan trọng.
Lưu ý rằng biểu thức ở vế phải đã phản chiếu cấu trúc của số tự nhiên mà ta khớp.
Khi ta khớp trường hợp cơ sở số 0, kết quả của chứng ta là trường hợp cơ sở `Image.empty`. Khi ta khớp trường hợp đệ quy `n` thì cấu trúc vế phải khớp cấu trúc trường hợp đệ quy theo lời định nghĩa về số tự nhiên.
Định nghĩa phát biểu rằng `n` bằng `1 + m`.
Ở vế phải ta thay 1 bởi `aBox`, và thay + bởi `beside`, rồi ta gọi đệ quy `boxes` với `m` (vốn là `n-1`) ở chỗ mà định nghĩa lặp lại.

```scala mdoc:reset:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
val aBox = Image.square(20).fillColor(Color.royalBlue)
```
```scala mdoc:silent
def boxes(count: Int): Image =
  count match {
    case 0 => Image.empty
    case n => aBox.beside(boxes(n-1))
  }
```

Để nhắc lại, vế trái của biểu thức `match` khớp đúng với lời định nghĩa về các số tự nhiên. Vế phải cũng khớp với định nghĩa này nhưng ta thay số tự nhiên bằng hình. Tương đương với số 0 là hình `Image.empty`. Tương đương với `1 + m` là hình `aBox.beside(boxes(m))`.

Dạng mẫu tổng quát này nghiệm đúng với bất kì thứ gì ta cần viết để chuyển đổi từ số tự nhiên qua dạng khác. 
Ta luôn có một biểu thức `match`.
Ta luôn có hai dạng mẫu, tương ứng với các trường hợp cơ sở và đệ quy.
Biểu thức vế phải luôn gồm có trường hợp cơ sở, và trường hợp đệ quy vốn bản thân nó có kết quả thay thế cụ thể cho `1` và `+`, cùng với lời gọi đệ quy tới `n-1`.

<div class="callout callout-info">
#### Structural Recursion over Natural Numbers Pattern {-}

The general pattern for structural recursion over the natural numbers is

```scala
def name(count: Int): Result =
  count match {
    case 0 => resultBase
    case n => resultUnit add name(n-1)
  }
```

where `Result`, `resultBase`, `resultUnit`, and `add` are specific to the problem we're solving.
So to implement a structural recursion over the natural numbers we must

 - recognise the method we're writing has a natural number as it's input;
 - work out the result type; and
 - decide what should be the base, unit, and addition for the result.
</div>

We're now ready to go explore the fun that can be had with this simple but powerful tool.

<div class="callout callout-info">
### Proofs and Programs

If you've studied maths you have probably come across proof by induction.
The general pattern of a proof by induction looks very much like the general pattern of a structural recursion over the natural numbers.
This is no coincidence; there is a deep relationship between the two.
We can view a structural recursion over the natural numbers as exactly a proof by induction.
When we claim the ability to write any transformation on the natural numbers in terms of the structural recursion skeleton, this claim is backed up by the mathematical foundation we're implicitly using.
We can also prove properties of our code by using the connection between the two: any structural recursion is implicitly defining a proof of some property.

This general connection between proofs and programs is known as the *Curry-Howard Isomorphism*.
</div>

### Exercises {-}

#### Three (or More) Stacks {-}

We've seen how to create a horizontal row of boxes. Now write a method `stacks` that takes a natural number as input and creates a vertical stack of boxes.

<div class="solution">
This is a modification of `boxes`, replacing `beside` with `above`.

```scala mdoc:silent
def stacks(count: Int): Image =
  count match {
    case 0 => Image.empty
    case n => aBox.above(boxes(n-1))
  }
```
</div>

#### Alternating Images {-}

We do more with the counter than simply using it in the recursive call. In this exercise we'll choose one `Image` when the counter is odd and a different `Image` when the counter is even. This will give us a row of alternating images as shown in [@fig:recursion:alternating-row].

![A row constructed by alternating between two different images.](./src/pages/recursion/alternating-row.pdf+svg){#fig:recursion:alternating-row}

To do this we need to learn about a new method on `Int`. The *modulo* method, written `%`, returns the remainder of dividing one `Int` by another. Here are some examples.

```scala mdoc
4 % 2
3 % 2
2 % 2
1 % 2
```

We can see that when the first number is even the result is 0; otherwise it is 1. So we need to check is the result is 0 and act accordingly. There are a few ways to do this. Here's one example

```scala mdoc
(4 % 2 == 0) match {
  case true  => "It's even!"
  case false => "It's odd!"
}
```

Here we match against the result of the comparison `(4 % 2 == 0)`. The type of this expression is `Boolean`, which has two possible values (`true` and `false`).

For `Booleans` there is special syntax that is more compact than `match`: an `if` expression. Here's the same code rewritten using `if`.

```scala mdoc
if(4 % 2 == 0) "It's even!"
else "It's odd!"
```

Use whichever you are more comfortable with!

That's all the background we need. Now we can write the method we're interested in. Here's the skeleton:

```scala mdoc:silent
def alternatingRow(count: Int): Image =
  ???
```

Implement the method. It's up to you what you choose for the two images used in the output.

<div class="solution">
Here's my solution. I used an `if` expression because it's a bit shorter than matching on the `Boolean`. Otherwise it's the same structural recursion pattern as before.

```scala mdoc:reset:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```
```scala mdoc:silent
val star = Image
  .star(5, 30, 15, 45.degrees)
  .strokeColor(Color.teal)
  .on(Image.star(5, 12, 7, 45.degrees).strokeColor(Color.royalBlue))
  .strokeWidth(5.0)

val circle = Image
  .circle(60)
  .strokeColor(Color.midnightBlue)
  .on(Image.circle(24).strokeColor(Color.plum))
  .strokeWidth(5.0)

def alternatingRow(count: Int): Image = {
  count match {
    case 0 => Image.empty
    case n =>
      if(n % 2 == 0) star.beside(alternatingRow(n-1))
      else circle.beside(alternatingRow(n-1))
  }
}
```
</div>


#### Getting Creative {-}

We can use the counter to modify the image in other ways. For example we can make the color, size, or any othe property of an image depend on the counter. I have made an example in [@fig:recursion:fun-row], but come up with your own ideas. Implement a method

```scala mdoc
def funRow(count: Int): Image =
  ???
```

that generates such an image.

![A row constructed by making size and color depend on the counter.](./src/pages/recursion/fun-row.pdf+svg){#fig:recursion:fun-row}

<div class="solution">
Here's my solution. I made the size of the star and its color depend on the counter.

```scala mdoc:reset:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```
```scala mdoc:silent
def funRow(count: Int): Image = {
  count match {
    case 0 => Image.empty
    case n =>
      Image
        .star(7, (10 * n), (7 * n), 45.degrees)
        .strokeColor(Color.azure.spin((5 * n).degrees))
        .strokeWidth(7.0)
        .beside(funRow(n - 1))
  }
}
```
</div>


#### Cross {-}

Our final exercise is to create a method `cross` that will generate cross images. [@fig:recursion:cross] shows four cross images, which correspond to calling the method `cross` with `0` to `3`.

The method skeleton is

```scala mdoc
def cross(count: Int): Image =
  ???
```

![Crosses generated by `count` from 0 to 3.](./src/pages/recursion/cross.pdf+svg){#fig:recursion:cross}

People often find this exercise harder than the preceding ones, so we'll make the process very explicit here.

Firstly, what pattern will we use to fill in the body of `cross`? Write out the pattern.

<div class="solution">
It's structural recursion over the natural numbers. You should end up with something like

```scala
def cross(count: Int): Image =
  count match {
    case 0 => <resultBase>
    case n => <resultUnit> <add> cross(n-1)
  }
```
</div>

Now we've identified the pattern we're using, we need to fill in the problem specific parts:

 - the base case; and
 - the unit and addition operators.

Hint: use [@fig:recursion:cross] to identify the elements above.

<div class="solution">
From the picture we can work out that the base case is the hexagon in red.

Successive elements in the picture add circles to the top, bottom, left, and right of the image. So our unit is a circle, but the addition operator is not a simple `beside` or `above` like we've seen before but `unit.beside(unit.above(cross(n-1)).above(unit)).beside(unit)`.
</div>

Now finish the implementation of `cross`.

<div class="solution">
Here's what we wrote.

```scala mdoc:reset:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```
```scala mdoc
  def cross(count: Int): Image = {
    count match {
      case 0 =>
        Image.regularPolygon(6, 10, 0.degrees)
          .strokeColor(Color.deepSkyBlue.spin(-180.degrees))
          .strokeWidth(5.0)
      case n =>
        val circle = Image
          .circle(20)
          .strokeColor(Color.deepSkyBlue)
          .on(Image.circle(15).strokeColor(Color.deepSkyBlue.spin(-15.degrees)))
          .on(Image.circle(10).strokeColor(Color.deepSkyBlue.spin(-30.degrees)))
          .strokeWidth(5.0)
        circle.beside(circle.above(cross(n - 1)).above(circle)).beside(circle)
    }
  }
```
</div>
