# Thiết kế mô đun xử lý tín hiệu từ dàn cảm biến quang trở và led chiếu sáng

Nếu bạn chưa xem bài viết [Thiết kế dàn cảm biến quang trở và led chiếu sáng](https://github.com/Peter8686/Robot_8PhotoresistorandLedModule.git) thì mời bạn xem lại để hiểu được phần này.

Trước khi vào vấn đề chính, đăng vài tấm ảnh cho uy tín :D

<div align="center">
    <img src="Image/aquan2019.jpg" alt="aquan2019.jpg">
</div>

<div align="center">
    <p>Á quân Robocon MTA 2019 ^^</p>
</div>

<div align="center">
    <img src="Image/rb2021mta.jpg" alt="rb2021mta.jpg">
</div>

<div align="center">
    <p>Nhà vô địch Robocon MTA 2021 ^^</p>
</div>

Kinh nghiệm của bản thân mình, là để xử lý 1 vấn đề lớn chúng ta nên đi từ trên xuống dưới, chia nhỏ các vấn đề và xử lý từng vấn đề nhỏ đó. Đối với robot cũng vậy. Mỗi con robot đều có một mô đun xử lý trung tâm, tính toán và điều khiển toàn bộ hệ thống của robot. Dàn cảm biến quang trở và led chiếu sáng trong robot cũng là 1 phần nhỏ trong cả con robot, phần nhỏ này có thể đưa trực tiếp vào mô đun xử lý trung tâm để xử lý trực tiếp.

### Nhưng mình không làm vậy!

Nếu mô đun xử lý trung tâm của các bạn đủ mạnh và đủ ngoại vi, đảm bảo xử lý được tất cả các tác vụ mượt mà thì ok, đưa trực tiếp để xử lý cũng được. Nhưng nếu mô đun xử lý trung tâm của các bạn không đủ mạnh, việc đưa các tín hiệu analog từ dàn cảm biến quang trở vào để nó xử lý đồng thời với các tác vụ điều khiển robot khác là không nên. Bởi tỉ lệ lỗi, treo là khá lớn.

### Mình làm thế này!

Mình sẽ thiết kế riêng một mô đun chuyên dụng chỉ để xử lý tín hiệu từ dàn cảm biến quang trở này. Mình gọi mô đun này là "ADC module". Tuy là có tốn kém thêm 1 chút nhưng hiệu quả đem lại là hoàn toàn xứng đáng!

Đầu vào của mô đun này là tín hiệu analog dạng điện áp từ các cảm biến quang trở gửi về, thông qua ngoại vi ADC của vi điều khiển biến đổi Analog to Digital (tương tự sang số) và sử dụng 1 vài thuật toán so sánh ngưỡng, để cho ra tín hiệu đầu ra là các tín hiệu digital 0 hoặc 1. Ví dụ 0 khi quang trở ở nền sân, 1 khi quang trở ở "line".

Các tín hiệu 0 hoặc 1 này được đưa đến mô đun xử lý trung tâm của robot để robot điều khiển bám "line". Việc làm như vậy sẽ giảm tải rất nhiều cho mô đun xử lý trung tâm, bởi khi này mô đun xử lý trung tâm chỉ cần đọc các chân IO đưa về là 0 hoặc 1.

Ví von ví dụ này như bạn có tiền, bạn thuê người giúp việc giúp bạn dọn dẹp nhà cửa, nấu ăn cho gia đình bạn để bạn có thời gian tập trung đi làm các công việc khác quan trọng hơn trong cuộc sống của bạn. Đến bữa cơm, bạn về nhà bạn chỉ cần ngồi mát ăn bát cơm, nhà cửa sạch sẽ, bạn được nghỉ ngơi thư giãn khiến đầu óc bạn được minh mẫn, xử lý các công việc khác 1 cách hiệu quả hơn. Nhưng bạn phải mất thêm tiền thuê người giúp việc :))).

## Sơ đồ nguyên lý, sơ đồ mạch in của mô đun xử lý tín hiệu (ADC Module)

Đối với mô đun này, ngoài việc xử lý tín hiệu đưa ra các chân IO với mức tín hiệu 0/1, mình có thiết kế thêm các chuẩn giao tiếp khác như UART, RS485, CAN để các bạn có thể truyền thông tin về giá trị của cảm biến quang trở, giá trị các chân IO,...v.v chỗ này có thể tùy biến thoải mái theo ý của các bạn.

Mình sẽ không đi quá sâu vào việc phân tích thiết kế mạch, các bạn có thể tìm hiểu trong source project mình share. Mọi thắc mắc có thể liên hệ mình qua gmail của mình ở cuối bài viết.

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

Mạch in mình thiết kế là 4 lớp, các bạn nên chọn đơn vị gia công chất lượng chút. Mình gia công ở Trung Quốc ở đơn vị [Jlcpcb.com](jlcpcb.com). Các bạn cần có thẻ Visa để thanh toán và đặt hàng.

<div align="center">
    <img src="Image/pcb_thucte.jpg" alt="pcbthucte">
</div>

<div align="center">
    <p>Mạch in thực tế, 4 lớp</p>
</div>

<div align="center">
    <img src="Image/pcbcolk.jpg" alt="pcbcolk">
</div>

<div align="center">
    <p>Mạch ADC Module hoàn chỉnh</p>
</div>

## Lập trình cho mô đun xử lý tín hiệu (ADC Module)

Có thời gian mình sẽ giải thích chi tiết hơn về lập trình cho vi xử lý thế nào. Hiện tại mình sẽ chỉ cung cấp source code và giải thích qua.

Chương trình của mô đun xử lý tín hiệu sẽ thực hiện lấy giá trị Analog của các mắt cảm biến quang trở khi đặt ở đường "line" và lưu vào 1 mảng (gọi là A). Lấy giá trị analog của các mắt cảm biến quang trở khi đặt ở nền sân và lưu vào 1 mảng (gọi là B). Sau đó tiến hành tính toán ngưỡng so sánh bằng cách lấy trung bình (hoặc chia theo 1 tỉ lệ nào đó nếu các bạn cảm thấy phù hợp hơn mình đã để biến k trong source code để các bạn có thể thay đổi) mảng A và mảng B làm giá trị tham chiếu để so sánh, phân biệt màu nền với màu của "line".

Mình đã viết cả thư viện lọc Kalman nhưng chưa có thời gian để đưa vào. Các bạn hiểu về code thì có thể tự đưa vào, tự chỉnh sửa dựa trên source code của mình. Nhưng mình thấy chưa cần đưa bộ lọc Kalman vào mạch đã chạy ổn định rồi ;)

Ngoài ra phần cứng mình có thiết kế khá nhiều chuẩn giao tiếp để cho các bạn có thể tùy biến, truyền dữ liệu cảm biến lên mô đun xử lý trung tâm của các bạn như UART, RS485, CAN hay trực tiếp từ các chân IO. 

Phần này tạm thời thế đã, mình sẽ update thêm nếu có gì mới ở đây.

Mời các bạn xem tiếp phần [Hướng dẫn sử dụng mô đun xử lý tín hiệu ADC Module](https://github.com/Peter8686/Robot_UserManualADCModule)

#### Mọi thắc mắc xin liên hệ qua địa chỉ email của tôi: thaohv1639x@gmail.com 
## Thanks for watching!
