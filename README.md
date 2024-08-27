# Thiết kế mô đun xử lý tín hiệu từ dàn cảm biến quang trở và led chiếu sáng

Kinh nghiệm của bản thân mình, là để xử lý 1 vấn đề lớn chúng ta nên đi từ trên xuống dưới, chia nhỏ các vấn đề và xử lý từng vấn đề nhỏ đó. Đối với robot cũng vậy. Mỗi con robot đều có một mô đun xử lý trung tâm, tính toán và điều khiển toàn bộ hệ thống của robot. Dàn cảm biến quang trở và led chiếu sáng trong robot cũng là 1 phần nhỏ trong cả con robot, phần nhỏ này có thể đưa trực tiếp vào mô đun xử lý trung tâm để xử lý trực tiếp.

### Nhưng mình không làm vậy!

Nếu mô đun xử lý trung tâm của các bạn đủ mạnh và đủ ngoại vi, đảm bảo xử lý được tất cả các tác vụ mượt mà thì ok, đưa trực tiếp để xử lý cũng được. Nhưng nếu mô đun xử lý trung tâm của các bạn không đủ mạnh, việc đưa các tín hiệu analog từ dàn cảm biến quang trở vào để nó xử lý đồng thời với các tác vụ điều khiển robot khác là không nên. Bởi tỉ lệ lỗi, treo là khá lớn.

### Mình làm thế này!

Mình sẽ thiết kế riêng một mô đun chuyên dụng chỉ để xử lý tín hiệu từ dàn cảm biến quang trở này. Mình gọi mô đun này là "ADC module". Tuy là có tốn kém thêm 1 chút nhưng hiệu quả đem lại là hoàn toàn xứng đáng!

Đầu vào của mô đun này là tín hiệu analog dạng điện áp từ các cảm biến quang trở gửi về, thông qua ngoại vi ADC của vi điều khiển biến đổi Analog to Digital (tương tự sang số) và sử dụng 1 vài thuật toán so sánh ngưỡng, để cho ra tín hiệu đầu ra là các tín hiệu digital 0 hoặc 1. Ví dụ 0 khi quang trở ở nền sân, 1 khi quang trở ở "line".

Các tín hiệu 0 hoặc 1 này được đưa đến mô đun xử lý trung tâm của robot để robot điều khiển bám "line". Việc làm như vậy sẽ giảm tải rất nhiều cho mô đun xử lý trung tâm, bởi khi này mô đun xử lý trung tâm chỉ cần đọc các chân IO đưa về là 0 hoặc 1.

Ví von ví dụ này như bạn có tiền, bạn thuê người giúp việc giúp bạn dọn dẹp nhà cửa, nấu ăn cho gia đình bạn để bạn có thời gian tập trung đi làm các công việc khác quan trọng hơn trong cuộc sống của bạn. Đến bữa cơm, bạn về nhà bạn chỉ cần ngồi mát ăn bát cơm, nhà cửa sạch sẽ, bạn được nghỉ ngơi thư giãn khiến đầu óc bạn được minh mẫn, xử lý các công việc khác 1 cách hiệu quả hơn. Nhưng bạn phải mất thêm tiền thuê người giúp việc :))).

## Sơ đồ nguyên lý, sơ đồ mạch in của mô đun xử lý tín hiệu (ADC Module):

Đối với mô đun này, ngoài việc xử lý tín hiệu đưa ra các chân IO với mức tín hiệu 0/1, mình có thiết kế thêm các chuẩn giao tiếp khác như UART, RS485, CAN để các bạn có thể truyền thông tin về giá trị của cảm biến quang trở, giá trị các chân IO,...v.v chỗ này có thể tùy biến thoải mái theo ý của các bạn.

Mình sẽ không đi quá sâu vào việc phân tích thiết kế mạch, các bạn có thể tìm hiểu trong source project mình share. Mọi thắc mắc có thể liên hệ mình qua gmail.

<div align="center">
    <img src="Image/main_sch.PNG" alt="main_sch.PNG">
</div>

<div align="center">
    <p>Sơ đồ nguyên lý tổng quát của ADC Module</p>
</div>

<div align="center">
    <img src="Image/3dtop.PNG" alt="3dtop.PNG">
</div>

<div align="center">
    <p>ADC Module mặt trên</p>
</div>

<div align="center">
    <img src="Image/3dbottom.PNG" alt="3dbottom.PNG">
</div>

<div align="center">
    <p>ADC Module mặt dưới</p>
</div>
