## Thông tin nền

Mục này đề cập một số thông tin nền về những công cụ mà chúng ta sẽ dùng.
Nếu bạn là người phát triển có kinh nghiệm thì đã thạo rồi và có thể bỏ qua.
Bằng không, hi vọng là mục sẽ giúp bạn một số manh mối có ích về phần mềm mà chúng ta sẽ làm việc trên đó.



### Cửa sổ dòng lệnh

Trở về thời trước đây khi mà tin học vẫn còn trong thuở sơ khai, giao diện cửa đồ hoạ thông dụng như bây giờ, trong đó người dùng chuột điều khiển con trỏ và tương tác bởi *thao tác trực tiếp* vẫn còn chưa tồn tại.
Hồi đó, người dùng phải gõ vào các câu lệnh trên thiết bị gọi là *thiết bị đầu cuối (terminal)*.
Thông thường, giao diện thao tác trực tiếp thì có ưu điểm vượt trội, song cũng có lúc thiết bị đầu cuối hay *dòng lệnh (command line)* lại tiện dụng hơn.
Chẳng hạn, nếu ta muốn biết tất cả những file có tên bắt đầu bằng chữ `data` đã chiếm mất bao nhiêu dung lượng ổ đĩa, thì trên hệ điều hành Linux hay OS X, ta có thể gõ vào lệnh

```bash
du -hs data*
```

Ta có thể tách câu lệnh trên thành 3 phần:

- tên lệnh `du` viết tắt từ disk usage (dung lượng đĩa sử dụng);
- các cờ `-hs` nghĩa là in tóm tắt thông tin để người dùng đọc được; và
- dạng mẫu `data*` nghĩa là tất cả những file nào có tên bắt đầu bằng `data`.

Nếu dùng giao diện thao tác trực tiếp, ta sẽ mất thời gian lâu hơn nhiều.

Để học sử dụng dòng lệnh, bắt đầu sẽ tốn nhiều thời gian, nhưng phần thưởng lại một công cụ vô cùng mạnh mẽ.
Trong cuốn này ta ít dùng cửa sổ dòng lệnh thôi, nên nếu bạn thấy "choáng" với ví dụ trên thì cũng đừng lo quá!


### Trình soạn file chữ

Có lẽ bạn đã quen với viết văn bản bằng trình xử lý văn bản rồi.
Một trình xử lý văn bản cho phép ta viết văn bản và kiểm soát định dạng để con chữ xuất hiện trên trang giấy như thế nào.
Một trình xử lý văn bản bao gồm các tính năng mạnh mẽ, như soát lỗi chính tả và tự động tạo mục lục, hay trợ giúp cho việc viết các đoạn thơ một cách dễ dàng hơn.

Một *trình soạn file chữ (text editor)* cũng tựa như trình xử lý văn bản, nhưng là đối với mã lệnh.
Nếu như trình xử lý văn bản quan tâm đến việc thể hiện hình thức của văn bản, thì trình soạn file chữ lại có nhiều tính năng cụ thể liên quan đến lập trình, điển hình có những công cụ mạnh giúp tìm kiếm và thay thế chữ, và khả năng nhanh chóng nhảy tới các phần khác nhau của file trong một dự án lập trình.

Các trình soạn chữ có từ thời của thiết bị đầu cuối và có lẽ thật ngạc nhiên là một số vẫn còn được dùng đến ngày nay.
Hai trình biên tập chữ cổ điển và huy hoàng vẫn còn tồn tại là Emacs và Vim.
Chúng có cách thức tiếp cận rất khác biệt và lập trình viên thường chỉ chọn một trong hai.
Tôi thì dùng Emacs khoảng 20 năm rồi, và trong lòng luôn coi Emacs là trình soạn chữ tốt nhất có thể có được, còn người dùng Vim thật ngốc nghếch với khiếu thẩm mĩ kém cùng một công cụ xoàng.
Ngược lại, chắc hẳn những người dùng Vim sẽ nghĩ điều tương tự về tôi.

Nếu có thứ gì hoà giải được hai nhóm người dùng Vim và Emacs, đó hẳn phải là hiểu biết rằng những trình soạn chữ hiện đại như Sublime Text và Atom đang đưa tới hồi kết của thời đại cuộc chiến giữa Vim và Emacs.
Dù sao thì chúng tôi cũng gợi ý bạn dùng Atom nếu bạn mới tham gia vào "cuộc chiến" trình soạn này.
Cả Vim và Emacs được tạo ra trước khi các giao diện thông dụng như hiện nay ra đời, và việc sử dụng chúng lại đòi hỏi một cách làm việc rất khác.


### Trình biên dịch

Mã lệnh mà ta viết trong một trình soạn chữ thì lại không thuộc dạng mà máy tính có thể thực hiện được.
Một *trình biên dịch* có nhiệm vụ dịch nó thành thứ mà máy tính có thể thực hiện được.
Khi dịch mã, trình biên dịch sẽ thực hiện những khâu kiểm tra nhất định đối với mã lệnh.
Nếu không vượt qua khâu kiểm tra này, mã lệnh sẽ không thể được biên dịch; thay vào đó trình biên dịch sẽ in ra một thông báo lỗi.
Trong phần còn lại cuốn sách này, chúng ta sẽ biết thêm rằng trình biên dịch có thể kiểm tra những gì và không thể kiểm tra những gì.

Khi chúng tôi nói rằng trình biên dịch sẽ dịch mã lệnh thành một thứ mà máy tính có thể chạy được, điều này không hoàn toàn đúng với trường hợp của Scala.
Sản phẩm đầu ra của trình biên dịch là thứ được gọi là mã byte (bytecode), và một chương trình khác có tên là máy ảo Java (Java Virtual Machine, JVM), sẽ chạy mã byte này[^complications].


### Môi trường phát triển tích hợp

Các môi trường phát triển tích hợp (integrated development environments, IDE) là một cách tiếp cận khác; ở đó một trình soạn chữ, một trình biên dịch, và vài công cụ lập trình khác được kết hợp vào thành một chương trình duy nhất.
Có người trông cậy hoàn toàn vào IDE, song cũng có người thích dùng cửa sổ lệnh và trình soạn chữ hơn.
Theo chúng tôi, nếu bạn mới lập trình thì nên chọn cách làm cửa sổ lệnh và trình soạn chữ.
Còn nếu bạn đã dùng quen IDE rồi thì IntelliJ IDEA hiện là IDE để phát triển chương trình Scala.


### Bộ kiểm soát phiên bản

Công cụ cuối cùng mà ta sẽ sử dụng là bộ kiểm soát phiên bản.
Một hệ thống kiểm soát phiên bản (version control system) là một chương trình cho phép ta ghi chép lại tất cả những thay đổi được thực hiện trên một nhóm tập tin.
Việc cho phép mọi người đồng thời cùng làm việc trong một dự án là rất cần thiết, và nó đảm bảo rằng mọi người không vô ý ghi đè lên những thay đổi của người khác.
Điều này không phải là mối quan tâm quá lớn trong Scala Sáng tạo, song ta nên bắt đầu tiếp xúc với kiểm soát phiên bản ngay từ bây giờ.

Phầm mềm kiểm soát phiên bản mà ta sẽ sử dụng được gọi là Git. Nó rất mạnh song phức tạp.
Một điều thuận lợi, đó là ta không cần phải học quá nhiều về Git.
Phần lớn việc sử dụng Git của ta sẽ thông qua một website có tên GitHub; nó cho phép mọi người chia sẻ phần mềm được lưu trong Git.
Ta sẽ dùng GitHub để chia sẻ phần mềm được sử dụng trong Scala Sáng tạo.


### Tiến lên!

Bây giờ khi đã có một vài kiến thức nền, ta hãy tiếp tục cài đặt phần mềm cần thiết để viết mã lệnh Scala.


[^complications]: Điều này bản thân nó không hoàn toàn đúng! Ta thường chạy mã lệnh Scala trên JVM, song thực ra thì ta có thể biên dịch Sala thành 3 định dạng khác nhau. Định dạng đầu tiên và cũng thông dụng nhất là mã byte (bytecode) JVM. Ta cuxgn có thể biên dịch thành Javascript, một ngôn ngữ lập trình khác vốn cho phép chạy các mã lệnh Scala trong một trình duyệt. Sau cùng, Scala Native sẽ biên dịch Scala thành một thứ mà máy tính *có thể* chạy được trực tiếp mà không cần tới JVM.
