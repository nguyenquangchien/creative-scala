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

[@fig:pictures:color-wheel] shows how colors vary as we change hue and lightness, and [@fig:pictures:saturation] shows the effect of changing saturation.

![A color wheel showing changes in hue (rotations) and lightness (distance from the center) with saturation fixed at 1.](src/pages/pictures/color-wheel.pdf+svg){#fig:pictures:color-wheel}

![A gradient showing how changing saturation effects color, with hue and lightness held constant. Saturation is zero on the left and one on the right.](src/pages/pictures/saturation.pdf+svg){#fig:pictures:saturation}

We can construct a color in the HSL representation using the `Color.hsl` method. This method takes as parameters the hue, saturation, and lightness. The hue is an `Angle`. We can convert a `Double` to an `Angle` using the `degrees` (or `radians`) methods.

```scala mdoc
0.degrees
180.degrees
3.14.radians
```

Saturation and lightness are both `Doubles` that should be between 0.0 and 1.0. Values outside this range will be converted to the closest number within the range. 

We can now create colors using the HSL representation.

```scala mdoc:silent
Color.hsl(0.degrees, 0.8, 0.6) // A pastel red
```

To view this color we can render it in a picture. See [@fig:pictures:triangle-pastel-red] for an example.

![Rendering pastel red in a triangle](./src/pages/pictures/triangle-pastel-red.pdf+svg){#fig:pictures:triangle-pastel-red}


### Manipulating Colors

The effectiveness of a composition often depends as much on the relationships between colors as the actual colors used. Colors have several methods that allow us to create a new color from an existing one. The most commonly used ones are:

- `spin`, which rotates the hue by an `Angle`;
- `saturate` and `desaturate`, which respectively add and subtract a `Normalised` value from the color; and
- `lighten` and `darken`, which respectively add and subtract a `Normalised` value from the lightness.

For example,

```scala mdoc:silent
Image.circle(100)
     .fillColor(Color.red)
     .beside(Image.circle(100).fillColor(Color.red.spin(15.degrees)))
     .beside(Image.circle(100).fillColor(Color.red.spin(30.degrees)))
     .strokeWidth(5.0)
```

produces [@fig:pictures:three-circles-spin].

![Three circles, starting with Color.red and spinning by 15 degrees for each successive circle](./src/pages/pictures/three-circles-spin.pdf+svg){#fig:pictures:three-circles-spin}

Here's a similar example, this time manipulating saturation and lightness, shown in [@fig:pictures:saturate-and-lighten].

```scala mdoc:silent
Image.circle(40)
   .fillColor(Color.red.darken(0.2.normalized))
   .beside(Image.circle(40).fillColor(Color.red))
   .beside(Image.circle(40).fillColor((Color.red.lighten(0.2.normalized))))
   .above(Image.rectangle(40, 40).fillColor(Color.red.desaturate(0.6.normalized))
               .beside(Image.rectangle(40,40).fillColor(Color.red.desaturate(0.3.normalized)))
               .beside(Image.rectangle(40,40).fillColor(Color.red)))
```

![The top three circles show the effect of changing lightness, and the bottom three squares show the effect of changing saturation.](./src/pages/pictures/saturate-and-lighten.pdf+svg){#fig:pictures:saturate-and-lighten}

[^byte]: A byte is a number with 256 possible values, which takes 8 bits within a computer to represent. A signed byte has integer values from -128 to 127, while an unsigned byte ranges from 0 to 255.


### Độ trong suốt

We can also add a degree of transparency to our colors, by adding an *alpha* value. An alpha value of 0.0 indicates a completely transparent color, while a color with an alpha of 1.0 is completely opaque. The methods `Color.rgba` and `Color.hsla` have a fourth parameter that is a `Normalized` alpha value. We can also create a new color with a different transparency by using the `alpha` method on a color. Here's an example, shown in [@fig:pictures:rgb-alpha].

```scala mdoc:silent
Image.circle(40)
     .fillColor(Color.red.alpha(0.5.normalized))
     .beside(Image.circle(40).fillColor(Color.blue.alpha(0.5.normalized)))
     .on(Image.circle(40).fillColor(Color.green.alpha(0.5.normalized)))
```

![Circles with alpha of 0.5 showing transparency](./src/pages/pictures/rgb-alpha.pdf+svg){#fig:pictures:rgb-alpha}


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
