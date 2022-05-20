## Cú pháp viết phương thức

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Ta đã thấy một ví dụ khai báo phương thức.

```scala mdoc:silent
def boxes(color: Color): Image = {
  val box =
    Image.rectangle(40, 40).
      strokeWidth(5.0).
      strokeColor(color.spin(30.degrees)).
      fillColor(color)

  box beside box beside box beside box beside box
}
```

Hãy dùng mã lệnh này để hiểu cú pháp khai báo một phương thức.
Phần đầu là *từ khoá* `def`.
Từ khoá là một từ đặc biệt để chỉ điều gì đó quan trọng đối với trình biên dịch Scala---trong trường hợp này là ta chuẩn bị khai báo một phương thức.
Ta đã thấy các từ khoá `object` và `val`.

`def` được nối tiếp ngay bởi tên phương thức, trong trường hợp này là `boxes`, theo cách giống như là `val` và `object` được nối tiếp bởi tên mà chúng khai báo.
Cũng như khai báo `val`, khai báo phương thức không phải là một khai báo tầng đỉnh và phải được bọc trong một khai báo `object` (hoặc các khai báo tầng đỉnh khác) khi viết vào trong file.

Tiếp theo ta có các tham số phương thức, định nghĩa trong cặp ngoặc (`()`).
Các tham số phương thức là những phần mà mã lệnh gọi có thể "cài cắm" vào biểu thức mà phương thức đó ước lượng thành.
Khi khai báo tham số phương thức, ta phải cấp cho chúng cả tên lẫn kiểu.
Giữa kiểu và tên có dấu hai chấm (`:`) phân cách.
Trước đây ta chưa từng phải khai báo kiểu.
Đa số các trường hợp, Scala sẽ tìm ra kiểu cho chúng ta, quá trình này gọi là *suy luận kiểu*.
Tuy nhiên, suy luận kiểu không thể suy ra được kiểu các tham số, bởi vậy ta phải cung cấp chúng.

Sau các tham số phương thức là đến kiểu kết quả.
Kiểu kết quả chính là kiểu dữ liệu của giá trị mà phương thức ước lượng thành khi gọi tới phương thức.
Khác với kiểu tham số, Scala có thể suy luận kiểu kết quả; nhưng quy tắc lập trình tốt là viết cả kiểu kết quả và ta sẽ thống nhất như vậy suốt cuốn Scala Sáng tạo.

Sau cùng, biểu thức phần thân của phương thức tính toán giá trị của gọi phương thức.
Phần thân có thể là một biểu thức khối, như `boxes` ở trên, hay chỉ là một biểu thức đơn lẻ.

<div class="callout callout-info">
#### Cú pháp khai báo phương thức {-}

Cú pháp để khai báo một phương thức là 

```scala
def methodName(param1: Param1Type, ...): ResultType =
  bodyExpression
```

trong đó

- `methodName` là tên phương thức;
- các `param1 : Param1Type, ...` đều tuỳ chọn và là một hoặc nhiều cặp tham số cùng kiểu tham số;
- `ResultType` cũng tuỳ chọn và là kiểu kết quả của lời gọi phương thức; và
- `bodyExpression` là biểu thức được ước lượng để cho kết quả của lời gọi phương thức.
</div>


### Bài tập {-}

Hãy cùng luyện tập khai báo phương thức bằng cách viết vài ví dụ đơn giản.

#### Bình phương {-}

Hãy viết một phương thức `square` nhận vào một đối số kiểu `Int` rồi trả lại bình phương kiểu `Int` của đối số này. (Bình phương một số là đem lấy số đó nhân với chính nó.)

<div class="solution">
Lời giải là

```scala mdoc:silent
def square(x: Int): Int =
  x * x
```

Ta có thể thu được lời giải này qua những bước sau.

Ta đã được cho tên phương thức (`square`), kiểu của tham số (`Int`), cũng như kiểu của kết quả (`Int`).
Từ đây ta có thể viết nên một khung của phương thức này 

```scala mdoc:reset:silent
def square(x: Int): Int =
  ???
```

ở đó ta đã chọn `x` là tên tham số. 
Lựa chọn này khá tuỳ ý.
Khi mà không có cái tên ý nghĩa nào thì bạn thường thấy những tên chỉ bằng một chữ cái `x`, `v`, hay `i` được dùng đến.

Tiện thể, đây cũng là mã lệnh hợp lệ.
Hãy nhập nó vào console mà xem!
Sẽ ra sao nếu bạn gọi `square` khi nó được định nghĩa như vậy?

Bây giờ ta cần phải hoàn thiện phần thân.
Ta đã được bảo rằng bình phương là đem nhân một số với chính nó, vì vậy `x * x` chính là cái thế chỗ cho `???`.
Không cần phải bọc biểu thức này trong ngoặc nhọn vì chỉ có một biểu thức trong phần thân.
</div>


#### Chia đôi {-}

Hãy viết phương thức `halve` nhận vào một đối số `Double` rồi trả lại số `Double` bằng một nửa đối số vừa nêu.

<div class="solution">
```scala mdoc:silent
def halve(x: Double): Double =
 x / 2.0
```

Ta có thể theo trình tự như `square` ở trên để luận ra lời giải.
</div>
