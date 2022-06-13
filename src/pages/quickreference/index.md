\appendix

# Tham khảo nhanh về cú pháp {#syntax-quick-reference}

## Nguyên văn và biểu thức

```scala
// Các nguyên văn:
123      // Int
123.0    // Double
"Hello!" // String
true     // Boolean

// Toán:
10 + 2   // Int + Int    = Int
10 + 2.0 // Int + Double = Double
10 / 2   // Int / Int    = Double

// Logic Boole:
true && false // phép VÀ logic
true || false // phép HOẶC logic
!true         // phép phủ định logic

// Nối chuỗi:
"abc" + "def" // String
"abc" + 123   // tự động quy đổi từ Int sang String

// Lời gọi phương thức và toán tử trung tố:
1.+(2)    // cách gọi phương thức
1 + 2     // cách dùng toán tử trung tố
1 + 2 + 3 // tương đương với 1.+(2).+(3)

// Câu lệnh điều kiện:
if(biểuThứcBoole) biểuThứcA else biểuThứcB

// Khối lệnh:
{
  biểuThứcHiệuỨngPhụ1
  biểuThứcHiệuỨngPhụ2
  biểuThứcKếtQuả
}
```

## Khai báo các giá trị và phương thức

```scala
// Cú pháp khai báo giá trị:
val tênGiáTrị: Kiểu = biểuThứcKếtQuả     // khai báo với kiểu tường minh
val tênGiáTrị = biểuThứcKếtQuả           // khai báo với kiểu suy diễn

// Phương thức cùng danh sách tham số và kiểu trả lại tường minh:
def tênPhươngThức(tênĐốiSố: KiểuĐốiSố, tênĐốiSố: KiểuĐốiSố): KiểuTrảLại =
  biểuThứcKếtQuả

// Phương thức cùng danh sách tham số và kiểu trả lại suy diễn:
def tênPhươngThức(tênĐốiSố: KiểuĐốiSố, tênĐốiSố: KiểuĐốiSố) =
  biểuThứcKếtQuả

// Phương thức đa biểu thức (bằng cách dùng khối):
def tênPhươngThức(tênĐốiSố: KiểuĐốiSố, tênĐốiSố: KiểuĐốiSố): KiểuTrảLại = {
  biểuThứcHiệuỨngPhụ1
  biểuThứcHiệuỨngPhụ2
  biểuThứcKếtQuả
}

// Phương thức không có danh sách tham số:
def tênPhươngThức: KiểuTrảLại =
  biểuThứcKếtQuả

// Gọi một phương thức có danh sách tham số:
tênPhươngThức(đốiSố, đốiSố)

// Gọi một phương thức không có danh sách tham số:
tênPhươngThức
```

## Các hàm như giá trị

Giá trị hàm được viết là `(tênĐốiSố: KiểuĐốiSố, ...) => biểuThứcKếtQuả`:

```scala
val double = (num: Int) => num * 2
// double: Int => Int = <function1>

val sum = (a: Int, b: Int) => a + b
sum: (Int, Int) => Int = <function2>
```

Các hàm trên nhiều dòng được viết bằng cách dùng khối biểu thức:

```scala
val printAndDouble = (num: Int) => {
  println("Số đã cho là " + num)
  num * 2
}
// printAndDouble: Int => Int = <function1>

scala> printAndDouble(10)
// Số đã cho là 10
// res0: Int = 20
```

Ta phải viết kiểu hàm khi khai báo các tham số cùng kiểu trả lại.
Cú pháp là `KiểuĐốiSố => KiểuTrảLại` hoặc `(KiểuĐốiSố, ...) => KiểuTrảLại`:

```scala
def doTwice(value: Int, func: Int => Int): Int =
  func(func(value))
// doTwice: (value: Int, func: Int => Int)Int

doTwice(1, double)
// res0: Int = 4
```

Các giá trị hàm cũng có thể được viết trên một dòng như biểu thức thông thường:

```scala
doTwice(1, (num: Int) => num * 10)
// res1: Int = 100
```

Đôi khi ta bỏ qua kiểu đối số, 
và cho rằng trình biên dịch có thể giúp ta hình dung mọi thứ:

```scala
doTwice(1, num => num * 10)
// res2: Int = 100
```

## Hướng dẫn tham khảo Doodle

### Nhập thư viện

```scala
// Các dòng lệnh nhập này giúp bạn có mọi thứ cần thiết:
import doodle.core._
import doodle.syntax._
```

### Tạo các hình ảnh

```scala
// Các hình cơ bản (viền đen, không tô màu):
val i: Image = Circle(bánKính)
val i: Image = Rectangle(rộng, cao)
val i: Image = Triangle(rộng, cao)

// Các hình ghép được viết bằng cú pháp toán tử:
val i: Image = imageA beside imageB // đặt kề hướng ngang
val i: Image = imageA above  imageB // đặt kề hướng đứng
val i: Image = imageA below  imageB // đặt kề hướng đứng
val i: Image = imageA on     imageB // chồng xếp
val i: Image = imageA under  imageB // chồng xếp

// Các hình ghép được viết bằng cú pháp gọi phương thức:
val i: Image = imageA.beside(imageB)
// v.v...
```

### Dùng kiểu cách cho các hình

```scala
// Đặt kiểu cách bằng cú pháp toán tử:
val i: Image = image fillColor màu     // màu tô mới (không thay đổi màu viền)
val i: Image = image strokeColor màu   // màu viền mới (không thay đổi màu tô)
val i: Image = image strokeWidth integer // bề rộng đường mới (không thay đổi phần được tô)
val i: Image = image fillColor màu strokeColor màuKhác // màu tô và màu viền mới

// Đặt kiểu cách bằng cú pháp lời gọi hàm:
val i: Image = imageA.fillColor(màu)
val i: Image = imageA.fillColor(màu).strokeColor(màuKhác)
// v.v...
```

### Màu

```scala
// Các màu cơ bản:
val c: Color = Color.red                       // màu định sẵn
val c: Color = Color.rgb(255.uByte, 127.uByte, 0.uByte)          // màu RGB
val c: Color = Color.rgba(255.uByte, 127.uByte, 0.uByte, 0.5.normalized)    // màu RGBA
val c: Color = Color.hsl(15.degrees, 0.25.normalized, 0.5.normalized)       // màu HSL
val c: Color = Color.hsla(15.degrees, 0.25.normalized, 0.5.normalized, 0.5.normalized) // màu HSLA 

// Đổi màu/trộn màu bằng cú pháp toán tử:
val c: Color = someColor spin       10.degrees     // đổi màu
val c: Color = someColor lighten    0.1.normalized // đổi độ sáng
val c: Color = someColor darken     0.1.normalized // đổi độ sáng
val c: Color = someColor saturate   0.1.normalized // đổi độ bão hòa
val c: Color = someColor desaturate 0.1.normalized // đổi độ bão hòa
val c: Color = someColor fadeIn     0.1.normalized // đổi độ mờ đục
val c: Color = someColor fadeOut    0.1.normalized // đổi độ mờ đục

// Đổi màu/trộn màu bằng cú pháp gọi phương thức:
val c: Color = someColor.spin(10.degrees)
val c: Color = someColor.lighten(0.1.normalized)
// v.v...
```

### Đường vẽ

```scala
// Tạo đường vẽ từ danh sách các PathElement:
val i: Image = OpenPath(List(
  MoveTo(Vec(0, 0).toPoint),
  LineTo(Vec(10, 10).toPoint)
))

// Tạo đường vẽ từ dãy PathElement khác:
val i: Image = OpenPath(
  (0 until 360 by 30) map { i =>
    LineTo(Vec.polar(i.degrees, 100).toPoint)
  }
)

// Kiểu phần tử element:
val e1: PathElement = MoveTo(toVec.toPoint)                        // không nét
val e2: PathElement = LineTo(toVec.toPoint)                        // nét thẳng
val e3: PathElement = BezierCurveTo(cp1Vec.toPoint, cp2Vec.toPoint, toVec.toPoint) // nét cong

// LƯU Ý: Nếu phần tử đầu không phải là MoveTo,
//        thì sẽ được quy đổi thành MoveTo
```

### Angles and Vecs

```scala
val a: Angle = 30.degrees                // góc tính bằng độ
val a: Angle = 1.5.radians               // góc tính bằng radian
val a: Angle = math.Pi.radians           // π radian
val a: Angle = 1.turns                   // góc tính bằng vòng hoàn chỉnh

val v: Vec = Vec.zero                    // vectơ không  (0,0)
val v: Vec = Vec.unitX                   // vectơ đơn vị phương x (1,0)
val v: Vec = Vec.unitY                   // vectơ đơn vị phương y (0,1)

val v: Vec = Vec(3, 4)                   // vectơ từ các tọa độ Đề-các
val v: Vec = Vec.polar(30.degrees, 5)    // vectơ từ các tọa độ cực
val v: Vec = Vec(2, 1) * 10              // nhân chiều dài
val v: Vec = Vec(20, 10) / 10            // chia chiều dài
val v: Vec = Vec(2, 1) + Vec(1, 3)       // cộng vectơ
val v: Vec = Vec(5, 5) - Vec(2, 1)       // trừ vectơ
val v: Vec = Vec(5, 5) rotate 45.degrees // quay ngược chiều kim đồng hồ

val x: Double = Vec(3, 4).x              // tọa độ x
val y: Double = Vec(3, 4).y              // tọa độ y
val a: Angle  = Vec(3, 4).angle          // ngược chiều kim đồng hồ từ (1, 0)
val l: Double = Vec(3, 4).length         // chiều dài
```
