# Biểu thức, giá trị, và kiểu dữ liệu

Các chương trình Scala gồm có 3 thành phần cơ bản: các *biểu thức*, *giá trị*, và *kiểu dữ liệu*. Ở mục này, ta sẽ tìm hiểu ba khái niệm nêu trên.

Dưới đây là một biểu thức rất đơn giản:

```scala mdoc:silent
1 + 2
```

Một *biểu thức* là một đoạn mã lệnh Scala code. Ta có thể viết các biểu thức trong một trình biên tập văn bản (text editor), hoặc lên giấy, hay lên tường; các biểu thức cũng giống như chữ viết vậy. Tương tự như chữ viết ra phải được đọc mới có tác dụng đối với hiện thực (và người đọc phải hiểu được ngôn ngữ dùng để viết chữ đó), máy tính phải *chạy* được một biểu thức thì nó mới có tác dụng. Kết quả từ việc chạy biểu thức là một *giá trị*. Các giá trị tồn tại trong bộ nhớ máy tính, theo cách giống như kết quả những câu chứ đọc được đọng lại trong tâm trí độc giả. Ta cũng sẽ nói rằng những biểu thức được *ước lượng* hay *thực thi* để mô tả quá trình chuyển chúng thành giá trị.

Ta có thể lập tức lượng giá các biểu thức bằng cách viết chúng vào đấu nhắc trong console (còn gọi là "terminal" hay thiết bị đầu cuối) rồi ấn phím "Enter" (hay "Return"). Hãy thử nó luôn.

```scala mdoc
1 + 2
```

Console sẽ phản hồi với giá trị mà biểu thức được ước lượng thành, cũng như kiểu dữ liệu của biểu thức.

Biểu thức `1 + 2` ước lượng thành giá trị `3`. Ta có thể viết số ba ở đây lên tờ giấy, nhưng giá trị thực sự vẫn là thứ được lưu trong bộ nhớ máy tính. Ở trường hợp này, đó là một số nguyên 32-bit biểu diễn dưới dạng "bù 2" (two's-complement, kiểu như nhị phân). Ý nghĩa của "số nguyên 32-bit biểu diễn dưới dạng bù 2" không quan trọng. Chúng tôi chỉ đề cập tới khái niệm này để nhấn mạnh rằng máy tính biểu diễn giá trị `3` là giá trị thực, chứ không phải là con số ghi ra giấy hay hiện lên trên màn hình console.

*Kiểu dữ liệu* là mảnh ghép cuối cùng trong bức hình. Một kiểu dữ liệu thì mô tả một tập hợp các giá trị. Biểu thức `1 + 2` có kiểu `Int`, điều này nghĩa là giá trị mà biểu thức ước lượng thành sẽ thuộc về một tập hợp hơn 4 tỉ trị số mà máy tính hiểu là số "nguyên" (integer). Chúng ta xác định kiểu của một biểu thức mà *không* chạy nó, đó là lí do mà kiểu `Int` không cho ta biết giá trị cụ thể nào mà biểu thức ước lượng thành.

Trước khi chạy một chương trình Scala, ta phải *biên dịch* nó. Khâu biên dịch sẽ kiểm tra xem một chương trình có ý nghĩa hay không. Nó phải đúng về mặt cú phép; nghĩa là nó phải được viết theo các quy tắc của Scala. Chẳng hạn, `(1 + 2)` là đúng cú pháp, nhưng `(1 + 2` thì không vì thiếu mất dấu đóng ngoặc `)` ứng với dấu mở ngoặc `(`. Khâu biên dịch cũng *kiểm tra kiểu*, nghĩa là các kiểu dữ liệu phải đúng với các phép toán mà ta định thực hiện. `1 + 2` vượt qua phép kiểm tra này (vì ta cộng hai số nguyên), nhưng `1.toUpperCase` thì không (chẳng có khái niệm chữ in hay chữ thường cho số nguyên cả.)

Chỉ những chương trình nào biên dịch thành không mới chạy được. Ta có thể hình dung việc biên dịch giống như các quy tắc ngữ pháp trong văn chương. Câu viết "FaRf  fjrmn;l df.fd"
không hợp với cú pháp tiếng Anh. Cách sắp xếp các chữ cái không tạo nên bất kì từ nào. Còn câu "dog fly a here no" thì gồm các từ tiếng Anh hợp lệ nhưng cách sắp xếp của chúng lại phá vỡ quy tắc ngữ pháp---tương tự như khâu kiểm tra kiểu dữ liệu mà Scala tiến hành.

Cần nhớ rằng việc kiểm tra kiểu được thực hiện trước khi chương trình chạy. Nếu bạn đã dùng một ngôn ngữ như Python hay Javascript, vốn đôi khi được gọi là "định kiểu động", thì không có sự kiểm tra kiểu trước khi chương trình chạy. Trong một ngôn ngữ "định kiểu tĩnh" như Scala, việc kiểm tra kiểu sẽ giúp ta bắt được một số lỗi tiềm tàng trước cả khi ta chạy mã lệnh này. Trong một ngôn ngữ định kiểu động, cái mà đôi khi được gọi là kiểu lại *không phải* là kiểu dữ liệu mà ta đang hiểu. Đối với ta thì kiểu dữ liệu tồn tại khi một chương trình được biên dịch, mà ta sẽ gọi là *thời gian biên dịch*. Còn khi một chương trình chạy, mà ta gọi là *thời gian chạy*, ta chỉ có những giá trị thôi. Các giá trị có thể ghi lại những thông tin về kiểu của biểu thức đã tạo ra chúng. Nếu có, thì ta sẽ gọi chúng là các *thẻ*, hoặc đôi lúc là *hộp*. Song không phải giá trị nào cũng đính thẻ hoặc đóng hộp được. Việc tránh gắn thẻ, hay còn gọi là *xóa kiểu*, cho phép ta viết những chương trình hiệu quả hơn.
