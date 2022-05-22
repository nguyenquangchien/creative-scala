## Ngữ nghĩa phương thức

Bây giờ khi đã biết cách khai báo phương thức, ta hãy quay trở lại ngữ nghĩa.
Làm thế nào để hiểu được một lời gọi phương thức theo mô hình thay thế vừa xét?

Ta đã biết rằng có thể thay thế một lời gọi phương thức bởi giá trị mà nó ước lượng thành.
Tuy nhiên, ta cần có một mô hình tinh chỉnh hơn để có thể tính ra xem giá trị này sẽ là gì.
Mô hình mở rộng này như sau: khi thấy một lời gọi phương thức, ta sẽ lập nên một khối mới và trong khối này:
gắn các tham số vào những biểu thức tương ứng cho trong lời gọi phương thức và thay thế vào phần thân phương thức.

Khi đó, ta có thể áp dụng mô hình thay thế như thường.

Hãy cùng xem một ví dụ đơn giản.
Cho trước phương thức 

```scala mdoc:silent
def square(x: Int): Int =
  x * x
```

ta có thể khai triển lời gọi phương thức này

```scala mdoc:silent
square(2)
```

bằng cách giới thiệu một khối

```scala mdoc:silent
{
  square(2)
}
```

để gắn tham số `x` vào với biểu thức `2`

```scala mdoc:silent
{
  val x = 2
  square(2)
}
```

và thay thế phần thân phương thức 

```scala mdoc:silent
{
  val x = 2
  x * x
}
```

Bây giờ ta có thể thực hiện thay thế như thường để có 

```scala mdoc:silent
{
  2 * 2
}
```

và sau cùng

```scala mdoc:silent
{
  4
}
```

Một lần nữa ta thấy rằng có sự thay thế nhưng không có riêng bước nào là khó cả.


### Bài tập {-}

Lân trước khi xét đến thay thế, ta đã dành nhiều thời gian khảo sát thứ tự ước lượng.
Trong đoạn mô tả trên ta đã quyết định rằng phải ước lượng các đối số của phương thức trước khi ước lượng phần thân.
Đây không phải là khả năng duy nhất.
Chẳng hạn, ta có thể ước lượng những đối số của phương thức chỉ vào lúc cần tới. Bằng cách này sẽ giúp ta tiết kiệm chút thời gian nếu phương thức không dùng đến một trong những tham số. 
Bằng cách dùng công cụ `println`, hãy xác định xem khi nào các tham số phương thức được ước lượng trong Scala.

<div class="solution">
Chương trình sau cho thấy rằng các tham số được ước lượng trước khi tiến vào phần thân phương thức.

```scala mdoc
def example(a: Int, b: Int): Int = {
  println("In the method body!")
  a + b
}

example({ println("a"); 1 }, { println("b"); 2 })
```

Phương án mà chúng tôi mô tả ở trên đã có ngôn ngữ dùng đến, tiêu biểu là Haskell, và cách này được gọi là ước lượng (lười) nhác hay không nghiêm.
</div>
