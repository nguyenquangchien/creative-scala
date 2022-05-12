## Names

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Ở các mục trước, chúng tôi đã giới thiệu rất nhiều khái niệm mới.
Trong mục này, ta sẽ khám phá một trong những khái niệm đó: đặt tên cho giá trị.

Ta dùng tên để chỉ các thứ khác nhau. 
Chẳng hạn, "Professeur Emile Perrot" dùng để chỉ một loài hoa hồng ngát hương, còn "Cherry Parfait" là loài hoa có khả năng chống bệnh tốt nhưng hầu như chẳng có mùi thơm gì.
Viết dài dòng với những câu từ hoa mĩ như vậy mới thể hiện được khác biệt trong lời văn.
Nhưng ngôn ngữ lập trình thì hạn chế hơn nhiều, chúng cho phép ta nói chính xác: tên gọi chỉ đến giá trị.
Đôi khi ta nói rằng các tên *buộc* vào giá trị, hay tên giới thiệu một *dây buộc*.
Mỗi khi ta phải viết ra giá trị thì thay vào đó sẽ viết tên nó, nếu giá trị này có tên. 
NÓi cách khác, một cái tên sẽ ước lượng thành giá trị mà nó chỉ đến. 
Từ đây sẽ tự nhiên nảy sinh câu hỏi: làm thế nòa để đặt tên cho các giá trị?
Trong Scala, có vài cách thực hiện điều này.
Hãy cùng xem nhé.


### Nguyên văn đối tượng

Ta đã thấy ví dụ về khai báo một nguyên văn đối tượng rồi.

```scala mdoc:silent
object Example {
  Image.circle(100).fillColor(Color.paleGoldenrod).strokeColor(Color.indianRed).draw()
}
```

Đây là một biểu thức nguyên văn, cũng như những nguyên văn khác mà ta từng gặp, nhưng trong trường hợp này nó tạo nên một đối tượng với cái tên `Example`.
Trong một chương trình, khi ta dùng tên `Example`, nó sẽ ước lượng thành đối tượng đó.

```scala
Example
// Example.type = Example$@76c39258
```

Hãy thử lệnh này vài lần trong console.
Bạn có nhận thấy khác biệt gì giữa các lần sử dụng tên này không?
Bạn có thể phát hiện thấy rằng lần *đàu* khi nhập vào tên `Example` thì sẽ vẽ nên bức tranh, song điều này sẽ không xảy ra ở những lần tiếp theo sử dụng tên.
Lần đầu tiên ta dùng tên một đối tượng thì phần thân của đối tượng được ước lượng và đối tượng được tạo nên.
Ở những lần sử dụng tiếp theo, đối tượng đã tồn tại rồi và sẽ không ước lượng lại nữa.
Có thể nói rằng sự khác biệt ở đây nằm ở chỗ biểu thức bên trong đối tượng gọi đến phương thức `draw`.
Nếu ta thay thế nó bằng một thứ kiểu như `1 + 1` (hoặc đơn giản chỉ xóa bỏ lời gọi tới `draw`) thì sẽ không thể nào phân biệt được giữa chúng.
Trong chương tiếp theo ta sẽ còn nói nhiều về vấn đề này.

Bạn có thể băn khoăn về kiểu của đối tượng mới được tạo nên.
Ta có thể hỏi console về điều này.

```scala
:type Example
// Example.type
```

Kiểu của `Example` là `Example.type`, một kiểu độc nhất mà không giá trị nào khác có được.


### Những khai báo `val`

Việc khai báo một nguyên văn đối tượng là sự hòa trộn giữa tạo đối tượng và định nghĩa một cái tên.
Sẽ rất hữu ích nếu ta có thể tách bạch hai điều này, để có thể đặt tên cho một đối tượng đã tồn tại rồi.
Lời khai báo `val` cho phép ta làm điều này.

Ta dùng `val` bằng cách viết

```scala
val <name> = <value>
```

trong đó `<name>` và `<value>` lần lượt thay cho tên và biểu thức ước lượng thành giá trị.
Chẳng hạn

```scala mdoc:silent
val one = 1
val anImage = Image.circle(100).fillColor(Color.red)
```

Hai lệnh khai báo này đã định nghĩa những cái tên `one` và `anImage`.
Ta có thể dùng hai tên gọi này để chỉ các giá trị trong mã lệnh sau này.

```scala mdoc
one
anImage
```


### Lời khai báo

Ở trên ta đã nói về các lời khai báo và định nghĩa.
Bây giờ là lúc để nói chính xác hơn ý nghĩa của những khái niệm này, và phân tích sâu hơn những khác biệt giữa `object` và `val`.

Ta đã biết về các biểu thức.
Chúng là thành phần của một chương trình, và ước lượng thành giá trị.
Một lời *khai báo* hay *định nghĩa* là thành phần khác của chương trình, nhưng không ước lượng thành giá trị.
Thay vì vậy, chúng đặt tên cho một thứ gì đó---không nhất thiết phải là giá trị, vì bạn có thể khai báo các kiểu trong Scala, dù ta không dành nhiều thời gian về điều này.
Cả `object` lẫn `val` đều là những lời khai báo.

Một hệ quả của sự tách biệt giữa khai báo với biểu thức, đó là ta không thể viết chương trình kiểu như

```scala
val one = ( val aNumber = 1 )
```

vì `val aNumber = 1` không phải là biểu thức và do vậy không ước lượng thành giá trị.

Dù vậy, ta có thể viết 

```scala mdoc:reset
val aNumber = 1
val one = aNumber
```


### Tầng đỉnh

Dường như không ổn khi ta có cả lời khai báo `object` lẫn `val`, vì chúng đều đặt tên cho giá trị.
Tại sao không phải chỉ là `val` để khai báo tên, và để cho `object` chi tạo nên đối tượng mà không đặt tên chúng?
Bạn có thể khai báo một nguyên văn đối tượng mà không đặt tên không?

<div class="solution">
Không, Scala không cho phép ta làm điều này.
Chẳng hạn, ta không thể viết 

```scala
object {}
```

Ta phải đặt tên cho bất kì nguyên văn đối tượng nào ta tạo ra.
</div>

Scala phân biệt giữa cái mà ta gọi là *tầng đỉnh* với mã lệnh khác.
Mã lệnh tại tầng đỉnh thì không có mã lệnh nào khác bọc quanh nó.
Nói cách khác, nó là những gì ta có thể viết vào một file mà Scala sẽ biên dịch mà không phải bọc nó vào một `object`.

Ta đã thấy rằng các biểu thức không được phép viết tại tầng đỉnh.
Các định nghĩa `val` cũng vậy.
Tuy nhiên, các nguyên văn đối tượng thì được.

Sự phân biệt này có chút khó chịu.
Một số ngôn ngữ khác không có sự bó buộc này.
Với trường hợp Scala, sở dĩ vậy vì Scala được lập trên cơ sở máy ảo Java Virtual Machine (JVM), vốn được thiết kế để chạy mã lệnh Java.
Java phân biệt giữa mã tầng đỉnh với mã lệnh khác, và Scala bị buộc phải phân biệt thế này khi làm việc với JVM. 
Console của Scala *không* có sự phân biệt tầng đỉnh này (bạn có thể hình dung rằng mọi thứ viết trên console đều được bọc bằng một đối tượng nào đó); điều này có thể gây nhầm lẫn với người mới dùng Scala.

Nếu tầng đỉnh cho phép viết nguyên văn đối tượng, nhưng không cho định nghĩa `val`, thì điều này có nghĩa rằng ta được khai báo `val` bên trong một nguyên văn đối tượng không?
Nếu ta có thể khai báo `val` bên trong một nguyên văn đối tượng, thì sau này ta có thể chỉ đến tên gọi đó không?

<div class="solution">
Được, dĩ nhiên rồi!

Ta có thể viết `val` bên trong một nguyên văn đối tượng như sau:

```scala mdoc:reset:silent
object Example {
  val hi = "Hi!"
}
```

Khi đó ta có thể chỉ đến nó bằng cú pháp `.` mà ta đã dùng.

```scala mdoc
Example.hi
```

Lưu ý rằng ta không thể viết `hi` lẻ loi được:

```scala mdoc:fail
hi
```

Ta phải báo Scala biết rằng ta muốn chỉ tới cái tên `hi` định nghĩa bên trong đối tượng `Example`.
</div>


### Phạm vi

Nếu bạn đã làm bài tập trên (bạn làm rồi chứ?) thì sẽ thấy được rằng một cái tên định nghĩa trong một đối tượng sẽ không thể dùng được ngoài đối tượng mà quên chỉ ra đối tượng có chứa tên đó.
Cụ thể, nếu ta khai báo

```scala mdoc:reset:silent
object Example {
  val hi = "Hi!"
}
```

thì ta không thể viết

```scala mdoc:fail
hi
```

Ta phải bảo Scala đi tìm `hi` bên trong `Example`.

```scala mdoc
Example.hi
```

Ta nói rằng một cái tên chỉ *nhìn thấy* ở những chỗ mà nó có thể được dùng mà không phải định tên (bằng cú pháp dấu chấm như trên), và cũng nói rằng *phạm vi* của một cái tên là những chỗ mà tên đó nhìn thấy được.
Như vậy, khi dùng các thuật ngữ mới rất trang trọng này, thì `hi` không thể nhìn thấy bên ngoài `Example`, hoặc nói cách khác `hi` chỉ có phạm vi trong `Example`.

Làm thế nào để xác định phạm vi của một cái tên?
Quy tắc cũng khá đơn giản: một cái tên chỉ nhìn thấy từ chỗ nó được khai báo đến cuối dấu đóng ngoặc nhọn gần nhất (các ngoặc nhọn gồm `{` và `}`).
Ở ví dụ trên `hi` được bọc bởi các dấu ngoặc của `Example` và do vậy chỉ nhìn thấy trong đó. 
Nó không thể nhìn thấy được từ những chỗ khác.

Ta có thể khai báo các nguyên văn đối tượng bên trong nguyên văn đối tượng khác, bằng cách này cho phép phân biệt phạm vi một cách chi li hơn.

Chẳng hạn, trong mã lệnh dưới đây

```scala mdoc:silent
object Example1 {
  val hi = "Hi!"

  object Example2 {
    val hello = "Hello!"
  }
}
```

`hi` vẫn trong tầm với trong `Example2` (`Example2` được định nghĩa bên trong cặp ngoặc nhọn bao bọc `hi`).
Tuy nhiên phạm vi của `hello` bị hạn chế trông `Example2`, và phạm vi của nó bó hẹp hơn là `hi`.

Điều gì sẽ xảy ra nếu ta khai báo một cái tên bên trong một phạm vi nơi đã được khai báo rồi?
Hiện tượng này là *phủ bóng*.
Trong mã lệnh dưới đây, lời định nghĩa `hi` bên trong `Example2` đã phủ bóng định nghĩa `hi` trong `Example1`

```scala mdoc:reset:silent
object Example1 {
  val hi = "Hi!"

  object Example2 {
    val hi = "Hello!"
  }
}
```

Scala cho phép ta làm điều này, song nói chung đây là cách làm dở vì nó có thể khiến mã lệnh rất khó hiểu.

Ta không cần dùng các nguyên văn đối tượng để tạo nên những phạm vi mới.
Scala cho phép ta tạo phạm vi mới gần như mọi nơi chỉ bằng việc viết cặp ngoặc nhọn. 
Bởi vậy ta có thể viết

```scala mdoc:reset:silent
object Example {
  val good = "Good"

  // Tạo một phạm vi mới
  {
    val morning = good ++ " morning"
    val toYou = morning ++ " to you"
  }

  val day = good ++ " day, sir!"
}
```

`morning` (và `toYou`) được khai báo bên trong một phạm vi mới. Ta không có cách nào chỉ đến phạm vi này từ bên ngoài (vì phạm vi này vô danh), bởi vậy ta không thể chỉ tới `morning` từ bên ngoài phạm vi mà nó được khai báo.
Nếu ta có điều gì bí mật mà không muốn cho phần còn lại của chương trình biến đến, thì đây chính là một cách để che giấu đi.

Cách hoạt động của các phạm vi lồng ghép nhau trong Scala được gọi là *phạm vi từ vựng*.
Không phải ngôn ngữ nào cũng có phạm vi từ vựng.
Chẳng hạn, Ruby và Python không có, còn Javascript thì mãi gần đây mới tiếp nhận phạm vi từ vựng.
Theo tác giả thì việc tạo nên ngôn ngữ mà không có phạm vi từ vựng thì cũng chẳng khác gì ăn ớt cay rồi đi vệ sinh mà không rửa tay vậy.


### Bài tập {-}

Hãy kiểm tra hiểu biết của bạn về các tên gọi và phạm vi bằng cách tìm ra giá trị của `answer` ở mỗi trường hợp sau.

```scala mdoc:silent
val a = 1
val b = 2
val answer = a + b
```

<div class="solution">
Một ví dụ đơn giản để mở đầu. `answer` bằng `1 + 2`, tức là `3`.
</div>

```scala mdoc:silent
object One {
  val a = 1

  object Two {
    val a = 3
    val b = 2
  }

  object Answer {
    val answer = a + Two.b
  }
}
```

<div class="solution">
Một ví dụ đơn giản khác. `answer` bằng `1 + 2`, tức là `3`. `Two.a` nằm ngoài tầm với khi `answer` được định nghĩa.
</div>

```scala mdoc:reset:silent
object One {
  val a = 5
  val b = 2

  object Answer {
    val a = 1
    val answer = a + b
  }
}
```

<div class="solution">
Ở đây `Answer.a` phủ bóng lên `One.a` cho nên `answer` bằng `1 + 2`, tức là `3`.
</div>

```scala mdoc:reset:silent
object One {
  val a = 1
  val b = a + 1
  val answer = a + b
}
```

<div class="solution">
Viết thế này hoàn toàn hợp lệ. Biểu thức `a + 1` ở vế phải của dòng khai báo `b` cũng giống như bao biểu thức khác, vì vậy một lần nữa `answer` lại bằng `3`.
</div>

```scala mdoc:reset:fail:silent
object One {
  val a = 1

  object Two {
    val b = 2
  }

  val answer = a + b
}
```

<div class="solution">
Mã lệnh này không biên dịch vì `b` nằm ngoài tầm với khi `answer` được khai báo.
</div>

```scala mdoc:silent:fail
object One {
  val a = b - 1
  val b = a + 1

  val answer = a + b
}
```

<div class="solution">
Câu hỏi mẹo! Mã lệnh này không hoạt động. Ở đây `a` và `b` được khai báo phụ thuộc lẫn nhau, dẫn tới sự phụ thuộc luẩn quẩn mà không thể phân giải được.
</div>
