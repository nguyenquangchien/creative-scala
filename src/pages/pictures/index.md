# Tính toán với hình vẽ

Đến giờ ta đã tính toán với số, chuỗi kí tự và các đối tượng đơn giản khác. Từ giờ trở đi, ta sẽ tập trung chú ý đến tính toán với hình vẽ, và sau đó là với hoạt hình. Các hình vẽ cho ta thêm cơ hội sáng tạo ngay lập tức, và chúng khiến cho kết quả đầu ra chương trình trở nên cụ thể hơn theo cách mà những phương pháp còn lại không có được.

Ta sẽ sử dụng một thư viện có tên Doodle để giúp việc tạo nên đồ họa. Trong chương này, ta sẽ tìm hiểu cơ bản về Doodle.

<div class="callout callout-info">
Nếu bạn chạy những ví dụ này từ dòng lệnh (SBT console) bêm trong Doodle, chương trình sẽ hoạt động. Nếu không, bạn sẽ cần phải bắt đầu mã lệnh với những câu lệnh nhập sau đây để gọi được Doodle.

```scala mdoc
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```
</div>
