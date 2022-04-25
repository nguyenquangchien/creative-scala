## Giá trị cũng là đối tượng

Trong Scala, tất cả giá trị đều là *đối tượng*. Một đối tượng là tập hợp gồm dữ liệu và các phép tính trên dữ liệu đó. Chẳng hạn, 2 là một đối tượng. Dữ liệu ở đây là số nguyên 2, còn các phép tính trên dữ liệu đó là những phép toán quen thuộc như +, -, v.v. Ta gọi các phép toán của một đối tượng là những *phương thức* của đối tượng đó. 

### Lời gọi phương thức

Ta tương tác với các đối tượng bằng cách *gọi* hay *kích hoạt* các phương thức. Chẳng hạn, ta có thể nhận được dạng chữ in của một chuỗi `String` bằng cách gọi phương thức `toUpperCase` của nó.

```scala mdoc
"Titan!".toUpperCase
```

Một số phương thức chấp nhận các *tham số* hay *đối số*, vốn kiểm soát cách hoạt động của phương thức này. Chẳng hạn, phương thức `take` lấy các kí tự từ một chuỗi `String`. Ta cần phải truyền tham số để cho `take` biết được ta cần bao nhiêu kí tự.

```scala mdoc
"Gilgamesh went abroad in the world".take(3)
"Gilgamesh went abroad in the world".take(9)
```

Một lời gọi phương thức cũng là một biểu thức, và do vậy sẽ ước lượng thành một đối tượng. Điều đó nghĩa là ta có thể nối các lời gọi lại với nhau để tạo thành chương trình phức tạp hơn:
```scala mdoc
"Titan!".toUpperCase.toLowerCase
```

<div class="callout callout-info">
#### Cú pháp lời gọi phương thức {-}

Cú pháp của một lời gọi phương thức là

```scala
anExpression.methodName(param1, ...)
```

hay

```scala
anExpression.methodName
```

trong đó

- `anExpression` là một biểu thức bất kì (sẽ ước lượng thành một đối tượng)
- `methodName` là tên của phương thức
- các `param1, ...` đều tùy chọn; đó là những biểu thức lước lượng thành các tham số cho phương thức.
</div>


### Toán tử

Ta đã nói rằng tất cả các giá trị đều là đối tượng, và ta kích hoạt các phương thức theo cú pháp `object.methodName(parameter)`. Như vậy, sẽ phải giải thích những biểu thức như `1 + 2` ra sao đây?

Trong Scala, một biểu thức có dạng `a.b(c)` cũng có thể được viết thành `a b c`. Bởi vậy, hai dòng sau là tương đương:

```scala mdoc
1 + 2
1.+(2)
```

Cách thứ nhất gọi phương thức như trên có tên là kiểu *toán tử*.

<div class="callout callout-info">

#### Kí pháp toán tử trung tố {-}

Bất kì biểu thức Scala nào có dạng `a.b(c)` thì cũng viêt được dưới dạng `a b c`.

Lưu ý rằng `a b c d e` thì tương đương với `a.b(c).d(e)`, chứ không phải `a.b(c, d, e)`.
</div>
