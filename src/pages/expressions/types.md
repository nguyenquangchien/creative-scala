## Kiểu dữ liệu

Bây giờ khi có thể viết được những biểu thức rồi, ta có thể nói thêm mọt chút về các kiểu dữ liệu.

Một tác dụng của kiểu dữ liệu là giúp ta tránh gọi những phương thức chưa từng tồn tại. Kiểu của biểu thức cho trình biên dịch biết những phương thức nào mà nó ước lượng thành. Mã lệnh ta viết sẽ không biên dịch nếu như ta cố gọi một phương thức không tồn tại. Sau đây là vài ví dụ đơn giản.

```scala mdoc:fail
"Brontë" / "Austen"
1.take(2)
```

Kiểu dữ liệu của biểu thức chính là thứ quy định xem ta có thể gọi các phương thức nào; ta có thể cho thấy điều này bằng việc gọi các phương thức đối với kết quả của những biểu thức phức tạp hơn.

```scala mdoc:fail
(1 + 3).take(1)
```

Quy trình *kiểm tra kiểu* này cũng có tác dụng với các tham số của phương thức.

```scala mdoc:fail
1.min("zero")
```

Là một thuộc tính của biểu thức, kiểu dữ liệu tồn tại lúc biên dịch (như ta đã thảo luận từ trước.) Điều này có nghĩa là ta có thể xác định kiểu của một biểu thức ngay cả khi nó ước lượng thành một kết quả lỗi lúc chạy chương trình. Chẳng hạn, khi chia một `Int` cho số không sẽ gây ra lỗi lúc chạy.

```scala mdoc:crash
1 / 0
```

Biểu thức `1 / 0` vẫn có kiểu dữ liệu, và ta tìm được kiểu này trong console như dưới đây.

```scala
:type 1 / 0
// Int
```

Ta cũng có thể viết một biểu thức phức hợp có chứa biểu thức con sẽ gây lỗi lúc thời gian chạy.

```scala mdoc:crash
(2 + (1 / 0) + 3)
```

Biểu thức này cũng có kiểu dữ liệu.

```scala
:type (2 + (1 / 0) + 3)
// Int
```
