## Bông hoa và những đường vẽ khác

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Ở mục trước ta đã thấy rằng việc phương thức chấp nhận hàm là tham số thật là hữu ích. Ở mục này ta sẽ thấy các phương thức trả lại hàm cũng rất hữu ích.

Ta đã thấy tất cả những bước cơ bản cần để vẽ nên các bông hoa. Bây giờ ta chỉ cần biết nét cong để tạo nên hình bông hoa! Hình mà tôi dùng có tên là [đường cong hoa hồng][rose-curve]. Một ví dụ được cho thấy trên hình [@fig:hof:rose7]. 

![Ví dụ đường cong hoa hồng.](src/pages/hof/rose7.pdf+svg){#fig:hof:rose7}

Mã lệnh cho đường cong tham số cho ta hình đó như sau.

```scala mdoc:silent
// Phương trình tham số vẽ hoa hồng với k = 7
val rose7 = (angle: Angle) =>
  Point((angle * 7).cos * 200, angle)
```

Có thể bạn sẽ thắc mắc tại sao tôi đặt tên hàm này là `rose7`. Đó là vì ta có thể thay đổi hình dáng bằng cách sửa số `7` thành một số khác. Ta có thể tạo một phương thức hoặc hàm cho phép ta truyền giá trị của tham số này và hàm sẽ trả lại một hình vẽ hoa hồng cụ thể. Dưới đây là mã lệnh thực hiện ý tưởng này.

```scala mdoc:silent
def rose(k: Int): Angle => Point =
  (angle: Angle) => Point((angle * k).cos * 200, angle)
```

Phương thức `rose` mô tả một họ đường cong. Chúng có dạng tương tự nhau, và ta tạo nên từng cá thể bằng cách chọn riêng một giá trị cho tham số `k`. Trong [@fig:hof:rose] chúng tôi đã cho thấy nhiều hình bông hoa khác, lần này với `k` lần lượt bằng 5, 8, và 9.

![Ví dụ các hình hoa hồng với tham số k chọn bằng 5, 8, hoặc 9.](src/pages/hof/rose.pdf+svg){#fig:hof:rose}

Bây giờ hãy cùng xem một số hình thú vị hơn. Ở [@fig:hof:lissajous] chúng tôi cho thấy các ví dụ một họ các đường nét có tên là [đường cong Lissajous][lissajous].

![Ví dụ các đường cong Lissajous, với các tham số a và b chọn bằng 1, 2, hoặc 3.](src/pages/hof/lissajous.pdf+svg){#fig:hof:lissajous}

Mã lệnh để vẽ hình là

```scala
def lissajous(a: Int, b: Int, offset: Angle): Angle => Point =
  (angle: Angle) =>
    Point(100 * ((angle * a) + offset).sin, 100 * (angle * b).sin)
```

Các ví dụ trong [@fig:hof:lissajous] đã dùng giá trị `a` và `b` bằng 1, 2, hoặc 3, và `offset` đặt bằng 90 độ.

Có vô số các hàm mà ta có thể dùng để tạo nên các đường nét thú vị. Hãy cùng xem một ví dụ nữa, lần này là đường có tên gọi [epicycloid][epicycloid]. Một epicycloid được vẽ nên khi ta đi theo một điểm trên một vòng tròn mà vòng tròn này quay quanh vòng tròn khác. Ta có thể xếp chồng vòng tròn lên trên vòng tròn khác, và thay đổi tốc độ quay của chúng, để tạo nên nhiều đường nét khác nhau. Chẳng hạn ta sẽ cố định số vòng tròn cùng bán kính của chúng nhưng cho phép tốc độ quay của chúng biến đổi. Dưới đây là mã lệnh:

```scala
def epicycloid(a: Int, b: Int, c: Int): Angle => Point =
  (angle: Angle) =>
    (Point(75, angle * a).toVec + Point(32, angle * b).toVec + Point(15, angle * c).toVec).toPoint
```

Bạn có thể nhận thấy rằng mã lệnh quy đổi từ điểm thành vectơ và rồi quy đổi ngược lại. Đây chỉ là một chi tiết kĩ thuật (ta không thể cộng các điểm nhưng có thể cộng véctơ) mà không quá quan trọng nếu bạn không thạo tính với vectơ.

Ở [@fig:hof:epicycloid] ta thấy ba ví dụ tạo ra bằng cách chọn các tham số a, b, c lần lượt là (1, 6, 14), (7, 13, 25), và (1, 7, -21).

![Ví dụ các đường epicycloid, với các tham số chọn bằng (1, 6, 14), (7, 13, 25), và (1, 7 -21).](src/pages/hof/epicycloid.pdf+svg){#fig:hof:epicycloid}


#### Bài tập {-}

Bây giờ ta có nhiều công cụ để nghịch thử rồi. Nhiệm vụ của bạn lúc này chỉ là sử dụng vài ý tưởng như đã thấy để vẽ nên một hình ảnh bạn thích. Để hứng thú hơn bạn có thể dùng lại hình ảnh từ đầu chương, nhưng đừng quá rập khuôn nếu bạn đã nghĩ ra một ý tưởng khác để tìm hiểu.


[lissajous]: https://en.wikipedia.org/wiki/Lissajous_curve
[epicycloid]: https://en.wikipedia.org/wiki/Epicycloid
[rose-curve]: https://en.wikipedia.org/wiki/Rose_(mathematics)
