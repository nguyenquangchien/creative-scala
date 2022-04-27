# Mở đầu {-}

Creative Scala - cuốn sách này hướng đến các lập trình viên chưa có sẵn kinh nghiệm với ngôn ngữ Scala.
Sách được soạn để giúp bạn nhập môn lập trình hàm (functional programming) theo cách thú vị. 
Chúng tôi coi rằng bạn đã bước đầu làm quen với một ngôn ngữ lập trình khác nhưng rất ít hoặc chưa lập trình với Scala hoặc các ngôn ngữ lập trình hàm khác bao giờ.

Với cuốn sách này, chúng tôi vạch ra 3 mục tiêu sau:

1. Giới thiệu về lập trình hàm để bạn có thể tính toán và lập luận về các chương trình, và để đọc hiểu được những cuốn sách nhập môn khác về lập trình hàm.

2. Dạy bạn Scala đủ để bạn có thể khám phá sở thích riêng của mình và sử dụng Scala.

3. Trình bày nội dung theo cách nhẹ nhàng, hấp dẫn, vui nhộn, qua phương tiện đồ họa 2 chiều trên máy tính.

Lý do thúc đẩy chúng tôi viết cuốn sách này là từ kinh nghiệm bản thân học lập trình, tập lập trình hàm, và giảng dạy Scala cho các lập trình viên trong môi trường thương mại.

Trước hết, chúng tôi tin rằng lập trình hàm là tương lai.
Vì đã coi như bạn ít kinh nghiệm về lập trình, nên chúng tôi sẽ không đi sâu vào chi tiết khác biệt giữa lập trình hàm và lập trình hướng đối tượng mà bạn có thể đã biết.
Nói ngắn gọn, hiện nay có nhiều cách nghĩ và viết chương trình, trong đó chúng tôi chọn cách tiếp cận lập trình hàm.

Lý do chọn lập trình hàm còn thú vị hơn.
Cách phổ biến để dạy lập trình hiện nay có thể được gọi là cách tiếp cận "kho cú pháp" ("bag of syntax").
Theo cách này, ngôn ngữ lập trình được giảng dạy như một tập hợp các đặc điểm cú pháp (biến, vòng lặp for, vòng lặp while, phương thức) và người học bị bỏ mặc để tự hình dung xem mình sẽ sử dụng từng đặc điểm như thế nào.
Chúng tôi đã thấy cách làm này thất bại cả khi chúng tôi còn là sinh viên học lập trình, lẫn cả khi đã tốt nghiệp đại học và đi giảng dạy; đơn giản là vì người học chẳng có một cách bài bản nào để bóc tách một vấn đề và biến nó thành mã lệnh được.
Kết quả là nhiều sinh viên đã bỏ ngang khóa học do chất lượng giảng dạy kém.
Còn những sinh viên tiếp tục theo học nhưng chúng tôi thì chẳng qua đã thạo lập trình từ trước.

Hãy thử nghĩ lại về môn toán hồi tiểu học, cụ thể là phép cộng theo hàng xem. 
Đây là cách cơ bản mà chúng ta đã được dạy để cộng các số lớn mà không thể tính nhẩm được. 
Do vậy, chẳng hạn khi cộng 266 với 385, ta sẽ đặt phép tính thẳng hàng, và tính cộng có nhớ. 
Giờ thì có thể toán không còn là môn học bạn thích nữa, song vẫn còn đây bài học quan trọng. 
Thứ nhất, chúng ta đã được dạy một cách bài bản để thu được đáp số. 
Ta có thể *tính* ra kết quả một khi ta nhận thấy đây là bài toán đặt phép cộng. 
Thứ hai, chúng ta thậm chí chẳng cần hiểu cơ chế hoạt động của cách đặt phép tính này mới tính toán được (dù rằng hiểu bản chất sẽ giúp ích cho thao tác tính toán). 
Miễn là cứ theo quy trình, ta sẽ thu được đáp số đúng.

Điều đáng lưu ý về lập trình hàm là nó hoạt động như phép đặt tính cộng vậy.
Chúng ta có các phương pháp để đảm bảo ta thu được kết quả đúng nếu làm đúng theo phương pháp.
Ta sẽ gọi đó là việc *tính toán* một chương trình.
Đây không phải để nói lập trình chẳng có sáng tạo gì, mà là thách thức lớn nằm ở việc hiểu được cấu trúc của vấn đề và một khi hiểu xong thì phương pháp mà ta cần sử dụng tự nhiên sẽ đến.
Còn mã lệnh bản thân nó không phải là tâm điểm.

Chúng tôi dạy lập trình hàm bằng Scala, nhưng không phải dạy Scala.
Ngôn ngữ này hiện nay đang có nhu cầu lớn.
Các lập trình viên Scala có thể dễ dàng tìm việc ở nhiều lĩnh vực công nghiệp, và đây là một lý do quan trọng thúc đẩy việc học Scala.
Một trong những nguyên nhân giải thích sự phổ biến của Scala là ở chỗ ngôn ngữ này bao phủ cả lập trình hướng đối tượng - cách lập trình cũ - và lập trình hàm.
Có rất nhiều mã lệnh lập trình theo lối hướng đối tượng, và nhiều lập trình viên đã quen với lối đó.
Scala cho ta một cách thuận lợi để đi từ lập trình hướng đối tượng sang lập trình hàm.
Tuy nhiên, điều này đồng nghĩa với Scala là một ngôn ngữ lớn, và sự tương tác giữa các phần hướng đối tượng và phần hàm có thể dễ gây nhầm lẫn.
Chúng tôi tin rằng lập trình hàm hiệu quả hơn nhiều so với lập trình hướng đối tượng; và các lập trình viên mới không cần phải làm tăng sự nhầm lẫn qua việc đồng thời học cả lập trình hướng đối tượng nữa.
Học lập trình hướng đối tượng có thể để sau.
Do vậy, cuốn sách này chỉ duy nhất dùng lối lập trình hàm trong Scala.

Sau cùng, chúng tôi chọn cái mà chúng tôi hi vọng là phương pháp vui nhộn để khám phá lập trình hàm và Scala: đó là đồ họa vi tính.
Có rất nhiều tài liệu nhập môn Scala, nhưng đa phần đều lấy các ví dụ liên quan đến kinh doanh hay toán học.
Chẳng hạn, một trong những bài tập đầu tiên trong khóa học phổ biến trên Coursera đã lập trình tập hợp qua các hàm chỉ thị.
Chúng tôi cảm thấy nếu bạn là típ người thích trực tiếp làm việc với những loại khái niệm như vậy thì bạn đã biết nhiều về lập trình quá rồi.
Chúng tôi muốn hướng đến nhóm độc giả khác: những người có lẽ nghĩ rằng toán không phải dành cho họ mà họ quan tâm và trân trọng mỹ thuật.
Chúng tôi không hề nói dối: trong quyển này có toán, nhưng chung tôi hi vọng là có thể khơi dậy và thực sự làm hiện hữu những khái niệm sao cho chúng bớt phần gây nản chí.

Dù rằng cuốn sách này sẽ xây dựng cho bạn một mô hình nhận thức cơ bản cần để bạn sử dụng thành thạo Scala,
song bạn sẽ không thể kết thúc mà biết *mọi thứ* để tự lực cánh sinh được.
Muốn tiến xa hơn, chúng tôi gợi ý bạn đọc thêm một số sách dạy Scala hay nữa đã xuất bản,
trong đó có quyển [Essential Scala][essential-scala] do chúng tôi viết.

Nếu bạn tự mình làm các bài tập trong cuốn này, chúng tôi khuyến khích bạn tham gia nhóm [Gitter chat room][underscore-gitter]
chỗ chúng tôi để nhận giúp đỡ về các bài tập cũng như cung cấp phản hồi về cuốn sách này.

Nội dung cuốn [Creative Scala][github-creative-scala] tồn tại dưới dạng nguồn mở,
cũng như mã nguồn thư viện đồ họa [Doodle][github-doodle]
được dùng trong các bài tập sau này. 
Bạn có thể lấy mã nguồn về từ [GitHub account][underscore-github] của chúng tôi.
Hãy liên lạc với chúng tôi qua Gitter hay qua email nếu bạn muốn đóng góp.

Cám ơn bạn đã sử dụng tài liệu này và chúc bạn lập trình một cách sáng tạo!

---Dave và Noel

## Lưu ý về phiên bản xem trước cuốn sách này {-}

<div class="callout callout-danger">
Đây là một bản phát hành *truy cập sớm* của sách Creative Scala. 
 Có thể có nhiều lỗi ty-pô và những lỗi khác trong sách và các bài ví dụ.

Nếu bạn phát hiện thấy lỗi hoặc muốn phản hồi lại, hãy cho chúng tôi biết qua nhóm [Gitter chat room][underscore-gitter]
hoặc qua email cho chúng tôi:

 - Dave Gurnell ([dave@underscore.io](mailto:dave@underscore.io))
 - Noel Welsh ([noel@underscore.io](mailto:noel@underscore.io))
</div>

## Lời cảm tạ {-}

Scala sáng tạo được viết bởi [Dave Gurnell][twitter-dave] và [Noel Welsh][twitter-noel]. Rất cám ơn [Richard Dallaway][twitter-richard], [Jonathan Ferguson][twitter-jono], và nhóm [Underscore][underscore] vì những đóng góp quý báu và đã đọc rà soát bản thảo kĩ lưỡng.

Chúng tôi cũng cám ơn nhiều người đã chỉ ra các lỗi sai và gợi ý để cải thiện cuốn sách: Neil Moore; Kelley Robinson, Julie Pitt, và những người tổ chức ScalaBridge - Matt Kohl; Alexa Kovachevich và những sinh viên khác đã luyện tập bằng cuốn Scala sáng tạo tại ScalaBridge hay những sự kiện khác, hoặc là tự học; cũng như nhiều thành viên tích cực khác của cộng đồng Scala những người đã trực tiếp bình luận và gợi ý về nội dung sách. Ngoài ra, chúng tôi ghi nhận sự giúp đỡ từ Bridgewater, và đặc biệt của Lauren Cipicchio, người có lẽ đã góp quỹ cho sự phát triển ban đầu của phiên bản thứ hai "Scala sáng tạo", và đã cung cấp cho một số loạt sinh viên ban đầu.

Sau cùng, "Scala sáng tạo" còn nợ rất nhiều giá trị trí tuệ từ sản phẩm của những nhà nghiên cứu trong lĩnh vực lý thuyết ngôn ngữ lập trình và giáo dục khoa học máy tính. Cụ thể, chúng tôi nhấn mạnh:

- sản phẩm của [nhóm nghiên cứu PLT](http://racket-lang.org/plt.html), và đặc biệt là cuốn sách ["How to Design Programs"](http://htdp.org/), viết bởi Matthew Flatt, Matthias Felleisen, Robert Bruce Findler, và Shriram Krishnamurthi; và
- phương pháp tiếp cận "viết mã lệnh sáng tạo" cho nhập môn lập trình do [Mark Guzdial](https://www.cc.gatech.edu/faculty/mark.guzdial/), [Dianna Xu](https://cs.brynmawr.edu/~dxu/), tiên phong cùng các cộng sự.
