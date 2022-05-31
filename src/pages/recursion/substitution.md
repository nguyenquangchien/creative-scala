## Suy luận về đệ quy

```scala mdoc:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
```

Bây giờ ta đã có nhiều kinh nghiệm dùng đệ quy cấu trúc trên các số nguyên.
Hãy cùng trở lại mô hình thay thế của ta và xem liệu nó có hoạt động được với công cụ đệ quy mới này không.

Hãy nhớ lại rằng luật thay thế phát biểu rằng ta có thể thay giá trị bằng biểu thức bất kì khi nào nhìn thấy giá trị.
Trong trường hợp lời gọi phương thức, ta có thể thay thế phần thân phương thức bằng cách đổi tên các tham số một cách thích hợp.

Ví dụ đầu tiên về đệ quy mà ta gặp là `boxes`, được viết như sau:

```scala mdoc:silent
val aBox = Image.square(20).fillColor(Color.royalBlue)

def boxes(count: Int): Image =
  count match {
    case 0 => Image.empty
    case n => aBox.beside(boxes(n-1))
  }
```

Hãy cùng thử dùng cách thay thế cho `boxes(3)` để xem ta nhận được gì.

Lần thay thế đầu tiên là

```scala mdoc:silent
boxes(3)
// Thay thế phần thân của `boxes`
3 match {
  case 0 => Image.empty
  case n => aBox.beside(boxes(n-1))
}
```

Nhờ việc biết cách ước lượng biểu thức `match` và một lần nữa dùng cách thay thế, ta có

```scala mdoc:silent
3 match {
  case 0 => Image.empty
  case n => aBox.beside(boxes(n-1))
}
// Thay thế vế phải biểu thức `case n`
aBox.beside(boxes(2))
```

Ta có thể lại thay thế với `boxes(2)` để có

```scala mdoc:silent
aBox.beside(boxes(2))
// Thay thế phần thân của boxes
aBox.beside {
  2 match {
    case 0 => Image.empty
    case n => aBox.beside(boxes(n-1))
  }
}
// Thay thế biểu thức vế phải của `case n`
aBox.beside {
  aBox.beside(boxes(1))
}
```

Lặp lại quá trình này thêm vài lần nữa, ta có

```scala mdoc:silent
aBox.beside {
  aBox.beside {
    1 match {
      case 0 => Image.empty
      case n => aBox.beside(boxes(n-1))
    }
  }
}
// Thay thế biểu thức vế phải của `case n`
aBox.beside {
  aBox.beside {
      aBox.beside(boxes(0))
  }
}
// Thay thế phần thân của boxes
aBox.beside {
  aBox.beside {
    aBox.beside {
      0 match {
        case 0 => Image.empty
        case n => aBox.beside(boxes(n-1))
      }
    }
  }
}
// Thay thế biểu thức vế phải của `case 0`
aBox.beside {
  aBox.beside {
    aBox.beside {
      Image.empty
    }
  }
}
```

Kết quả cuối cùng được rút gọn thành

```scala mdoc:silent
aBox.beside(aBox).beside(aBox).beside(Image.empty)
```

chính là điều ta mong đợi.
Do vậy, có thể nói rằng phép thay thế đã phát huy tác dụng để suy luận về đệ quy.
Thật tuyệt vời!
Tuy nhiên các phép thay thế khá phức tạp và khó theo dõi nếu không viết hẳn ra.


### Suy luận về đệ quy cấu trúc

Có một cách thực dụng hơn để suy luận vê đệ quy cấu trúc. Đệ quy cấu trúc đảm bảo rằng tổng thể đệ quy được đúng đắn nếu như ta làm đúng từng thành phần của nó. Có hai phần trong một đệ quy cấu trúc; trường hợp cơ sở và trường hợp đệ quy. Với trường hợp cơ sở, chỉ cần nhìn vào là biết đúng sai rồi. Trường hợp đệ quy thì có lời gọi đệ quy (phương thức tự gọi lại nó) nhưng *ta không phải xét tới điều này*. Ta có được luôn điều này nhờ đệ quy cấu trúc, bởi vậy nó sẽ đúng miễn là các phần khác đều đúng. Có thể đơn giản là coi rằng lời gọi đệ quy là đúng đắn và rồi kiểm tra để đảm bảo ta đang làm đúng với kết quả nhận được từ lời gọi nêu trên.

Hãy cùng áp dụng cách này để suy luận về `boxes`.

```scala mdoc:reset:invisible
import doodle.core._
import doodle.image._
import doodle.image.syntax._
import doodle.image.syntax.core._
import doodle.java2d._
val aBox = Image.square(20).fillColor(Color.royalBlue)
```
```scala mdoc:silent
def boxes(count: Int): Image =
  count match {
    case 0 => Image.empty
    case n => aBox.beside(boxes(n-1))
  }
```

Bằng cách điêu tra có thể nói rằng trường hợp cơ sở là đúng.
Khi nhìn vào trường hợp đệ quy ta *coi* rằng `boxes(n-1)` sẽ làm đúng.
Khi đó câu hỏi trở thành: liệu rằng điều ta làm là đúng với kết quả nhận được từ lời gọi đệ quy `boxes(n-1)`?
Câu trả lời là có: nếu đệ quy `boxes(n-1)` tạo nên `n-1` ô trên một hàng, thì việc gắn một ô lên phía trước chúng là điều đúng đắn.
Vì các trường hợp đơn lẻ đã đúng đắn nên toàn bộ công việc sẽ đảm bảo là đúng nhờ đệ quy cấu trúc.

Cách suy luận này thị gọin hơn nhiều là dùng thay thế *và cũng* đảm bảo hiệu nghiệm *nếu* ta dùng đệ quy cấu trúc.


### Bài tập {-}

Dưới đây là vài ví dụ khá ngốc nghếch về đệ quy cấu trúc.
Hãy phân tích xem liệu những phương thức này có hoạt động như chúng cam kết không, mà *không* chạy mã lệnh.

```scala mdoc:silent
// Cho trước một số tự nhiên, hãy trả lại chính số đó 
// Ví dụ:
//   identity(0) == 0
//   identity(3) == 3
def identity(n: Int): Int =
  n match {
    case 0 => 0
    case n => 1 + identity(n-1)
  }
```

<div class="solution">
Dĩ nhiên là có!
Trường hợp cơ bản là quá hiển nhiên.
Nhìn vào trường hợp đệ quy, ta coi rằng `identity(n-1)` trả lại chính identity, tức là nhận diện cho `n-1` (giá trị `n-1`).
Khi đó, nhận diện cho `n` sẽ bằng `1 + identity(n-1)`.
</div>

```scala mdoc:silent
// Cho trước một số tự nhiên, hãy nhân đôi số đó 
// Ví dụ:
//   double(0) == 0
//   double(3) == 6
def double(n: Int): Int =
  n match {
    case 0 => 0
    case n => 2 * double(n-1)
  }
```

<div class="solution">
Không!
Phương thức này sai ở hai chỗ.
Thứ nhất, vì ta tính nhân trong trường hợp đệ quy nên rốt cuộc ta sẽ phải nhân với trường hợp cơ sở bằng không, và do đó toàn bộ kết quả sẽ bằng không.

Ta có thể thử sửa chữa điều này bằng việc thêm trường hợp cơ sở bằng `1` (và có lẽ vẫn còn tự hỏi tại sao khung đệ quy cấu trúc vẫn không giúp gì ta được).

```scala mdoc:reset:silent
def double(n: Int): Int =
  n match {
    case 0 => 0
    case 1 => 1
    case n => 2 * double(n-1)
  }
```

Tuy nhiên, cách này vẫn chẳng cho ta kết quả đúng. Trong trường hợp đệ quy ta đang làm sai: đáng ra ta phải cộng chứ không phải là nhân.

Viết bằng biểu thức đại số:

```scala
2(n-1 + 1) == 2(n-1) + 2
```

Vậy nếu `double(n-1)` là `2(n-1)` thì ta sẽ phải *cộng* 2, chứ không phải nhân 2.
Phương thức đúng phải là

```scala mdoc:reset:silent
def double(n: Int): Int =
  n match {
    case 0 => 0
    case n => 2 + double(n-1)
  }
```
</div>
