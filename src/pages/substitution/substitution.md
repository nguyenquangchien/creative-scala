## Thay thế

Luật thay thế nói rằng mỗi khi thấy một biểu thức, ta có thể thay thế nó bằng giá trị mà biểu thức ước lượng thành. Chẳng hạn, khi thấy

```scala mdoc:silent
1 + 1
```

thì ta có thể thay thế nó bằng  `2`.
Tiếp theo, điều này nghĩa là khi thấy một biểu thức phức hợp như

```scala mdoc:silent
(1 + 1) + (1 + 1)
```

thì ta có thể thay thế `2` cho `1 + 1` và nhận được

```scala mdoc:silent
2 + 2
```

vốn ước lượng thành `4`.

Cách suy luận này chính là trong lúc ta rút gọn biểu thức đại số khi học phổ thông. 
Dĩ nhiên, giới khoa học máy tính lại có từ ngữ đao to búa lớn để chỉ quá trình này.
Ngoài thay thế, ta có thể gọi nó là *rút gọn biểu thức*, hay *suy luận phương trình*.

Thay thế giúp ta cách suy luận về chương trình, chính là cách nói khác cho
"hình dung ra xem chương trình làm điều gì".
Ta có thể áp dụng thay thế cho bất kì biểu thức nào ta đã thấy.
Để cho dễ, ở đây ta sẽ dùng ví dụ với các số và chuỗi thay vì hình, vậy ta sẽ trở lại một ví dụ từng gặp ở chương trước:

```scala mdoc:silent
1 + ("Moonage daydream".indexOf("N"))
```

Ở ví dụ trước ta đã có phần cẩu thả.
Bây giờ ta sẽ chuẩn chỉ hơn để minh họa được các bước mà máy tính cần đi qua.
Dù sao đi nữa, ta cũng cố thử mô phỏng lại máy tính.

Biểu thức chứa dấu `+` bao gồm 2 biểu thức con, đó là `1` và `("Moonage daydream".indexOf("N"))`.
Ta cần phải quyết định xem biểu thức nào cần ước lượng trước: bên trái hay bên phải.
Hãy cùng chọn tùy ý biểu thức con bên phải (rồi sau đây ta còn quay lại lựa chọn này.)

Biểu thức con `("Moonage daydream".indexOf("N"))` một lần nữa lại chứa hai biểu thức con khác, `"Moonage daydream"` và `"N"`.
Hãy lại ước lượng bên phải trước, nhớ rằng các biểu thức nguyên văn không phải là giá trị và chúng phải được ước lượng.

Nguyên văn `"N"` ước lượng thành `"N"`.
Để tránh sự nhầm lần này ta hãy viết giá trị là `|"N"|`.
Bây giờ ta có thể thay thế giá trị này vào biểu thức đã cho ở những bước đầu tiên

```scala
1 + ("Moonage daydream".indexOf(|"N"|))
```

Đến đây, ta có thể ước lượng được phần bên trái của biểu thức con, thay thế biểu thức nguyên văn `"Moonage daydream"` bởi giá trị của nó `|"Moonage daydream"|`.
Bằng cách này ta có

```scala
1 + (|"Moonage daydream"|.indexOf(|"N"|))
```

Tình huống bây giờ là cần ước lượng toàn biểu thức `(|"Moonage daydream"|.indexOf(|"N"|))`, vốn sẽ ước lượng thành `|-1|` (một lần nữa, ta phân biệt giá trị số nguyên với biểu thức nguyên văn bằng cách dùng các vạch đứng).
Và ta lại thực hiện thay thế để thu được

```scala
1 + |-1|
```

Đến đây ta cần ước lượng phần bên trái, là nguyên văn `1`, thu được `|1|`.
Thực hiện thay thế để có

```scala
|1| + |-1|
```

Và ta có thể ước lượng toàn biểu thức để nhận được

```scala
|0|
```

Bây giờ ta có thể yêu cầu Scala ước lượng toàn biểu thức để kiểm tra suy luận của mình.

```scala mdoc
1 + ("Moonage daydream".indexOf("N"))
```

Đúng rồi!

Đến đây ta có thấy một số điều sau:

 - thực hiện thay thế một cách bài bản như máy tính làm có thể tốn rất nhiều bước;
 - cách ước lượng tắt như bạn nhẩm tính có thể lại đem tới đáp số đúng; và
 - việc chọn ước lượng từ phải qua trái, vốn dường như tùy tiện, lại cho ta đáp số đúng.

Liệu có phải bằng cách nào đó ta đã chọn được thứ tự thay thế giống như Scala làm (không phải vậy, nhưng ta vẫn chưa điều tra kĩ việc này) hay liệu thứ tự mà ta chọn không thực sự quan trọng?
Chính xác là khi nào ta có thể làm tắt mà vẫn có thể thu được đáp số đúng, như ở ví dụ đầu tiên với phép cộng?
Ta sẽ xét kĩ những câu hỏi này ngay sau đây, song trước hết hãy cùng nói về cách mà phép thay thế làm việc với các tên.


### Các tên gọi

Luật thay thế đối với các tên là thay thế một tên bằng giá trị mà tên đó chỉ tới.
Ta đã ngầm áp dụng luật này rồi.
Bây giờ ta chỉ phát biểu quy củ thôi.

Chẳng hạn, với mã lệnh

```scala mdoc:silent
val name = "Ada"
name ++ " " ++ "Lovelace"
```

Ta có thể áp dụng thay thế để được

```scala mdoc:silent
"Ada" ++ " " ++ "Lovelace"
```

vốn sẽ ước lượng thành

```scala mdoc:silent
"Ada Lovelace"
```

Ta có thể dùng tên để được quy củ hơn trong việc thay thế.
Trở lại ví dụ đầu tiên

```scala mdoc:silent
1 + 1
```

ta có thể đặt cho biểu thức này một cái tên:

```scala mdoc:silent
val two = 1 + 1
```

Khi ta thấy một biểu thức phức hợp như 

```scala mdoc:silent
(1 + 1) + (1 + 1)
```

cách thay thế sẽ cho ta biết rằng có thể thay `two` cho `1 + 1` để có

```scala mdoc:silent
two + two
```

Hãy nhớ rằng khi phân tích biểu thức

```scala mdoc:silent
1 + ("Moonage daydream".indexOf("N"))
```

ta đã chia nó thành các biểu thức con vốn sẽ được ước lượng và thay thế.
Việc này nếu diễn đạt bằng từ sẽ khá rối rắm.
Chỉ bằng vài lệnh khai báo `val`, ta có thể làm gọn hơn và dễ thấy hơn.
Sau đây là chính biểu thức đó khi được chia thành các phần.

```scala mdoc:silent
val a = 1
val b = "Moonage daydream"
val c = "N"
val d = b.indexOf(c)
val e = a + d
```

Nếu tại lúc này, ta tùy ý quy định rằng việc ước lượng xảy ra từ trên xuống dưới, thì ta có thể thử nghiệm với các trật tự khác nhau để xem chúng dẫn tới những khác biệt ra sao.

Chẳng hạn,

```scala mdoc:reset:silent
val c = "N"
val b = "Moonage daydream"
val a = 1
val d = b.indexOf(c)
val e = a + d
```

đem tới kết quả giống hệt như trên.
Tuy nhiên ta không thể viết

```scala mdoc:reset:fail:silent
val e = a + d
val a = 1
val b = "Moonage daydream"
val c = "N"
val d = b.indexOf(c)
```

vì `e` phụ thuộc vào `a` và `d`, mà trong trật tự từ trên xuống dưới thì `a` và `d` vẫn chưa được ước lượng. 
Ta có quyền tranh luận rằng, kể cả thử nghiệm đi nữa thì điều này vẫn có vẻ ngốc nghếch. Toàn biểu thức mà ta cần ước lượng là  `e` nhưng `a` tới `d` lại là các biểu thức con của `e`, vậy dĩ nhiên ta phải ước lượng các biểu thức con trước khi ước lượng biểu thức lớn.
