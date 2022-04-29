## Tạo ra màu sắc

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Ta đã thấy cách dùng những màu định sẵn cho các hình vẽ rồi. Thế còn tạo riêng ra các màu mới? Trong mục này ta sẽ thấy cách tự tạo màu, và biến đổi các màu sẵn có thành các màu mới.

### Các màu RGB

Máy tính làm việc với các màu được định nghĩa bằng cách trộn lẫn lượng sắc đỏ, sắc lục và sắc lam. Mô hình "RGB" này là một [mô hình cộng tính][additive-model] với màu sắc. Điều đó nghĩa là cộng thêm các sắc tố vào sẽ làm cho màu tổng hợp tiến gần tới màu trắng. Như vậy khác hẳn với sơn màu, đó là mô hình trừ; nghĩa là cứ thêm màu sơn vào sẽ tổng hơp tiến gần màu đen. Mỗi sắc tố đỏ, lục, và lam có thể nhận giá trị từ 0 đến 255. Nếu cả 3 thành phần đều đặt trị số cực đại bằng 255 thì ta được màu trắng. Nếu tất cả sắc tố bằng 0 thì ta được màu đen.

Ta có thể tự tạo ra những màu RGB bằng phương thức `rgb` của đối tượng `Color`. Phương thức này nhận vào ba tham số: các sắc tố đỏ, lục và lam. Đó là những số từ 0 đến 255, gọi là `UnsignedByte`[^byte]. Không có biểu thức nguyên văn nào cho `UnsignedByte` như đã từng có với `Int`, bởi vậy ta phải quy đổi từ `Int` sang `UnsignedByte`. Có thể làm điều này bàng phương thức `uByte`. Một số `Int` có thể nhận nhiều giá trị hơn là một `UnsignedByte`. Bởi vậy, nếu con số quá nhỏ hoặc quá lớn để có thể biểu diễn bằng một một `UnsignedByte` thì nó sẽ được quy đổi thành giá trị sát nhất trong khoảng từ 0 đến 255. Những ví dụ dưới đây minh họa cho phép quy đổi.

```scala mdoc
0.uByte.get
255.uByte.get
128.uByte.get
-100.uByte.get // Quá nhỏ, quy đổi thành 0
1000.uByte.get // Quá lớn, quy đổi thành 255
```

(Lưu ý rằng `UnsignedByte` là một đặc điểm của Doodle. Nó không được cung cấp bởi Scala.)

Bây giờ khi đã biết cách lập nên `UnsignedBytes`, ta có thể tạo các màu RGB rồi.

```scala mdoc:silent
Color.rgb(255.uByte, 255.uByte, 255.uByte) // White, trắng
Color.rgb(0.uByte, 0.uByte, 0.uByte) // Black, đen
Color.rgb(255.uByte, 0.uByte, 0.uByte) // Red, đỏ
```

### Các màu HSL

Cách biểu diễn màu RGB không dễ dùng lắm. Định dạng HSL (viêt tắt từ hue-saturation-lightness, sắc độ-bão hòa-độ sáng) thì gàn gũi hơn với cách mà ta nhìn nhận các màu. Theo cách biểu diễn này, một màu gồm có:

- *sắc độ*, là góc từ 0 đến 360 độ quanh bánh xe màu.
- *độ bão hòa*, là một số từ 0 đến 1, cho ta cường độ của màu từ một màu xám xỉn tới một màu thuần khiết; và 
- *độ sáng* là một số từ 0 đến 1, cho màu đó một độ sáng từ đen tuyền đến trắng tinh.

[@fig:pictures:color-wheel] cho thấy màu sắc thay đổi ra sao khi thay chỉnh sắc độ và độ sáng, và [@fig:pictures:saturation] cho thấy ảnh hưởng từ sự thay đổi độ bão hòa.

![Một bánh xe màu ch tháy những thay đổi về sắc độ (quay bánh) và độ sáng (gần hay xa tâm) với độ bão hòa cố định bằng 1.](src/pages/pictures/color-wheel.pdf+svg){#fig:pictures:color-wheel}

![Một dốc màu (gradient) cho thấy việc thay đổi độ bão hòa ảnh hưởng thế nào đến màu sắc, khi giữ nguyên sắc độ và độ sáng. Độ bão hòa bằng 0 ở phía trái và bằng 1 ở phía phải.](src/pages/pictures/saturation.pdf+svg){#fig:pictures:saturation}

Ta có thể lập nên một màu biểu diễn theo cách HSL bằng phương thức `Color.hsl`. Phương thức này nhận các tham số là sắc độ, độ bão hòa và độ sáng. Sắc độ là dữ liệu kiểu góc `Angle`. Ta có thể quy đổi từ `Double` sang `Angle` bằng các phương thức `degrees` (hay `radians`).

```scala mdoc
0.degrees
180.degrees
3.14.radians
```

Cả độ bão hòa lẫn độ sáng đều là `Doubles` và phải có giá trị từ 0.0 tới 1.0. Các giá trị rơi ra ngoài khoảng này sẽ được quy đổi về trị số sát nhất trong khoảng đó.

Bây giờ ta có thể tạo các màu bằng cách biểu diễn HSL.

```scala mdoc:silent
Color.hsl(0.degrees, 0.8, 0.6) // Một màu đỏ pastel
```

Để xem được màu này ta có thể vẽ nó lên một bức tranh. Một ví dụ là [@fig:pictures:triangle-pastel-red].

![Vẽ màu đỏ pastel lên một hình tam giác](./src/pages/pictures/triangle-pastel-red.pdf+svg){#fig:pictures:triangle-pastel-red}


### Thao tác với màu sắc

Mức độ hiệu quả của một cách phối màu thường phụ thuộc vào không chỉ những màu được chọn mà còn cả mối liên hệ giữa chúng nữa. Các màu có vài phương thức cho phép ta tạo ra màu mới từ mầu sẵn có. Những phương thức thông dụng nhất là:

- `spin`, để quay sắc độ một góc bằng `Angle`;
- `saturate` và `desaturate`, lần lượt cộng hoặc trừ một giá trị được chuẩn hóa vào màu hiện có; và
- `lighten` và `darken`, lần lượt cộng hoặc trừ một giá trị được chuẩn hóa vào độ sáng.

Chẳng hạn,

```scala mdoc:silent
Image.circle(100)
     .fillColor(Color.red)
     .beside(Image.circle(100).fillColor(Color.red.spin(15.degrees)))
     .beside(Image.circle(100).fillColor(Color.red.spin(30.degrees)))
     .strokeWidth(5.0)
```

cho ta [@fig:pictures:three-circles-spin].

![Ba hình tròn, bắt đầu với Color.red và quay góc 15 độ ở từng hình kế tiếp](./src/pages/pictures/three-circles-spin.pdf+svg){#fig:pictures:three-circles-spin}

Sau đây là một ví dụ tương tự, lần này thao tác với độ bão hòa và độ sáng, cho thấy ở hình [@fig:pictures:saturate-and-lighten].

```scala mdoc:silent
Image.circle(40)
   .fillColor(Color.red.darken(0.2.normalized))
   .beside(Image.circle(40).fillColor(Color.red))
   .beside(Image.circle(40).fillColor((Color.red.lighten(0.2.normalized))))
   .above(Image.rectangle(40, 40).fillColor(Color.red.desaturate(0.6.normalized))
               .beside(Image.rectangle(40,40).fillColor(Color.red.desaturate(0.3.normalized)))
               .beside(Image.rectangle(40,40).fillColor(Color.red)))
```

![Ba hình tròn trên cùng cho thấy hiệu ứng thay đổi độ sáng, còn ba hình vuông dưới cùng cho thấy hiệu ứng thay đổi độ bão hòa.](./src/pages/pictures/saturate-and-lighten.pdf+svg){#fig:pictures:saturate-and-lighten}

[^byte]: Byte là một số có thể nhận một trong 256 giá trị; byte chiếm 8 bit để biểu diễn nó trong máy tính. Một byte có dấu nhận các giá trị số nguyên từ -128 tới 127, còn byte không dấu chạy từ 0 đến 255.


### Độ trong suốt

Ta cũng có thể thêm một chút độ trong suốt vào các màu sắc, bằng cách thêm một giá trị *alpha*. Giá trị alpha bằng 0.0 biểu thị một màu trong suốt, còn màu với alpha bằng 1.0 thì hoàn toàn đục. Các phương thức `Color.rgba` và `Color.hsla` có một tham số thứ tư là một trị số alpha được chuẩn hóa. Ta cũng có thể tạo một màu mới với độ trong suốt khác bằng cách dùng phương thức `alpha` trên một màu. Dưới đây là một ví dụ, cho kết quả như [@fig:pictures:rgb-alpha].

```scala mdoc:silent
Image.circle(40)
     .fillColor(Color.red.alpha(0.5.normalized))
     .beside(Image.circle(40).fillColor(Color.blue.alpha(0.5.normalized)))
     .on(Image.circle(40).fillColor(Color.green.alpha(0.5.normalized)))
```

![Các hình tròn với alpha bằng 0.5 cho thấy mức độ trong suốt](./src/pages/pictures/rgb-alpha.pdf+svg){#fig:pictures:rgb-alpha}


### Bài tập {-}

#### Các tam giác tương tự {-}

Hãy tạo nên ba hình tam giác, được sắp đặt bên trong một hình tam giác, với màu sắc tương tự. Nói màu sắc tương tự nghĩa là chúng giống nhau về sắc độ. Hãy xem một ví dụ (khá kĩ lưỡng) ở [@fig:pictures:analogous-triangles].

![Các tam giác tương tự. Màu sắc được chọn là các biến thể của `darkSlateBlue`](./src/pages/pictures/complementary-triangles.pdf+svg){#fig:pictures:analogous-triangles}

<div class="solution">
Những kiểu ví dụ này đang trở nên ngày một dài dòng và khó viết từ console. Ta sẽ tìm cách khắc phục điều này trong bài sau.

```scala mdoc
Image.triangle(40, 40)
  .strokeWidth(6.0)
  .strokeColor(Color.darkSlateBlue)
  .fillColor(Color.darkSlateBlue
               .lighten(0.3.normalized)
               .saturate(0.2.normalized)
               .spin(10.degrees))
  .above(Image.triangle(40, 40)
           .strokeWidth(6.0)
           .strokeColor(Color.darkSlateBlue.spin(-30.degrees))
           .fillColor(Color.darkSlateBlue
                        .lighten(0.3.normalized)
                        .saturate(0.2.normalized)
                        .spin(-20.degrees))
           .beside(Image.triangle(40, 40)
                     .strokeWidth(6.0)
                     .strokeColor(Color.darkSlateBlue.spin(30.degrees))
                     .fillColor(Color.darkSlateBlue
                                  .lighten(0.3.normalized)
                                  .saturate(0.2.normalized)
                                  .spin(40.degrees))))
```
</div>
