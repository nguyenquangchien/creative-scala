## Trừu tượng hoá

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Ở mục trước, ta đã tìm hiểu nhiều về tên. 
Nếu muốn theo phong cách của dân lập trình, ta có thể nói rằng *tên đã khái quát hoá các biểu thức*.
Điều này diễn đạt được bản chất của việc định nghĩa các tên, vậy ta hãy cùng giải mã cách nói này của dân lập trình.

Khái quát hoá nghĩa là lược bỏ những chi tiết không cần đến. 
Chẳng hạn, các số là một cách khái quát hoá.
Số "một" không bao giờ tìm thấy được trong tự nhiên dưới dạng khái niệm thuần tuý. 
Nó luôn là một đối tượng, như một quả táo, hay một cuốn sách Scala sáng tạo.
Khi làm toán, khái niệm các con số giúp ta khái quát hoá tất cả những chi tiết không cần thiết của các sự vật cụ thể mà ta đang đếm, mà chỉ thao tác với bản thân con số thôi.

Tương tự như vậy, một cái tên sẽ đại diện cho một biểu thức.
Một biểu thức cho ta biết cách thiết lập một giá trị.
Nếu giá trị đó có một tên thì ta sẽ không cần biết gì về việc giá trị đó được thiết lập ra sao.
Biểu thức có thể phức tạp tuỳ ý, nhưng ta không cần lưu tâm đến sự phức tạp này nếu ta chỉ dùng đến cái tên.
Đây là ý nghĩa của việc nói rằng cái tên đã khái quát hoá một biểu thức.
Mỗi khi có một biểu thức, ta có thể thay thế một cái tên để chỉ tới cùng giá trị đó.

Khái quát hoá giúp cho mã lệnh dễ đọc và viết hơn.
Hãy làm một ví dụ tao ra một loạt các ô như trên [@fig:programs:sequential-boxes].

![Năm ô vuông tô màu xanh Royal Blue](./src/pages/programs/sequential-boxes.pdf+svg){#fig:programs:sequential-boxes}

Ta có thể viết hẳn ra một biểu thức duy nhất để tạo ra bức tranh.

```scala mdoc:silent
Image.rectangle(40, 40)
     .strokeWidth(5.0)
     .strokeColor(Color.royalBlue.spin(30.degrees))
     .fillColor(Color.royalBlue)
     .beside(
       Image.rectangle(40, 40)
         .strokeWidth(5.0)
         .strokeColor(Color.royalBlue.spin(30.degrees))
         .fillColor(Color.royalBlue)
     ).beside(
        Image.rectangle(40, 40)
          .strokeWidth(5.0)
          .strokeColor(Color.royalBlue.spin(30.degrees))
          .fillColor(Color.royalBlue)
     ).beside(
        Image.rectangle(40, 40)
             .strokeWidth(5.0)
             .strokeColor(Color.royalBlue.spin(30.degrees))
            .fillColor(Color.royalBlue)
     ).beside(
        Image.rectangle(40, 40)
             .strokeWidth(5.0)
             .strokeColor(Color.royalBlue.spin(30.degrees))
             .fillColor(Color.royalBlue)
     )
```

Trong mã lệnh này thấy khó thấy được dạng mẫu đơn giản bên trong. 
Liệu thật sự bạn có thể liếc qua mà phát hiện được rằng tất cả các hình vuông đều như nhau không?
Nếu ta có thể khái quát hoá bằng cách đặt tên cho ô thì mã lệnh sẽ dễ đọc hơn nhiều.

```scala mdoc:silent
val box =
  Image.rectangle(40, 40)
       .strokeWidth(5.0)
       .strokeColor(Color.royalBlue.spin(30.degrees))
       .fillColor(Color.royalBlue)

box.beside(box).beside(box).beside(box).beside(box)
```

Bây giờ ta có thể dễ dàng thấy được rằng ô được tạo nên ra sao, và dễ dàng thấy được bức tranh gồm hình ô lặp lại 5 lần.


### Bài tập {-}

#### Lại là trường bắn {-}

Hãy trở về đích bắn tên mà ta đã tạo ra ở chương trước, xem [@fig:programs:target3].

![Đích bắn tên](./src/pages/programs/target3.pdf+svg){#fig:programs:target3}

Lần trước ta đã tạo nên hình ảnh mà ta chưa biết cách đặt tên cho giá trị, vì vậy ta có thể viết một biểu thức lớn.
Lần này trở lại, hãy đặt tên cho các thành phần của bức tranh để cho người khác dễ hiểu được hình vẽ đã được tạo nên thế nào.
Bạn sẽ phải tự đánh giá để quyết định xem những phần nào cần đặt tên còn phần nào không xứng đáng có tên riêng.

<div class="solution">
Chúng tôi quyết định đặt tên cho bia đích, giá đỡ, và nền đất như ở dưới đây. 
Điều này sẽ giúp làm rõ xem bức tranh cuối cùng được vẽ nên thế nào.
Việc đặt tên nhiều thành phần khác, theo chúng tôi, sẽ không còn giúp hiểu rõ nữa.

```scala mdoc:silent
val coloredTarget =
  (
    Image.circle(10).fillColor(Color.red) on
      Image.circle(20).fillColor(Color.white) on
      Image.circle(30).fillColor(Color.red)
  )

val stand =
  Image.rectangle(6, 20) above Image.rectangle(20, 6).fillColor(Color.brown)

val ground =
  Image.rectangle(80, 25).strokeWidth(0).fillColor(Color.green)

val image = coloredTarget above stand above ground
```
</div>


#### Đường phố {-}

Để thấy được một cách thuyết phục hơn về việc dùng tên, hãy tạo ra một cảnh đường phố như trên [@fig:programs:street].
Bằng cách đặt các thành phần riêng của hình ảnh, bạn có thể tránh được đáng kể việc lặp lại.

![Cảnh đường phố](./src/pages/programs/street.pdf+svg){#fig:programs:street}

<div class="solution">
Sau đây là lời giải của chúng tôi.
Như bạn thấy, bằng cách chia khung cảnh thành những thành phần nhỏ hơn, ta đã có thể viết khá ít mã lệnh.

```scala mdoc:reset:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```
```scala mdoc:silent
val roof = Image.triangle(50, 30) fillColor Color.brown

val frontDoor =
  (Image.rectangle(50, 15) fillColor Color.red) above (
    (Image.rectangle(10, 25) fillColor Color.black) on
    (Image.rectangle(50, 25) fillColor Color.red)
  )

val house = roof above frontDoor

val tree =
  (
    (Image.circle(25) fillColor Color.green) above
    (Image.rectangle(10, 20) fillColor Color.brown)
  )

val streetSegment =
  (
    (Image.rectangle(30, 3) fillColor Color.yellow) beside
    (Image.rectangle(15, 3) fillColor Color.black) above
    (Image.rectangle(45, 7) fillColor Color.black)
  )

val street = streetSegment beside streetSegment beside streetSegment

val houseAndGarden =
  (house beside tree) above street

val image = (
  houseAndGarden beside
  houseAndGarden beside
  houseAndGarden
) strokeWidth 0
```
</div>
