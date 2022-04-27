## IntelliJ

IntelliJ là một môi trường phát triển tích hợp (integrated development environment, IDE) cho Scala và những ngôn ngữ lập trình khác. Nó tích hợp một loạt công cụ lập trình vào trong một ứng dụng, và chúng tôi gợi ý nó cho các bạn đang sử dụng các IDE khác như Visual Studio hay Eclipse.

Để bắt đầu, hãy [downloading][intellij-download] và cài đặt IntelliJ. Bạn có thể sử dụng phiên bản cộng đồng miễn phí để luyện tập Scala Sáng tạo. Khi cài đặt IntelliJ bạn sẽ phải trả lời nhiều câu hỏi. Đa số các câu, bạn có thể chấp nhận phương án mặc định. Khi được hỏi về các trình cắm điển hình ("featured plugins"), *hãy chắc rằng bạn cài đặt trình cắm Scala*.

Một khi bạn đã hoàn thành cấu hình đó, bạn sẽ thấy một hộp thoại hỏi rằng liệu bạn có muốn tạo một dự án mới, nhập một dự án, mở một file, hoặc kiểm soát check out từ hệ thống kiểm soát phiên bản (version control).
Hãy chọn "checkout from version control", rồi chọn GitHub.

Trong hộp thoại mở ra, hãy chuyển "Auth type" thành Token.
Bây giờ thì dùng trình duyệt tới trang web GitHub.
Chọn tài khoản của bạn (góc phải phía trên trang web).
Chọn cài đặt "Settings" tiếp đến là Vé truy cập cá nhân "Personal access tokens".
Chọn một vé (token). Đặt tên nó là "intellij" rồi tick vào ô "repo".
Copy chuỗi số dài rồi dán vào ô "Token".
Bây giờ hãy đăng nhập vào GitHub.

Tiếp theo, cài đặt phần mở rộng (add-on) cửa sổ lệnh SBT console.

[intellij-download]: https://www.jetbrains.com/idea/download/
