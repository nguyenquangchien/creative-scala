## Color

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Ngoài cách bố trí ra, Doodle còn có những toán tử đơn giản để thêm màu sắc cho các hình bạn vẽ. Hãy thử những phương thức mô tả trong [@tbl:pictures:color] để xem chúng tác dụng ra sao.

+-----------------------------+-----------+-------------------------+------------------------------+
| Phương thức                 | Tham số   | Mô tả                   | Ví dụ                        |
+=============================+===========+=========================+==============================+
| `fillColor`                 | `Color`   | Tô hình bằng            | `Image.circle(10)            |
|                             |           | màu đã chọn.            |    .fillColor(Color.red)`    |
+-----------------------------+-----------+-------------------------+------------------------------+
| `strokeColor`               | `Color`   | Vẽ viền hình bằng       | `Image.circle(10)            |
|                             |           | màu đã chọn.            |    .strokeColor(Color.blue)` |
+-----------------------------+-----------+-------------------------+------------------------------+
| `strokeWdith`               | `Double`  | Đặt bề rộng của viền    | `Image.circle(10)            |
|                             |           | hình vẽ.                |    .strokeWidth(3)`          |
+-----------------------------+-----------+-------------------------+------------------------------+
| `noFill`                    | Không     | Xóa màu tô              | `Image.circle(10).noFill`    |
|                             |           | trong hình.             |                              |
+-----------------------------+-----------+-------------------------+------------------------------+
| `noStroke`                  | Không     | Xóa đường viền          | `Image.circle(10).noStroke`  |
|                             |           | của hình.               |                              | 
+-----------------------------+-----------+-------------------------+------------------------------+

: Một vài phương thức vẽ màu cho các hình trong Doodle. {#tbl:pictures:color}

Doodle có nhiều cách để tạo màu sắc.
Cách đơn giản nhất là dùng màu định sẵn trong [CommonColors.scala][common-colors].
Một số màu thông dụng nhất được mô tả trong [@tbl:pictures:colors].

+--------------+-------+------------------------------------------+
| Màu          | Kiểu  | Ví dụ                                    |
+==============+=======+==========================================+
|`Color.red`   |`Color`| `Image.circle(10).fillColor(Color.red)`  |
+--------------+-------+------------------------------------------+
|`Color.blue`  |`Color`| `Image.circle(10).fillColor(Color.blue)` |
+--------------+-------+------------------------------------------+
|`Color.green` |`Color`| `Image.circle(10).fillColor(Color.green)`|
+--------------+-------+------------------------------------------+
|`Color.black` |`Color`| `Image.circle(10).fillColor(Color.black)`|
+--------------+-------+------------------------------------------+
|`Color.white` |`Color`| `Image.circle(10).fillColor(Color.white)`|
+--------------+-------+------------------------------------------+
|`Color.gray`  |`Color`| `Image.circle(10).fillColor(Color.gray)` |
+--------------+-------+------------------------------------------+
|`Color.brown` |`Color`| `Image.circle(10).fillColor(Color.brown)`|
+--------------+-------+------------------------------------------+

: Một số màu định sẵn thông dụng nhất. {#tbl:pictures:colors}

### Bài tập {-}

#### Mắt quỷ {-}

Hãy tạo hình vẽ ở [@fig:pictures:evil-eye], vốn được thiết kế giông như một lá bùa truyền thống tránh khỏi con mắt quỷ. Tôi đã dùng màu `cornflowerBlue` cho lòng đen mắt, và `darkBlue` cho màu bên ngoài, nhưng bạn có thể tự chọn để thử nghiệm!

![Mắt quỷ, cấm vào!](src/pages/pictures/evil-eye.pdf+svg){#fig:pictures:evil-eye}

<div class="solution">
Đây là lá bùa của tôi:

```scala mdoc
Image
  .circle(10)
  .fillColor(Color.black)
  .on(Image.circle(20).fillColor(Color.cornflowerBlue))
  .on(Image.circle(30).fillColor(Color.white))
  .on(Image.circle(50).fillColor(Color.darkBlue))
```
</div>
