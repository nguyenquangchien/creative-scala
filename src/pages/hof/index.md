# Trồng trọt và Hàm bậc cao

Ở chương này ta sẽ học cách vẽ những bông hoa và dùng hàm như các giá trị lớp hạng nhất.

Ta biết rằng chương trình làm việc với những giá trị, nhưng không phải giá trị nào cũng thuộc *lớp hạng nhất* (first-class). Một giá trị thuộc lớp hạng nhất là giá trị mà ta có thể truyền như tham số vào phương thức, hay trả lại như một kết quả từ lời gọi phương thức, hay đặt một tên bằng `val`.

Nếu ta truyền hàm như một đối số vào trong hàm khác thì:

- hàm được truyền thì dùng như giá trị thuộc lớp hạng nhất; và 
- hàm nào nhận vào tham số hàm như vậy sẽ được gọi là *hàm bậc cao*.

Thuật ngữ này không đặc biệt quan trọng, song bạn sẽ gặp phải trong những tài liệu khác, bởi vậy cần biết tới nó (ít ra là hiểu nôm na ý nghĩa).
Mọi thứ sẽ sớm rõ hơn khi ta xem thêm vài ví dụ nữa.

Đến giờ ta đã dùng lẫn các thuật ngữ *hàm* và *phương thức*.
Ta sẽ sớm thấy rằng trong Scala, hai thuật ngữ này có ý nghĩa riêng, dù liên quan đến nhau.

Vậy là đủ kiến thức cơ bản rồi. Hãy cùng đi sâu vào để xem:

- cách tạo ra hàm trong Scala; và
- cách dùng hàm thuộc lớp hạng nhất để cấu trúc hoá chương trình.

Thôi thúc ta tìm hiểu vấn đề này sẽ là ví dụ vẽ những bông hoa như [@fig:hof:flower-power].

![A flower created using the techniques in this chapter](src/pages/hof/flower-power.pdf+svg){#fig:hof:flower-power}

<div class="callout callout-info">
Nếu bạn chạy những ví dụ này từ dòng lệnh (SBT console) bêm trong Doodle, chương trình sẽ hoạt động. Nếu không, bạn sẽ cần phải bắt đầu mã lệnh với những câu lệnh nhập sau đây để gọi được Doodle.

```scala mdoc:silent
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```
</div>
