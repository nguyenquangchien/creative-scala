## Hàm

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Về cơ bản, hàm là một phương thức, nhưng ta có thể dùng hàm như một giá trị thuộc lớp hạng nhất:

- ta có thể truyền hàm như một đối số hay tham số vào trong một phương thức hoặc hàm;
- ta có thể trả lại hàm từ bên trong một phương thức hoặc hàm; và 
- ta có thể đặt tên cho nó bằng `val`.

Sau đây là một ví dụ mà ta đặt tên `add42` cho một hàm làm nhiệm vụ cộng 42 vào giá trị đầu vào.

```scala mdoc
val add42 = (x: Int) => x + 42
```

Ta có thể gọi hàm này như thể ta gọi một phương thức.

```scala mdoc
add42(0)
```

Đây là một ví dụ về một nguyên văn hàm. Ta hãy xem xét chúng ngay sau đây.


### Nguyên mẫu hàm

Ta vừa thấy một ví dụ về nguyên văn hàm, đó là 

```scala mdoc
(x: Int) => x + 42
```

Cú pháp chung là dạng mở rộng từ ví dụ nói trên.


<div class="callout callout-info">
#### Cú pháp nguyên văn hàm {-}

Cú pháp khai báo một nguyên văn hàm như sau 

```scala
(parameter: type, ...) => expression
```

trong đó
- các tham số `parameter` (có thể có hoặc không) là những tên đặt cho các tham số hàm;
- các kiểu `type` là kiểu của những tham số hàm; và 
- biểu thức `expression` quyết định kết quả của hàm này.

Cặp ngoặc tròn bọc quanh tham số có thể bỏ qua không dùng nếu như hàm chỉ có một tham số.
</div>



### Kiểu của hàm

Để truyền một hàm tới các tham số, ta cần biết cách viết ra kiểu của chúng (vì khi khai báo một tham số, ta phải khai báo kiểu của nó).

Ta viết kiểu một hàm như `(A, B) => C` trong đó `A` và `B` là các kiểu tham số và `C` là kiểu kết quả.
Cũng dạng mẫu này đã khái quát hoá từ các hàm không có tham số thành một lượng bất kì các tham số.

Đây là một ví dụ. Ta phải tạo một phương thức để chấp nhận một hàm, và hàm đó từ `Int` tới `Int`. Ta viết kiểu này là `Int => Int` hay `(Int) => Int`.

```scala mdoc
def squareF(x: Int, f: Int => Int): Int =
  f(x) * f(x)
```

Ta có thể truyền `add42` phương thức nêu trên

```scala mdoc
squareF(0, add42)
```

Ta cũng có thể truyền một nguyên mẫu hàm

```scala mdoc
squareF(0, x => x + 42)
```

Lưu ý rằng ở đây ta không phải đặt kiểu tham số vào nguyên văn hàm vì Scala đã có đủ thông tin để suy diễn được kiểu đó rồi.



<div class="callout callout-info">
#### Cú pháp khai báo kiểu hàm {-}

Để khai báo một kiểu hàm, ta viết

```scala
(A, B, ...) => C
```

trong đó

- `A, B, ...` là những kiểu của các tham số đầu vào; và 
- `C` là kiểu của kết quả.

Nếu một hàm chỉ có đúng một tham số thì cặp ngoặc tròn có thể bỏ đi được:

```scala
A => B
```
</div>



### Hàm như là đối tượng 

Tất cả những giá trị thuộc lớp hạng nhất đều là các đối tượng trong Scala, kể cả các hàm.
Như vậy nghĩa là hàm cũng có thể chứa phương thức, bao gồm những cách hữu ích để ghép.

```scala mdoc
val addTen = (a: Int) => a + 10
val double = (a: Int) => a * 2
val combined = addTen.andThen(double) // ghép hai hàm 
combined(5)
```

Khi gọi hàm, thực ra ta đi gọi tới phương thức có tên `apply` đối với hàm. Scala cho phép viết tắt bất kì đối tượng nào có phương thức tên là `apply`, theo đó ta có thể bỏ tên phương thức `apply` và viết lời gọi này như một lời gọi hàm. Như vậy các dòng lệnh dưới đây là tương đương nhau:

```scala mdoc
val halve = (a: Int) => a / 2
halve(4)
halve.apply(4)
```


### Quy đổi phương thức thành hàm

Phương thức rất giống với hàm, vì vậy Scala cho ta cách quy đổi hàm thành phương thức. Nếu ta viết vào sau tên phương thức một dấu `_` thì nó sẽ được chuyển thành một hàm.

```scala mdoc
def times42(x: Int): Int =
  x * 42

val times42Function = times42 _
```

Chúng ta cũng có thể viết một lời gọi phương thức mà thay toàn bộ tham số của nó bằng `_` va Scala sẽ quy đổi phương thức này thành một hàm.

```scala mdoc
val times42Function2 = times42(_)
```



#### Bài tập {-}

##### Nguyên văn hàm

Ta hãy luyện tập một chút viết các nguyên văn hàm. Hãy viết một nguyên văn hàm để:

- tính bình phương đầu vào kiểu `Int` của nó;
- có tham số `Color` và quay màu của màu `Color` đó đi góc 15 độ; và 
- nhận đầu vào là một `Image` rồi tạo ra bốn bảo sao xếp trên cùng một hàng, mỗi bản sao lại được quay góc 90 độ so với hình đứng trước (để làm điều này, xem phương thức `rotate` đối với `Image`.)

<div class="solution">
Hàm thứ nhất là

```scala mdoc
(x: Int) => x * x
```

Hàm thứ hai là

```scala mdoc
(c: Color) => c.spin(15.degrees)
```

Hàm thứ ba nhất là

```scala mdoc
(image: Image) => 
  image.beside(image.rotate(90.degrees))
    .beside(image.rotate(180.degrees))
    .beside(image.rotate(270.degrees))
    .beside(image.rotate(360.degrees))
```
</div>



##### Kiểu của hàm {-}

Dưới đây là một hàm thú vị mà ta sẽ dùng nhiều tới trong những mục sau này. Bây giờ bạn chưa cần phải hiểu ngay tác dụng của nó, dù có lẽ vẫn muốn thử nghiệm xem sao.

```
val roseFn = (angle: Angle) =>
  Point.cartesian((angle * 7).cos * angle.cos, (angle * 7).cos * angle.sin)
```

Kiểu của hàm `roseFn` nêu trên là gì? Kiểu này nghĩa là sao?

<div class="solution">
Kiểu này là `Angle => Point`; đồng nghĩa với việc `roseFn` là một hàm nhận vào chỉ một đối số có kiểu `Angle` (góc) rồi trả lại một giá trị kiểu `Point` (điểm). Nói cách khác, `roseFn` chuyển đổi một `Angle` một `Point`.
</div>
