## Biểu thức nguyên văn

Bây giờ ta hãy khám phá các dạng biểu thức khác nhau trong Scala, bắt đầu bằng loại đơn giản nhất, biểu thức *nguyên mẫu*. Sau đây là một biểu thức nguyên mẫu:

```scala mdoc
3
```

Biểu thức nguyên mẫu sẽ ước lượng thành "chính nó." Ta viết biểu thức nào thì console sẽ in ra giá trị hệt như vậy. Song cần nhớ rằng vẫn có sự khác biệt giữa hình thức viết của giá trị và cách biểu diễn nó trong bộ nhớ máy tính.

Scala có nhiều loại biểu thức nguyên văn. Ta đã thấy nguyên văn kiểu `Int`. Cũng có một loại khác, biểu thức nguyên văn với cú pháp khác, đó là *các số phẩy động*. Nó tương ứng với cách mà máy tính xấp xỉ một số thực. Sau đây là ví dụ:

```scala mdoc
0.1
```

Như bạn thấy, kiểu này được gọi là một `Double`.

Các số thì tốt rồi, nhưng còn chữ thì sao? Kiểu dữ liệu `String` biểu diễn cho một dãy các kí tự. Ta viết các chuỗi nguyên văn bằng cách đặt nội dung của chúng giữa cặp dấu nháy kép.

```scala mdoc
"To be fond of dancing was a certain step towards falling in love."
```

Đôi khi ta muốn viết các chuỗi chạy trên vài dòng khác nhau. Có thẻ làm điều này bằng cách dùng 3 dấu nháy kép, như sau.

```scala mdoc
"""
A new, a vast, and a powerful language is developed for the future use of analysis,
in which to wield its truths so that these may become of more speedy and accurate
practical application for the purposes of mankind than the means hitherto in our
possession have rendered possible.

  -- Ada Lovelace, the world's first programmer
"""
```

`String` là một dãy các kí tự. Bản thân kí tự lại có một kiểu riêng, đó là `Char`, và các nguyên mẫu kí tự được viết giữa cặp dấu nháy đơn.

```scala mdoc
'a'
```

Sau cùng, ta sẽ xem cách biểu diễn nguyên mẫu của kiểu `Boolean`, được đặt tên theo nhà logic học người Anh [George Boole](https://en.wikipedia.org/wiki/George_Boole). Tên gọi kiểu cách đơn giản là để chỉ những giá trị có thể là `true` (đúng) hoặc `false` (sai), và đây chính là cách mà ta viết các nguyên mẫu boolean.

```scala mdoc
true
false
```

Bằng các biểu thức nguyên mẫu, ta có thể tạo các giá trị, nhưng sẽ không có tác dụng gì nếu ta không thể thao tác trên các giá trị vừa tạo này. Ta đã thấy vài ví dụ về những biểu thức phức hợp như `1 + 2`. Ở mục kê tiếp, ta sẽ tìm hiểu về các đối tượng và phương thức, từ đó ta sẽ hiểu được biểu thức này cũng như các biểu thức thú vị khác, hoạt động ra sao.
