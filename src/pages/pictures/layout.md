## Bố trí

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Ta đã thấy cách tạo nên những hình cơ bản. Ta có thể kết hợp chúng lại bằng những phương thức bố trí khác nhau để tạo nên những hình phức tạp hơn. Hãy thử đoạn mã lệnh sau---bạn sẽ thấy một hình tròn và một hình chữ nhật hiện ra cạnh nhau, như ở [@fig:picture:circle-rect].

```scala
(Image.circle(10).beside(Image.rectangle(10, 20))).draw()
```

![Một hình tròn bên cạnh hình chữ nhật](src/pages/pictures/circle-beside-rectangle.pdf+svg){#fig:picture:circle-rect}

`Image` có chứa vài phương thức bố trí để kết hợp các hình. Chúng được mô tả trong [@tbl:pictures:layout]. Hãy thử xem chúng làm được việc gì.

+---------------+-----------+----------------------------+------------------------------+
| Phương thức   | Tham số   | Mô tả                      | Ví dụ                        |
+===============+===========+============================+==============================+
| `beside`      |`Image`    | Đặt các hình cạnh nhau     | `Image.circle(10)            |
|               |           | theo hướng ngang           |    .beside(Image.circle(10))`|
+---------------+-----------+----------------------------+------------------------------+
| `above`       |`Image`    | Đặt các hình cạnh nhau     | `Image.circle(10)            |
|               |           | theo hướng đứng            |    .above(Image.circle(10))` |
+---------------+-----------+----------------------------+------------------------------+
| `below`       |`Image`    | Đặt các hình cạnh nhau     | `Image.circle(10)            |
|               |           | theo hướng đứng            |    .below(Image.circle(10))` |
+---------------+-----------+----------------------------+------------------------------+
| `on`          |`Image`    | Đặt các hình chồng lên nhau| `Image.circle(10)            |
|               |           | và cùng căn giữa           |    .on(Image.circle(10))`    |
+---------------+-----------+----------------------------+------------------------------+
| `under`       |`Image`    | Đặt các hình chồng lên nhau| `Image.circle(10)            |
|               |           | và cùng căn giữa           |    .under(Image.circle(10))` |
+---------------+-----------+----------------------------+------------------------------+

: Các phương thức bố trí có sẵn trong Doodle {#tbl:pictures:layout}

### Bài tập {-}

#### Bề rộng của một hình tròn {-}

Hãy tạo nên hình [@fig:picture:width-of-a-circle] sử dụng các phương thức bố trí và những hình cơ bản mà ta đã đề cập tới cho đến giờ.

![Bề rộng của một hình tròn](src/pages/pictures/width-of-a-circle.pdf+svg){#fig:picture:width-of-a-circle}

<div class="solution">
Đó là ba hình tròn nhỏ đặt chồng lên trên một hình tròn lớn, và ta chỉ cần thực hiện như đoạn mã lệnh sau.

```scala mdoc
(Image
   .circle(20)
   .beside(Image.circle(20))
   .beside(Image.circle(20))).on(Image.circle(60))
```
</div>
