## Làm việc trong console

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Trình biên tập hoặc IDE bạn dùng sẽ cho phép bạn lưu mã lệnh vào một file, nhưng bạn cần phải lưu các file vào đúng chỗ mà trình biên dịch Scala có thể tìm thấy.
Nếu bạn làm việc từ bản mẫu Doodle thì bạn cần lưu mã lệnh vào thư mục `src/main/scala/`.

Vậy từ console, làm thế nào để dùng mã lệnh ta đã lưu vào file?
Có một câu lệnh đặc biệt, chỉ có tác dụng từ console, giúp ta chạy mã lệnh đã lưu trong file.
Lệnh đó có tên là `:paste`[^load]. Sau chữ `:paste` ta viết tên file muốn chạy. Chẳng hạn, nếu ta lưu trong file `src/main/scala/Example.scala` biểu thức sau

```scala mdoc:silent
Image.circle(100).fillColor(Color.paleGoldenrod).strokeColor(Color.indianRed)
```

thì ta có thể chạy mã lệnh này bằng cách gõ vào console

```scala
:paste src/main/scala/Example.scala
// res0: doodle.core.Image = ContextTransform(<function1>,ContextTransform(<function1>,Circle(100.0)))
```

Lưu ý rằng giá trị đã được đặt tên là `res0` ở ví dụ trên. Nếu ta đang gõ dở mã lệnh, cái tên ở trong console có thể sẽ khác đi tùy theo bạn đã gõ gì vào console rồi. Ta có thể vẽ hình bằng cách ước lượng `res0.draw` (hoặc cái tên phù hợp ở console của bạn).

### Các mẹo sử dụng console

Dưới đây là một số mẹo sử dụng console một cách năng suất hơn:

- Nếu ấn phím mũi tên lên, bạn sẽ lấy được những gì lần trước đây bạn gõ vào console. Rất tiện để tránh phải gõ đi gõ lại các tên file dài! Bạn có thể ấn phím nhiều lần để duyệt qua lịch sử các tương tác của bạn tại console.

- Bạn có thể nhấn phím `Tab` để được những phương án gợi ý điền mã lệnh, song không may là tên file thì không được. Chẳng hạn, nếu bạn gõ vào `Stri` và nhấn phím `Tab`, console sẽ cho thấy những cách hoàn thành có thể. Gõ vào `Strin` và console sẽ điền `String` cho bạn.

[^load]: Một lệnh tên là `:load` có tác dụng hơi khác với `:paste`. Nó biên dich và tự chạy từng dòng trong file, còn `:paste` thì biên dịch và chạy file luôn một lượt. Chúng có ngữ nghĩa hơi khác nhau chút. Cách làm việc của `:paste` gần sát hơn với cách mà mã lệnh Scala hoạt động bên ngoài console, vì vậy ta sẽ ưu tiên dùng nó thay vì `:load`.

<div class="callout callout-warn">
Một khi đã bắt đầu lưu mã lệnh vào file, ta sẽ có thể thấy rằng trình biên dịch không thích mã lệnh của ta lắm vào lần tiếp theo khi ta khởi động SBT. Để biết cách sửa chữa, hãy đọc mục tiếp theo.
</div>
