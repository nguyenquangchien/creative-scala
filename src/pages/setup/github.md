## GitHub

Chúng tôi đã tạo ra một [bản mẫu (template)] để giúp bạn có thể thiết lập tất cả mã lệnh mà bạn cần để luyện tập cho toàn bộ đợt học Scala Sáng tạo.
Bản mẫu này được lưu trên [GitHub][github], một website giúp việc chia sẻ mã lệnh.

Bạn có thể sao chép bản mẫu về máy của bạn, việc này gọi là sao chép (cloning) Git, nhưng cũng đồng nghĩa với việc bạn không thể lưu trữ bất kì sửa đổi nào đã thực hiện trở lại GitHub nơi mọi người xem được những sửa đổi đó.

Nếu muốn chia sẻ những sửa đổi đã thực hiện, bạn cần phải nhân bản cái bản mẫu dự án trên tài khoản GitHub của bạn.
Việc nhân bản này được Git gọi là "forking".
Bạn nhân bản mã lệnh trên GitHub rồi sau đó nhân bản *cái bản fork đó* về máy tính.
Từ khi đó, bạn có thể lưu những sửa đổi mà bạn thự hiện vào bản fork của mình trên GitHub.

Để bắt đầu quá trình này, bạn cần tạo một tài khoản GitHub nếu chưa có sẵn.

Một khi đã có tài khoản rồi, bạn hãy thăm [dự án mẫu](https://github.com/creativescala/creative-scala-template) trong trình duyệt của bạn. Ở góc trên tay phải có một nút bấm tên là "Fork". Hãy ấn nút này để tạo một bản sao từ bản mẫu cho riêng bạn. Trình duyệt sẽ dẫn bạn tới một trang web hiển thị bản sao mẫu riêng của bạn. Hãy nhớ tên của bản mã lệnh này. Nó sẽ có tên gọi kiểu như `yourname/creative-scala-template` trong đó `yourname` là tên người dùng GitHub của bạn.

Bây giờ việc sao chép nhân bản của bạn sẽ chỉ đơn giản như là chạy câu lệnh dưới đây và thay thế `yourname` bằng tên người dùng GitHub thật của bạn.

```bash
git clone git@github.com:yourname/creative-scala-template.git
```

Bây giờ bất kì thay đổi nào bạn thực hiện đều được gửi trở lại bản sao của bạn trên GitHub.
Quá trình thực hiện điều này trong Git sẽ khá phức tạp.
Mỗi khi thực hiện một thay đổi, bạn phải:

  - `add` - bổ sung thay đổi vào cái mà ta gọi là chỉ số (index) của Git;
  - `commit` - chấp nhận thay đổi; và sau cùng
  - `push` - đẩy thay đổi này vào bản sao.

Sau đây là một ví dụ mà ta thực hiện bằng dòng lệnh.

```bash
git add
git commit -m "Explain here what you did"
git push
```

GitHub tạo ra một công cụ đồ họa miễn phí tuyệt vời bằng Git, gọi là [GitHub Desktop](https://desktop.github.com/).
Có lẽ đây là cách dễ nhất để sử dụng Git với những người mới bắt đầu như bạn.

[github]: https://github.com/
[template]: https://github.com/underscoreio/creative-scala-template
