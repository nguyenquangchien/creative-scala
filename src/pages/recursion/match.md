## Biểu thức khớp

Ở mục trước ta đã thấy biểu thức khớp `match` 

```scala
count match {
  case 0 => Image.empty
  case n => aBox.beside(boxes(n-1))
}
```

Ta sẽ hiểu loại biểu thức mới này sao đây, 
và tự viết nó bằng cách nào?
Hãy cùng mổ xẻ biểu thức này.

Trước hết phải nói rằng `match` là biểu thức thực sự, 
nghĩa là nó lượng giá thành một giá trị.
Nếu không thì phương thức `boxes` đã chẳng hoạt động được!

Để hiểu được nó lượng giá thành cái gì, ta cần thêm chi tiết. 
Một biểu thức `match` thường có dạng sau

```scala
<anExpression> match {
  case <pattern1> => <expression1>
  case <pattern2> => <expression2>
  case <pattern3> => <expression3>
  ...
}
```

`<anExpression>`, mà cụ thể là `count` ở ví dụ trên, là biểu thức mà lượng giá thành giá trị ta đang khớp nó với.
Dạng mẫu `<pattern1>` và v.v. được khớp với giá trị này.
Đến giờ ta đã thấy hai loại dạng mẫu:

 - nguyên văn (như ở `case 0`) sẽ khớp chính xác với giá trị mà nguyên văn đó lượng giá thành; và
 - đại diện (như ở `case n`) sẽ khớp với *thứ bất kì*, và hình thành gắn kết ngay trong biểu thức vế phải.

Cuối cùng, các biểu thức vế phải, `<expression1>` và v.v. chỉ là biểu thức như mọi biểu thức khác mà ta đã viết tới giờ.
bộ biểu thức `match` lượng giá thành giá trị biểu thức vế phải của dạng mẫu *đầu tiên* mà nó khớp được.
Bởi vậy khi ta gọi `boxes(0)`, cả hai dạng mẫu đều sẽ khớp (vì cái đại diện khớp được mọi thứ), nhưng vì dạng mẫu nguyên văn lại đứng trước nên biểu thức `Image.empty` sẽ được ước lượng.

Một biểu thức `match` mà kiểm tra toàn bộ trường hợp khả dĩ thì được gọi là khớp triệt để.
Nếu ta có thể cho rằng `count` luôn lớn hơn hoặc bằng không, thì `match` trong `boxes` chính là phép khớp triệt để.

Một khi đã quen với các biểu thức `match`, ta cần nhìn vào cấu trúc các số nguyên trước khi có thể giải thích đệ quy cấu trúc lên chúng.


### Bài tập {-}

#### Đoán kết quả {-}

Hãy cùng kiểm tra hiểu biết của mình về phép khớp bằng cách đoán từng biểu thức sau sẽ lượng giá thành cái gì, và tại sao.

```scala mdoc:silent
"abcd" match {
  case "bcde" => 0
  case "cdef" => 1
  case "abcd" => 2
}
```

```scala mdoc:fail:silent
1 match {
  case 0 => "zero"
  case 1 => "one"
  case 1 => "two"
}
```

```scala mdoc:fail:silent
1 match {
  case n => n + 1
  case 1 => 1000
}
```

```scala mdoc:fail:silent
1 match {
  case a => a
  case b => b + 1
  case c => c * 2
}
```

<div class="solution">

Ví dụ thứ nhất lượng giá thành `2`, vi trong số các dạng mẫu, chỉ có duy nhất `"abcd"` là khớp được nguyên mẫu `"abcd"`.

Ví dụ thứ hai lượng giá thành `"one"`, vi trường hợp khớp đầu tiên chính là cái được ước lượng.

Ví dụ thứ nhất lượng giá thành `2`, vì `case n` định nghĩa một dạng mẫu đại diện khớp được mọi thứ.

Ví dụ cuối lượng giá thành `1` vì trường hợp khớp đầu tiên được ước lượng.
</div>

#### Không khớp {-}

Điều gì sẽ xảy ra nếu không dạng mẫu nào khớp trong biểu thức `match`?
Hãy thử đoán, rồi viết một biểu thức `match` mà không khớp được để xem liệu bạn có đoán đúng không.
(Đến đây, ta không có lí do nào để lường trước một ứng xử cụ thể bởi vậy đoán cách nào hợp lý cũng được hết.)

<div class="solution">
Sau đây là ba khả năng khả dĩ mà tôi nghĩ được; có lẽ bạn sẽ nghĩ đến điều khác?

 - Biểu thức có thể ước lượng thành một giá trị mặc định nào đó, như `Image.empty` (nhưng Scala sẽ chọn mặc định thế nào là đúng đắn?)
 - Trình biên dịch Scala sẽ không cho phép bạn viết mã lệnh như vậy.
 - Biểu thức `match` sẽ thất bại khi thực thi.

Dưới đây là biểu thức khớp thất bại.

```scala mdoc:crash
2 match {
  case 0 => "zero"
  case 1 => "one"
}
```

Đáp án đúng là một trong hai khả năng cuối, hoặc không biên dịch được hoặc thất bại lúc thực thi.
Ở ví dụ này ta bị lỗi thực thi. 
Câu trả lời chính xác phụ thuộc vào việc Scala được cấu hình ra sao (ta có thể bảo trình biên dịch từ chối biên dịch các biểu thức khớp mà nó cho thấy rằng chúng không triệt để, song đây không phải là cách ứng xử mặc định).
</div>
