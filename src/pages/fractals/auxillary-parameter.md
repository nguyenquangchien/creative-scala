## Tham số phụ trợ 

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
val aBox = Image.square(20).fillColor(Color.royalBlue)
```

Ta đã thấy cách dùng đệ quy cấu trúc trên số tự nhiên để viết những chương trình thú vị. 
Ở mục này ta sẽ tìm hiểu bằng cách nào các *tham số phụ trợ* cho phép ta viết những chương trình phức tạp hơn.
Một tham số phụ trợ chỉ là một tham số bổ sung thêm vào phương thức của ta để cho phép truyền thêm thông tin vào lời gọi đệ quy.

Chẳng hạn, hãy hình dung việc tạo nên hình ở [@fig:recursion:growing-boxes], trong đó cho thấy một hàng các ô có kích thước tăng dần khi đi dọc theo hàng này.

![Các ô kích thước tăng dần theo từng lần đệ quy.](./src/pages/recursion/growing-boxes.pdf+svg){#fig:recursion:growing-boxes}

Làm thế nào để tạo nên hình này?

Ta biết rằng phải là một đệ quy cấu trúc trên các số tự nhiên, bởi vậy ta có thể lập tức viết ra khung mã lệnh sau 

```scala
def growingBoxes(count: Int): Image =
  count match {
    case 0 => base
    case n => unit add growingBoxes(n-1)
  }
```

Dùng những gì đã học được từ các `boxes` trước đây, ta có thể phát triển thêm và viết ra 

```scala
def growingBoxes(count: Int): Image =
  count match {
    case 0 => Image.empty
    case n => Image.square(???).beside(growingBoxes(n-1))
  }
```

Bây giờ thách thức sẽ là: bằng cách nào khiến cho các ô lớn lên khi ta đi qua phải.

Có hai cách làm việc này.
Cách mẹo mực là chuyển trật tự trường hợp đệ quy và đặt kích thước của ô là một hàm phụ thuộc vào `n`.
Sau đây là mã lệnh.

```scala mdoc:silent
def growingBoxes(count: Int): Image =
  count match {
    case 0 => Image.empty
    case n => growingBoxes(n-1).beside(Image.square(n*10))
  }
```

Hãy dành chút thời gian để hình dung tại sao mã lệnh này phát huy tác dụng, trước khi xem cách làm bằng tham số phụ trợ.

Một phương án khác, đơn giản là ta thêm một tham số nữa vào `growingBoxes` để báo cho ta biết ô hiện tại kích cỡ bao nhiêu.
Khi đệ quy, ta sẽ thay đổi kích cỡ này.
Sau đây là mã lệnh.

```scala mdoc:silent
def growingBoxes(count: Int, size: Int): Image =
  count match {
    case 0 => Image.empty
    case n => 
      Image
        .square(size)
        .beside(growingBoxes(n-1, size + 10))
  }
```

Ở phương thức có tham số phụ trợ, có hai ưu điểm: ta chỉ phải nghĩ cần có những thay đổi gì từ một lượt đệ quy này tới lượt kết tiếp (ở đây là ô lớn dần), và nó cho phép mã lệnh gọi thay đổi tham số này (chẳng hạn làm cho ô lớn hơn hay nhỏ đi).

Bây giờ khi đã thấy phương thức tham số phụ trợ, ta hãy cùng luyện tập sử dụng nó.

#### Các ô tô bóng {-}

Ở bài tập này, ta sẽ vẽ bức tranh như ở [@fig:recursion:gradient-boxes].
Ta đã biết cách vẽ một dãy các ô.
Thử thách ở bài tập này là làm cho màu sắc thay đổi theo từng bước.

Gợi ý: bạn có thể `spin` (quay) màu tô ở mỗi lượt đệ quy.

![Five boxes filled with changing colors starting from Royal Blue](./src/pages/recursion/gradient-boxes.pdf+svg){#fig:recursion:gradient-boxes}

<div class="solution">
Có hai cách triển khai giải pháp.
Phương thức tham số phụ trợ, đó là bổ sung thêm tham số vào `gradientBoxes` và truyền `Color` thông qua đệ quy cấu trúc.

```scala mdoc:silent
def gradientBoxes(n: Int, color: Color): Image =
  n match {
    case 0 => Image.empty
    case n =>
      aBox
        .fillColor(color)
        .beside(gradientBoxes(n - 1, color.spin(15.degrees)))
  }
```

Ta cũng có thể làm cho màu tô thành một hàm theo `n`, như đã thể hiện với kích cỡ ô trong `growingBoxes` nêu trên.

```scala mdoc:silent
def gradientBoxes(n: Int): Image =
  n match {
    case 0 => Image.empty
    case n =>
      aBox
        .fillColor(Color.royalBlue.spin((15 * n).degrees))
        .beside(gradientBoxes(n - 1))
  }
```
</div>

#### Các đường tròn đồng tâm {-}

Bây giờ ta hãy thử một biến thể của chủ đề này, vẽ các vòng tròn đồng tâm như ở [@fig:recursion:concentric-circles]. Ở đây ta đang thay đổi kích cỡ thay vì thay đổi màu của hình ở mỗi lượt. Còn ngoài ra, dạng mẫu vẫn y nguyên như vậy. Ta hãy triển khai mã lệnh nhé.

![Các vòng tròn đồng tâm, tô màu Royal Blue](./src/pages/recursion/concentric-circles.pdf+svg){#fig:recursion:concentric-circles}

<div class="solution">
Mã lệnh này gần như giống hệt `growingBoxes`.

```scala mdoc:silent
def concentricCircles(count: Int, size: Int): Image =
  count match {
    case 0 => Image.empty
    case n => 
      Image
        .circle(size)
        .on(concentricCircles(n-1, size + 5))
  }
```
</div>

#### Một lần nữa, với cảm xúc {-}

Bây giờ hãy kết hợp cả hai kĩ thuật để đổi kích cỡ và màu trong từng bước, cho ta kết quả như ở [@fig:recursion:colorful-circles].
Hãy thử nghiệm đến khi thu được kết quả như bạn mong muốn.

![Các vòng tròn đồng tâm với màu sắc thay đổi thú vị](./src/pages/recursion/colorful-circles.pdf+svg){#fig:recursion:colorful-circles}

<div class="solution">
Đây là giải pháp của chúng tôi, trong đó cố gắng phân chia bài toán thành những phần có thể tái sử dụng và giảm lượng mã lệnh lặp lại.
Vẫn còn nhiều chỗ mã lệnh lặp lại vì ta chưa có trong tay những công cụ làm giảm thiểu sự lặp lại.
Ta sẽ tìm hiểu vấn đề này sớm sau đây.

```scala mdoc:silent
def circle(size: Int, color: Color): Image =
  Image.circle(size).strokeWidth(3.0).strokeColor(color)

def fadeCircles(n: Int, size: Int, color: Color): Image =
  n match {
    case 0 => Image.empty
    case n => 
      circle(size, color)
        .on(fadeCircles(n-1, size+7, color.fadeOutBy(0.05.normalized)))
  }

def gradientCircles(n: Int, size: Int, color: Color): Image =
  n match {
    case 0 => Image.empty
    case n => 
      circle(size, color)
        .on(gradientCircles(n-1, size+7, color.spin(15.degrees)))
  }

def image: Image =
  fadeCircles(20, 50, Color.red)
    .beside(gradientCircles(20, 50, Color.royalBlue))
```
</div>
