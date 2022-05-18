## Thứ tự ước lượng

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Bây giờ ta đã sẵn sàng trả lời câu hỏi thứ tự ước lượng.
Ta có thể tự hỏi liệu thứ tự ước lượng có quan trọng không?
Ở những ứng dụng ta đã thấy trước đây, thứ tự dường như không quan trọng, chỉ cần lưu ý rằng ta không thể ước lượng biểu thức trước khi ước lượng hết các biểu thức con của nó.

Để xem xét kĩ những vấn đề này, ta cần giới thiệu một khái niệm mới.
Đến giờ ta gần như luôn tính toán với các biểu thức *thuần*.
Đây là những biểu thức mà ta có thể tùy ý thay thế theo bất kì thứ tự nào mà không gặp vấn đề gì[^corner-cases].

Các biểu thức *không thuần* là những biểu thức mà thứ tự ước lượng là quan trọng.
Ta đã dùng một biểu thức không thuần, đó là phương thức `draw`.
Nếu ta ước lượng

```scala
Image.circle(100).draw
Image.rectangle(100, 50).draw
```

và

```scala
Image.rectangle(100, 50).draw
Image.circle(100).draw
```

thì các cửa sổ chứa các hình ảnh sẽ xuất hiện theo thứ tự khác nhau. 
Khác biệt là rất nhỏ, nhưng *vẫn là* khác biệt, chính là điều muốn nói ở đây.

Tính năng độc đáo chính của biểu thức không thuần là ở chỗ sự ước lượng chúng gây ra thay đổi trông thấy.
Chẳng hạn, việc ước lượng `draw` khiến cho một hình ảnh được hiển thị. 
Ta gọi những biến đổi trông thấy này là *hiệu ứng phụ*, hay gọi tắt là *hiệu ứng*.
Trong một chương trình có chứa hiệu ứng phụ, ta không thể dùng cách thay thế.
Tuy nhiên ta có thể dùng hiệu ứng phụ để điều tra thứ tự ước lượng.
Công cụ giúp ta thực hiện là phương thức `println`.

Phương thức `println` hiển thị chữ lên console (một hiệu ứng phụ) và ước lượng thành unit.
Sau đây là ví dụ:

```scala mdoc
println("Hello!")
```

Hiệu ứng phụ của `println`---in ra console---cho ta cách tiện lợi để điều tra thứ tự ước lượng.
Chẳng hạn, kết quả của việc chạy mã lệnh

```scala mdoc
println("A")
println("B")
println("C")
```

sẽ cho thấy rằng các biểu thức được thực hiện từ trên xuống. 
Ta hãy dùng `println` để điều tra thêm.


### Bài tập {-}

#### Không thay thế cho Println {-}

Trong một chương trình thuần ta có thể đặt tên cho biểu thức bất kì và thay thế mọi lượt xuất hiện của biểu thức này bằng tên.
Cụ thể, ta có thể viết lại 

```scala mdoc:silent
(2 + 2) + (2 + 2)
```

thành

```scala mdoc:silent
val a = (2 + 2)
a + a
```

mà kết quả chương trình vẫn không thay đổi.

Hãy dùng `println` làm ví dụ về một biểu thức không thuần nhằm cho thấy rằng: nhận định trên *không* đúng với các biểu thức không thuần, và  the case for impure expressions, và do vậy ta có thể nói rằng biểu thức không thuần, hay hiệu ứng phụ, đã phá vỡ luật thay thế.

<div class="solution">
Sau đây là một ví dụ đơn giản cho thấy điều này.
Hai chương trình dưới khác biệt trông thấy.

```scala mdoc
println("Happy birthday to you!")
println("Happy birthday to you!")
println("Happy birthday to you!")
```

```scala mdoc
val happy = println("Happy birthday to you!")
happy
happy
happy
```

Do vậy ta không thể thoải mái sử dụng thay thế khi chương trình có các hiệu ứng phụ, và cần phải nhận thức được thứ tự ước lượng.
</div>


#### Phát điên với các phương thức {-}

Khi chúng tôi giới thiệu về phạm vi thì cũng giới thiệu cả biểu thức khối, dù rằng chưa gọi chúng bằng cái tên này.
Một khối được tạo thành từ cặp ngoặc nhọn (`{}`). Nó ước lượng tất cả các biểu thức có trong cặp ngoặc. Giá trị cuối cùng là giá trị của biểu thức cuối cùng trong khối.

```scala mdoc
// Ước lượng thành 3
{
  val one = 1
  val two = 2
  one + two
}
```

Ta có thể dùng biểu thức khối để điều tra thứ tự ước lượng các tham số phương thức, bằng cách đặt biểu thức `println` vào trong khối ước lượng thành một giá trị hữu ích nào đó khác.

Chẳng hạn, dùng `Image.rectangle` hay `Color.hsl` và biểu thức khối, ta có thể xác định xem liệu Scala ước lượng các tham số phương thức theo thứ tự cố định hay không, và nếu đúng vậy thì thứ tự là gì.

Lưu ý rằng bạn có thể viết gọn một khối trên một dòng, bằng cách phân tách những biểu thức dấu chấm phẩy (`;`).
Thường thì đây không phải là phong cách hay song cũng hữu ích cho việc thử nghiệm này.
Sau đây là một ví dụ.

```scala mdoc
// Ước lượng thành 3
{ val one = 1; val two = 2; one + two }
```

<div class="solution">
Mã lệnh sau biểu diễn rằng các tham số phương thức được ước lượng từ trái qua phải.

```scala mdoc
Color.hsl(
  {
    println("a")
    0.degrees
  },
  {
    println("b")
    1.0
  },
  {
    println("c")
    1.0
  }
)
```

Có thể viết mã lệnh này gọn hơn như sau
```scala mdoc
Color.hsl({ println("a"); 0.degrees },
          { println("b"); 1.0 },
          { println("c"); 1.0 })
```
</div>


#### Thứ tự cuối {-}

Các biểu thức Scala được ước lượng theo thứ tự nào?
Hãy làm thử nghiệm bất kì theo ý bạn, để trả lời câu hỏi này.
Bạn có thể giả định một cách hợp lý rằng Scala dùng quy tắc thống nhất với tất cả mọi biểu thức.
Không có trường hợp đặc biệt cho các biểu thức khác nhau.

<div class="solution">
Ta đã thấy rằng các biểu thức được ước lượng từ trên xuống dưới, và tham số phương thức được ước lượng từ trái qua phải.
Có thể ta sẽ muốn kiểm tra rằng các biểu thức nói chung được ước lượng từ trái qua phải.
Điều này có thể cho thấy khá dễ dàng.

```scala mdoc
{ println("a"); 1 } + { println("b"); 2 } + { println("c"); 3}
```

Vậy kết luận là biểu thức Scala được ước lượng từ trên xuống dưới và từ trái qua phải.
</div>

[^corner-cases]: Điều này không hoàn toàn đúng. Có những trường hợp lắt léo mà ở đó thứ tự ước lượng sẽ tạo nên khác biệt thậm chí với cả biểu thức thuần. Song ở đây ta sẽ không lo lắng về các trường hợp như vậy. Nếu bạn muốn tìm hiểu thêm, và điều đó thú vị và hữu ích, bạn có thể đọc về ước lượng ham ("eager evaluation") và ước lượng nhác ("lazy evaluation").
