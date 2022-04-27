## Cài đặt chương trình cửa sổ lệnh (Terminal) và trình biên tập file chữ (Text Editor)

Trong mục này, chúng tôi gợi ý cách thiết lập cho những bạn mới lập trình, và mô tả cách thiết lập Scala Sáng tạo với cửa sổ lệnh và một trình biên tập file chữ.
Ta cần cài đặt:

- JVM (máy ảo Java);
- Git;
- một trình biên tập chữ, và
- một dự án mẫu cho Scala Sáng tạo.


### OS X

Mở cửa sổ lệnh. (Kích chuột vào biểu tượng kính lúp ở góc trên bên phải thanh công cụ. Gõ vào chữ "terminal".)

Cài đặt Java. 
Gõ vào cửa sổ lệnh dòng chữ sau

```bash
java
```

Nếu chương trình chạy được thì máy bạn đã cài Java rồi. 
Còn nếu không thì nó sẽ nhắc bạn cài đặt Java.

Hãy cài đặt homebrew.
Copy và paste dòng sau vào cửa sổ lệnh

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Hãy cài đặt `git` bằng homebrew.
Tại cửa sổ lệnh, gõ vào

```bash
brew install git
```

Bây giờ thì cài đặt trình biên tập Atom.
Một lần nữa, gõ vào cửa sổ lệnh

```bash
brew install Caskroom/cask/atom
```

Cài đặt trợ giúp Scala trong Atom như sau: Settings > Install > language-scala

Bây giờ ta sẽ dùng Git để làm cho dự án SBT hoạt động với Scala sáng tạo (Creative Scala).
Hãy gõ vào

```bash
git clone https://github.com/underscoreio/creative-scala-template.git
```

<div class="callout callout-info">

#### Chia sẻ kết quả học tập của bạn {-}

Có một cách thiết lập khác như sau: ban đầu "nhân bản" (fork) dự án mẫu Creative Scala, rồi "sao chép" (clone) về máy tính của bạn.
Đây là cách thiết lập cần làm nếu bạn muốn chia sẻ kết quả học tập của mình với người khác; chẳng hạn bạn đang học Scala Sáng tạo với thầy giáo trực tuyến hoặc chỉ đơn thuần là bạn thấy (chính đáng thôi) tự hào về thành quả của mình.

Theo cách thiết lập này, ban đầu bạn *fork* mẫu Creative Scala.
Sau đó là sao chép bản fork mà *bạn* vừa mới tạo.
Cách này sẽ được mô tả kĩ hơn ở mục GitHub bên dưới.
</div>


Bây giờ hãy chuyển tới thư mục mà ta mới lập rồi chạy SBT.

```bash
cd creative-scala-template
./sbt.sh
```

SBT sẽ khởi động.
Bên trong SBT, hãy gõ `console`.
Sau cùng, gõ vào

```scala
Example.image.draw()
```

và một hình ảnh ba vòng tròn sẽ xuất hiện!

Nếu bạn tới đây rồi, điều đó có nghĩa bạn đã cài đặt thành công tất cả phần mềm bạn cần để học tập toàn bộ khoá học Scala Sáng tạo.

Bước sau cùng là khởi động Atom rồi dùng nó để mở `Example.scala`, mà bạn có thể thấy ở `src/main/scala`.


### Windows

Tải về và cài đặt Java.
Tìm chữ "JDK" (Java development kit).
Đường link sẽ đưa bạn tới website của Oracle.
Chấp nhận giấy phép của họ rồi tải về JDK.
Chạy bộ cài đặt mà bạn mới tải về.

Tải về và cài đặt Atom.
Hãy đến `https://atom.io/` và tải về Atom cho Windows.
Chạy bộ cài đặt mà bạn mới tải về.

Tải về và cài đặt Git.
Tới `https://git-scm.com/` và tải về Git cho Windows.
Chạy bộ cài đặt mà bạn mới tải về.
Đến cuối, chương trình sẽ cho bạn chọn có mở Git hay không. 
Hãy chấp nhận, và một cửa sổ sẽ mở ra với dòng lệnh. 
Gõ vào


```bash
git clone https://github.com/underscoreio/creative-scala-template.git
```

<div class="callout callout-info">
 
#### Chia sẻ thành quả của bạn {-}

Có một cách thiết lập khác như sau: ban đầu "nhân bản" (fork) dự án mẫu Creative Scala, rồi "sao chép" (clone) về máy tính của bạn.
Đây là cách thiết lập cần làm nếu bạn muốn chia sẻ kết quả học tập của mình với người khác; chẳng hạn bạn đang học Scala Sáng tạo với thầy giáo trực tuyến hoặc chỉ đơn thuần là bạn thấy (chính đáng thôi) tự hào về thành quả của mình.

Theo cách thiết lập này, ban đầu bạn *fork* mẫu Creative Scala.
Sau đó là sao chép bản fork mà *bạn* vừa mới tạo.
Cách này sẽ được mô tả kĩ hơn ở mục GitHub bên dưới.
</div>

Hãy mở một cửa sổ dòng lệnh thông thường. 
Kích chuột vào biểu tượng cửa sổ ở góc trái phía dưới màn hình. 
Trong hộp tìm kiếm, gõ vào "cmd" rồi chạy chương trình mà nó tìm được. 
Trong cửa sổ mới mở ra, bạn hãy gõ

```bash
cd creative-scala-template
```

Lệnh này sẽ chuyển tới thư mục chứa dự án mẫu Scala Sáng tạo mà ta mới tải về.
Hãy gõ vào 

```bash
sbt.bat
```

để khởi động SBT. 
Bên trong SBT, gõ vào `console`.
Sau cùng, gõ vào

```scala
Example.image.draw()
```

và một hình ảnh ba vòng tròn sẽ xuất hiện!

Nếu bạn tới đây rồi, điều đó có nghĩa bạn đã cài đặt thành công tất cả phần mềm bạn cần để học tập toàn bộ khoá học Scala Sáng tạo.

Bước sau cùng là khởi động Atom rồi dùng nó để mở `Example.scala`, mà bạn có thể thấy ở thư mục `src\main\scala`.


### Linux

Theo các hướng dẫn cho OS X, nhưng sử dụng trình quản lý gói (distributions package manager) trong máy bạn để cài đặt phần mềm thay vì dùng Homebrew.
