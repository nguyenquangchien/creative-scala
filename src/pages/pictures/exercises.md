## Bài tập

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

### Soạn ra mục tiêu

Hãy tạo một bức vẽ các đường nét thể hiện mục tiêu (bia) bắn tên gồm ba đường tròn đồng tâm như trên [@fig:pictures:target1].

![Bia bắn đơn giản](src/pages/pictures/target1.pdf+svg){#fig:pictures:target1}

Hãy tiến xa hơn và vẽ thêm một cái giá đỡ để dựng bia này trên trường bắn như trên [@fig:pictures:target2].

![Archery target with a stand](src/pages/pictures/target2.pdf+svg){#fig:pictures:target2}

<div class="solution">
Cách làm đơn giản nhất là tạo nên ba hình tròn đồng tâm bằng phương thức `on`:

```scala mdoc:silent
Image
  .circle(20)
  .on(Image.circle(40))
  .on(Image.circle(60))
```

Thêm nữa, ta có thể tạo một giá đỡ bằng hai hình chữ nhật:

```scala mdoc:silent
Image
  .circle(20)
  .on(Image.circle(40))
  .on(Image.circle(60))
  .above(Image.rectangle(6, 20))
  .above(Image.rectangle(20, 6))
```
</div>


### Nhằm thẳng mục tiêu

Hãy tô màu bia bằng hai màu đỏ và trắng, còn giá đỡ màu nâu (nếu được),
và nền cỏ màu xanh. Xem ví dụ [@fig:pictures:target3].

![Bia bắn tên được tô màu](src/pages/pictures/target3.pdf+svg){#fig:pictures:target3}

<div class="solution">
Mẹo ở đây là sử dụng các cặp ngoặc tròn để kiểm soát thứ tự lồng ghép.
Các phương thức `fillColor()`, `strokeColor()`, và `strokeWidth()`
áp dụng đối với một hình ảnh thôi---ta phải đảm bảo rằng hình ảnh đó
có chứa đúng tập hợp các hình ta cần:

```scala mdoc:silent
Image
  .circle(20).fillColor(Color.red)
  .on(Image.circle(40).fillColor(Color.white))
  .on(Image.circle(60).fillColor(Color.red))
  .above(Image.rectangle(6, 20).fillColor(Color.brown))
  .above(Image.rectangle(20, 6).fillColor(Color.brown))
  .above(Image.rectangle(80, 25).noStroke.fillColor(Color.green))
```
</div>
