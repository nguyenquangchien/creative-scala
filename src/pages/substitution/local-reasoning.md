## Suy luận cục bộ

Ta đã thấy rằng thứ tự ước lượng chỉ thực sự quan trọng khi ta có hiệu ứng phụ.
Chẳng hạn, nếu các biểu thức sau tạo ra hiệu ứng phụ

```scala
disableWarheads()   # vô hiệu hóa đầu đạn
launchTheMissles()  # phóng tên lửa
```

Ta thực sự muốn đảm bảo chắc rằng các biểu thức được ước lượng từ trên xuống dưới để cho các đầu đạn bị vô hiệu hóa trước khi tên lửa được phóng ra.

Tất cả chương trình hữu ích phải có một hiệu ứng nào đó, vì hiệu ứng chính là cách mà chương trình tương tác với thế giới bên ngoài.
Hiệu ứng có thể chỉ là in ra thứ gì đó khi chương trình kết thúc và nội dung đó vẫn còn hiện.
Làm giảm thiểu hiệu ứng phụ là mục tiêu then chốt của lập trình hàm, vì vậy ta sẽ nói thêm về chủ đề này.

Thay thế thì rất dễ hiểu.
Khi thứ tự ước lượng không quan trọng, điều đó nghĩa là bất kì mã lệnh nào khác cũng không làm thay đổi ý nghĩa đoạn mã lệnh mà ta đang xét.
`1 + 1` thì luôn bằng `2`, bất kể mã lệnh khác trong chương trình có thế nào đi nữa. Nhưng hiệu ứng của `launchTheMissles()` thì lại phụ thuộc vào liệu ta đã vô hiệu hóa đầu đạn chưa.

Kết cục của điều này là mã lệnh thuần khiết có thể hiểu được biệt lập.
Vì không có mã nào khác có thể làm thay đổi ý nghĩa của nó nên nếu ta chỉ quan tâm đến một đoạn mã thì có thể bỏ qua phần còn lại.
Mặt khác, ý nghĩa của mã lệnh không thuần lại phụ thuộc vào tất cả mã lệnh mà đã được chạy trước khi nó ước lượng.
Đặc tính này được gọi là *suy luận cục bộ*.

Mã lệnh thuần khiết có đặc tính này, nhưng mã không thuần thì không.

Khi chương trình lớn dần, thì ta ngày càng khó nhớ được tất cả thông tin chi tiết.
Vì dung lượng mà ta ghi nhớ được chỉ là cố định thôi nên giải pháp duy nhất là giới thiệu khái quát hóa.
Lại nhớ rằng khái quát hóa là việc lược bỏ các chi tiết không liên quan.
Mã thuần khiết là khái quát hóa ở mức cao nhất, vì nó cho ta biết rằng mọi chi tiết khác đều là không liên quan.
Đây là một trong số những đặc tính khiến giới lập trình hàm phấn khởi: khả năng làm cho các chương trình lớn trở nên dễ hiểu.
Lập trình hàm không có nghĩa là tránh các hiệu ứng, vì mọi chương trình hữu ích đều có hiệu ứng.
Tuy nhiên, nó có nghĩa là kiểm soát các hiệu ứng để cho phần lớn mã lệnh đều có thể suy luận được bằng mô hình thay thế đơn giản.


### Ý nghĩa của ý nghĩa

Đến giờ, ta đã nói nhiều về ý nghĩa của mã lệnh, trong đó ta nói "ý nghĩa" là để chỉ kết quả ước lượng thành, và có thể là hiệu ứng phụ mà mã lệnh đó thực hiện.

Trong phép thay thế, ý nghĩa của chương trình chính là kết quả mà chương trình ước lượng thành.
Như vậy hai chương trình sẽ bằng nhau nếu chúng ước lượng thành cùng kết quả.
Đây chính là lí do tại sao hiệu ứng phụ lại phá vỡ sự thay thế: trong mô hình thay thế không có khái niệm về hiệu ứng phụ và do vậy không thể phân biệt nổi hai chương trình chỉ khác nhau bởi hiệu ứng phụ.

Chương trình còn có thể khác nhau theo những cách khác.
Chẳng hạn, một chương trình này có thể chạy lâu hơn chương trình kia để cho ra cùng kết quả.
Một lần nữa, phép thay thế không thể phân biệt nổi chúng.

Thay thế là một cách khái quát hóa, và ngoài kết quả ra thì mọi chi tiết khác đều bị bỏ đi.
Hiệu ứng phụ, thời gian và lượng bộ nhớ sử dụng đều không liên quan tới thay thế, nhưng có lẽ lại đáng quan tâm đối với những người viết hoặc chạy chương trình.
Ở đây luôn có sự đánh đổi.
Ta có thể dùng những mô hình phức tạp hơn để nắm bắt thêm được những chi tiết này, song mô hình như vậy lại khó dùng hơn.
Với đa số người dùng, hầu như lúc nào phép thay thế cũng sẽ là sự đánh đổi hợp lý; nó rất dễ dùng đồng thời vãn còn hữu ích.
