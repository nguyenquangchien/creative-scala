## Các gói và lệnh nhập

Khi ta thay đổi mã lệnh để biên dịch, ta phải thêm vào nhiều *lệnh nhập*.
Ở mục này, ta sẽ tìm hiểu về chúng.

Ta đã thấy rằng một tên có thể phủ bóng lên một tên khác. 
Điều này có thể gây nên vấn đề trong những chương trình lớn hơn, vì nhiều phần của chương trình có thể muốn dùng một tên chung cho nhiều mục đích.
Ta có thể tạo nên các phạm vi để che giấu những tên này khỏi bên ngoài, song vẫn cần phải giải quyết những cái tên định nghĩa ở tầng đỉnh.


Ta cũng gặp vấn đề tương tự trong ngôn ngữ giao tiếp.
Chẳng hạn, nếu cả người anh và một cậu bạn đều có tên là "Ziggy" thì bạn sẽ phải hạn định xem bạn muốn chỉ ai khi gọi tên họ.
Có thể bạn sẽ phân biệt theo ngữ cảnh, hoặc có lẽ tên cậu bạn là "Ziggy S" còn tên người anh chỉ là "Ziggy".

Trong Scala, ta có thể dùng các *gói* để tổ chức các tên. 
Mỗi gói tạo ra một phạm vi cho các tên được định nghĩa ở tầng đỉnh.
Tất cả các tên tầng đỉnh trong cùng một gói thì được định nghĩa trong cùng phạm vi.
Để đưa các tên trong một gói vào một phạm vi khác, ta phải *nhập* chúng.

Để tạo một gói thì rất đơn giản: ta viết 

```scala
package <name>
```

vào đầu file, trong đó thay `<name>` bởi tên của gói.

Khi ta muốn dùng các tên định nghĩa trong một gói, ta dùng một lệnh `import` (nhập), chỉ định tên của gói theo sau là `_` cho tất cả các tên, hoặc chỉ một số tên cụ thể trong gói đó nếu muốn.

Sau đây là một ví dụ.

<div class="info">
Bạn không thể định nghĩa gói từ trong console.
Để chạy các mã lệnh sau bạn phải viết mã lệnh trong gói `example` vào một file và bien dịch file đó.
</div>

Hãy cùng bắt đầu bằng việc định nghĩa vài cái tên trong một gói.

```scala
package example

object One {
  val one = 1
}

object Two {
  val two = 2
}

object Three {
  val three = 3
}
```

Bây giờ để đưa những tên này vào trong phạm vi, ta phải nhập chúng.
Có thể ta chỉ nhập mỗi một cái tên.

```scala
import example.One

One.one
```

Hoặc nhập cả hai tên `One` và `Two`.

```scala
import example.{One, Two}

One.one + Two.two
```

Hoặc nhập tất cả mọi tên trong `example`.

```scala
import example._

One.one + Two.two + Three.three
```

Trong Scala, ta cũng có thể nhập vào gần như mọi thứ định nghĩa nên một phạm vi, bao gồm các đối tượng.
Vì vậy mã lệnh sau sẽ đưa `one` vào trong phạm vi.

```scala
import example.One._

one
```

### Tổ chức gói

Gói giúp ta ngăn chặn các tên ở tầng đỉnh khỏi xung khắc nhau, song sự xung khắc giữa các tên gói thì sao?
Người ta thường tổ chức các gói theo cấp bậc, để tránh xung khắc. 
Chẳng hạn, trong Doodle thì gói `core` được định nghĩa bên trong gói `doodle`.
When we use the statement

```scala mdoc:silent
import doodle.core._
```

Ta đang chỉ ra rằng ta muốn gói `core` bên trong gói `doodle`, chứ không phải một gói nào đó khác cũng tên là `core`.
