## Image (Hình)

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Ta hãy bắt đầu bằng những hình đơn giản, lập trình từ dòng lệnh console như đã làm trước đây.

```scala mdoc
Image.circle(10)
```

Điều gì xảy ra ở đây vậy? `Image` là một đối tượng còn `circle` là phương thức trên đối tượng đó. Ta truyền tới `circle`  một tham số, `10` nhằm cho biết đường kính của hình tròn mà ta vẽ. Lưu ý kiểu của kết quả---một `Image` (hình).

```scala mdoc
Image.circle(10)
```

Ta vẽ hình tròn bằng cách gọi phương thức `draw`.

```scala
Image.circle(10).draw()
```

Một cửa sổ sẽ xuất hiện như cho thấy trên [@fig:pictures:circle].

![Một hình tròn](src/pages/pictures/circle.pdf+svg){#fig:pictures:circle}

Doodle hỗ trợ một loạt các hình "cơ bản": tròn, chữ nhật, và tam giác. Hãy thử vẽ một hình chữ nhật.

```scala
Image.rectangle(100, 50).draw()
```

Kết quả được cho thấy ở [@fig:pictures:rectangle].

![Một hình chữ nhật](src/pages/pictures/rectangle.pdf+svg){#fig:pictures:rectangle}

Cuối cùng, hãy thử một hình tam giác, mà kết quả được cho thấy ở [@fig:pictures:triangle].


```scala
Image.triangle(60, 40).draw()
```

![Một hình tam giác](src/pages/pictures/triangle.pdf+svg){#fig:pictures:triangle}

### Bài tập {-}

#### Tôi đi vòng tròn {-}

Hãy tạo các hình tròn rộng 1, 10, và 100 đơn vị. Bây giờ hãy vẽ chúng lên!
Create circles that are 1, 10, and 100 units wide. Now draw them!

<div class="solution">
Ở bài tập này, chúng ta kiểm tra xem Doodle đã được cài đặt để hoạt động bình thường chưa, đồng thời làm quen với thư viện này. Một trong những điểm quan trọng ở Doodle là sự phân biệt giữa *định nghĩa một hình* với *vẽ hình đó*. Ta sẽ nói thêm về điều này xuyên suốt cuốn sách.

Ta có thể tạo nên các hình tròn với mã lệnh dưới đây:

```scala mdoc:silent
Image.circle(1)
Image.circle(10)
Image.circle(100)
```

Ta có thể vẽ nên các hình tròn bằng cách gọi phương thức `draw` lên mỗi hình tròn.

```scala
Image.circle(1).draw()
Image.circle(10).draw()
Image.circle(100).draw()
```
</div>


#### Kiểu của hình nghệ thuật {-}

Kiểu dữ liệu của một hình tròn, hình chữ nhật, hình tam giác là gì? 

<div class="solution">
Chúng đều có kiểu `Image`, như ta thấy trên dòng lệnh console.

```scala
:type Image.circle(10)
// doodle.core.Image
:type Image.rectangle(10, 10)
// doodle.core.Image
:type Image.triangle(10, 10)
// doodle.core.Image
```
</div>

#### Không kiểu bản vẽ nghệ thuật {-}

Kiểu dữ liệu của *bản vẽ* một hình là gì? Điều này nghĩa là sao?

<div class="solution">
Một lần nữa, ta có thể đặt câu hỏi này cho console.

```scala
:type Image.circle(10).draw()
// Unit
```

Ta thấy rằng kiểu của bản vẽ một hình là `Unit`. `Unit` là kiểu của một biểu thức trong đó không có giá trị nào hay ho để trả lại cả. Đây là trường hợp cho `draw`; ta gọi nó vì ta muốn có thứ gì đó xuất hiện trên màn hình, chứ không vì ta phải dùng đến giá trị mà nó trả lại. Chỉ có một giá trị duy nhất thuộc kiểu `Unit`. Giá trị này cũng có tên gọi là unit, với biểu thức nguyên văn được viết là `()`

Bạn sẽ nhận thấy rằng theo mặc định thì console sẽ không in ra giá trị unit.

```scala
()
```

Ta có thể hỏi console về kiểu dữ liệu để thấy được nó thực sự là unit trong trường hợp này.

```scala
:type ()
// Unit
```
</div>
