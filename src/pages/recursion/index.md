# Đệ quy cấu trúc

Trong chương này ta sẽ thấy dạng mẫu chính thứ nhất để tính toán cấu trúc: *đệ quy cấu trúc trên những số tự nhiên*. Nghe có vẻ đao to búa lớn, vậy ta hãy cùng tách ra xem:

- Nói dạng mẫu nghĩa là một cách viết mã lệnh hữu dụng cho nhiều ngữ cảnh khác nhau. Ta sẽ còn gặp đệ quy cấu trúc ở nhiều tình huống khác nhau trong sách này.

- Nói số tự nhiên nghĩa là những số nguyên từ 0, 1, 2, trở lên. 

- Nói đệ quy nghĩa là điều gì đó tự nó lặp lại. Đệ quy cấu trúc nghĩa là phép đệ quy tuân theo cấu trúc của dữ liệu mà nó xử lí. Nếu dữ liệu có tính đệ quy (tức là tham chiếu tới chính nó) thì đệ quy cấu trúc cũng sẽ tham chiếu tới chính nó. Sau này sẽ thấy kĩ hơn điều đó nghĩa là gì.

<div class="callout callout-info">
Nếu bạn chạy các ví dụ từ dòng lệnh SBT console bên trong Doodle thì chúng sẽ tự hoạt động. Nếu không, bạn sẽ cần phải mở đầu mã lệnh với những câu lệnh nhập import sau để Doodle dùng được.

```scala mdoc:silent
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```
</div>

