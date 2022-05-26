## Một dãy các ô

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Hãy cùng bắt đầu với ví dụ đơn giản, vẽ một hàng gồm các ô như [@fig:recursion:sequential-boxes].

![Năm ô vuông tô màu Royal Blue](./src/pages/recursion/sequential-boxes.pdf+svg){#fig:recursion:sequential-boxes}
 
Để bắt đầu, hãy cùng định nghĩa một ô.

```scala mdoc:silent
val aBox = Image.square(20).fillColor(Color.royalBlue)
```

Khi đó để có một ô trong hàng, chỉ việc 

```scala mdoc:silent
val oneBox = aBox
```

Nếu ta muốn có hai ô sát cạnh nhau, cũng rất dễ dàng.

```scala mdoc:silent
val twoBoxes = aBox.beside(oneBox)
```

Tương tự với ba ô.

```scala mdoc:silent
val threeBoxes = aBox.beside(twoBoxes)
```

Và cứ như vậy muốn tạo bao nhiêu ô cũng được. 

Bạn có thể nghĩ rằng đây là cách bất thường để tạo ra những hình này.
Tại sao không viết thế này luôn chẳng hạn?

```scala mdoc:reset:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
val aBox = Image.square(20).fillColor(Color.royalBlue)
val oneBox = aBox
val twoBoxes = aBox.beside(oneBox)
```
```scala mdoc:silent
val threeBoxes = aBox.beside(aBox).beside(aBox)
```

Hai cách định nghĩa nêu trên tương đương nhau.
Ta chọn cách viết các hình sau dựa trên cơ sở hình đã vẽ trước, để nhấn mạnh cấu trúc mà ta đang xử lý, vốn là công đoạn hình thành nên đệ quy cấu trúc.

Viết ra các hình theo cách này có thể sẽ rất nhàm chán.
Cái mà ta cần là một cách để chỉ bảo cho máy biết số ô ta cần vẽ.
Nói đúng kĩ thuật, ta muốn khái quát những biểu thức nêu trên.
Ở chương trước, ta đã biết rằng các phương thức thì khái quát hoá biểu thức, vì vậy hãy cùng thử viết một phương thức để giải quyết vấn đề này.

Ta hãy bắt đầu bằng cách viết một khung "dàn ý" phương thức để định nghĩa, như thường lệ, những thứ đi vào phương thức và thứ được ước luọng thành.
Trong trường hợp này, ta cấp một biến `Int` là `count`, đó là số ô cần có, và nhận lại một `Image`.

```scala mdoc:silent
def boxes(count: Int): Image =
  ???
```

Bây giờ là phần mới, *đệ quy cấu trúc*.
Ta đã nhận thấy rằng `threeBoxes` nêu trên đã được định nghĩa dựa theo `twoBoxes`, còn `twoBoxes` lại được định nghĩa dựa theo `box`.
Thậm chí, ta còn có thể định nghĩa `box` theo *không* box, như sau:

```scala mdoc:reset:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
val aBox = Image.square(20).fillColor(Color.royalBlue)
```
```scala mdoc:silent
val oneBox = aBox.beside(Image.empty)
```

Ở đây đã sử dụng `Image.empty` để biểu diễn không box.

Hãy hình dung như ta đã viết xong phương thức `boxes`.
Ta có thể nói rằng những đặc tính sau của `boxes` luôn thoả mãn, nếu phương thức này được viết đúng:

- `boxes(0) == Image.empty`
- `boxes(1) == aBox.beside(boxes(0))`
- `boxes(2) == aBox.beside(boxes(1))`
- `boxes(3) == aBox.beside(boxes(2))`

Ba thuộc tính sau cùng đều có chung một dạng.
Ta có thể mô tả tất thảy chúng, và cho trường hợp với `n > 0`, chỉ bằng một thuộc tính duy nhất `boxes(n) == aBox.beside(boxes(n - 1))`.
Bởi vậy ta chỉ còn lại hai thuộc tính sau

- `boxes(0) == Image.empty`
- `boxes(n) == aBox.beside(boxes(n-1))`

Hai thuộc tính này định nghĩa trọn vẹn động thái của `boxes`.
Thực ra ta có thể viết `boxes` bằng cách chuyển đổi những động thái trên thành mã lệnh.

Nội dung đầy đủ của `boxes` là

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

Hãy thử nó và xem bạn được kết quả gì!
Cách viết này chỉ hơi dài hơn các thuộc tính mà ta đã ghi ra ở trên, và là phép đệ quy cấu trúc đầu tiên của ta trên các số tự nhiên.

Đến đây ta có hai câu hỏi cần giải đáp.
Một là, biểu thức `match` (khớp) hoạt động ra sao?
Quan trọng hơn nữa, có nguyên tắc chung nào ta có thể dùng để tự viết các phương thức như thế này không?
Hãy lân lượt trả lời từng câu hỏi một.

### Bài tập: Xếp chồng các ô {-}

Ngay cả trước khi ta đi sâu vào chi tiết biểu thức `match`, bạn cũng có thể chỉnh sửa `boxes` để tạo nên một hình như [@fig:recursion:stacked-boxes].

Đến đây ta cố gắng quen với cú pháp của `match`, do đó thay vì sao chép và dán các `boxes`, hãy tự tay bạn viết lại toàn bộ để tập cho quen.

![Ba ô xếp chồng được tô màu Royal Blue](./src/pages/recursion/sequential-boxes.pdf+svg){#fig:recursion:stacked-boxes}

<div class="solution">
Tất cả những gì bạn cần làm là thay đổi `beside` thành `above` trong `boxes`.

```scala mdoc:silent
def stackedBoxes(count: Int): Image =
  count match {
    case 0 => Image.empty
    case n => aBox.beside(stackedBoxes(n-1))
  }
```
</div>
