# ADC Module - Ứng dụng cảm biến quang trở trong dò đường cho Robot

## Intro

Đầu tiên, đây là 1 dự án miễn phí nhằm hỗ trợ các bạn học viên, sinh viên áp dụng công nghệ dò đường cho robot sử dụng cảm biến quang trở.

Công nghệ dò đường cho robot sử dụng các cảm biến quang trở hay hồng ngoại,...v.v đã có từ rất lâu. Tuy nhiên để có thể áp dụng một cách hiệu quả, lựa chọn được cảm biến có độ ổn định và chính xác cao thì đối với các bạn học viên, sinh viên có thể còn gặp nhiều khó khăn.

## Nguyên lý hoạt động của quang trở và ứng dụng trong dò đường robot

Quang trở là 1 cảm biến thay đổi giá trị điện trở theo cường độ ánh sáng chiếu vào nó. Cường độ ánh sáng càng mạnh thì điện trở của quang trở càng nhỏ và ngược lại.

Ánh sáng chiếu vào các màu sắc khác nhau sẽ bị hấp thụ 1 phần khác nhau, còn lại là chúng phản xạ trở lại dẫn đến cường độ ánh sáng phản xạ trở lại là khác nhau. Các robot dò đường thường có những đường "line" để đi theo. Và màu sắc của các đường "line" sẽ khác biệt với màu nền. Giả sử trong các sân chơi robot, màu "line" sẽ là màu trắng, màu nền sân là màu xanh lá. Nếu dùng 1 đèn led chiếu vào "line" và màu nền sân, để cảm biến quang trở gần đó thu lại ánh sáng phản xạ từ "line" và nền sân, ta sẽ thấy giá trị điện trở của quang trở sẽ có sự khác biệt, chính là bởi vì ánh sáng phản xạ của "line" và màu nền sân là khác nhau. Dựa vào nguyên lý như vậy, ta có thể áp dụng quang trở để phân biệt "line" và nền sân.

<div align="center">
    <img src="Image/FBline.png" alt="Schematic">
</div>

Mô tả thực tế

## Từ sự thay đổi về điện trở của quang trở, làm thế nào để vi điều khiển biết được?

Bằng cách mắc mạch theo kiểu cầu phân áp dưới đây, ta cấp cho cầu phân áp điện áp tham chiếu VREF, khi quang trở LDR9 có sự thay đổi về điện trở, điện áp rơi (ADCIN) trên quang trở cũng sẽ thay đổi theo. Đưa giá trị điện áp này vào ngoại vi ADC của vi điều khiển, chúng ta sẽ xác định được giá trị này.

<div align="center">
    <img src="Image/schematic_pcb.png" alt="Schematic_pcb" style="display: inline-block; margin-right: 10px;">
    <img src="Image/adc_conveter.png" alt="adcImage" style="display: inline-block;">
</div>

## Thiết kế phần cứng cho mô đun dò đường robot sử dụng quang trở

### Thiết kế dàn cảm biến quang trở và led chiếu sáng

Mỗi một cảm biến quang trở, mình sử dụng 2 đèn led để chiếu sáng. Mục đích là để tăng cường độ ánh sáng chiếu và ánh sáng phản xạ. Bởi nếu ánh sáng chiếu yếu, khi gặp các nguồn sáng mạnh hơn từ môi trường chiếu vào sẽ làm nhiễu cảm biến.

<div align="center">
    <img src="Image/8_led_schematic.png" alt="8ledSchematic">
</div>

<div align="center">
    <p>Sơ đồ nguyên lý dàn cảm biến quang trở và led chiếu sáng</p>
</div>

Led và quang trở được bố trí như ở dưới đây, chỉ lưu ý khoảng cách giữa 2 cặp led và quang trở ở giữa nên được thay đổi khi độ rộng đường line thay đổi. Ví dụ độ rộng đường line là 3cm thì 2 cặp led và quang trở ở giữa các bạn nên để khoảng cách khoảng 2.8cm, để 2 cặp led và quang trở này nằm ở giữa vạch khi robot chạy giữa line.

<div align="center">
    <img src="Image/8led_pcb.png" alt="8ledpcb">
</div>

### Thiết kế mô đun xử lý tín hiệu từ dàn cảm biến quang trở và led chiếu sáng

Kinh nghiệm của bản thân mình, là để xử lý 1 vấn đề lớn chúng ta nên đi từ trên xuống dưới, chia nhỏ các vấn đề và xử lý từng vấn đề nhỏ đó. Đối với robot cũng vậy. Mỗi con robot đều có một mô đun xử lý trung tâm, tính toán và điều khiển toàn bộ hệ thống của robot. Dàn cảm biến quang trở và led chiếu sáng trong robot cũng là 1 phần nhỏ trong cả con robot, phần nhỏ này có thể đưa trực tiếp vào mô đun xử lý trung tâm để xử lý trực tiếp.

#### Nhưng mình không làm vậy!

Nếu mô đun xử lý trung tâm của các bạn đủ mạnh và đủ ngoại vi, đảm bảo xử lý được tất cả các tác vụ mượt mà thì ok, đưa trực tiếp để xử lý cũng được. Nhưng nếu mô đun xử lý trung tâm của các bạn không đủ mạnh, việc đưa các tín hiệu analog từ dàn cảm biến quang trở vào để nó xử lý đồng thời với các tác vụ điều khiển robot khác là không nên. Bởi tỉ lệ lỗi, treo là khá lớn.

#### Mình làm thế này!

Mình sẽ thiết kế riêng một mô đun chuyên dụng chỉ để xử lý tín hiệu từ dàn cảm biến quang trở này. Mình gọi mô đun này là "ADC module". Tuy là có tốn kém thêm 1 chút nhưng hiệu quả đem lại là hoàn toàn xứng đáng!

Đầu vào của mô đun này là tín hiệu analog dạng điện áp từ các cảm biến quang trở gửi về, thông qua ngoại vi ADC của vi điều khiển biến đổi Analog to Digital (tương tự sang số) và sử dụng 1 vài thuật toán so sánh ngưỡng, để cho ra tín hiệu đầu ra là các tín hiệu digital 0 hoặc 1. Ví dụ 0 khi quang trở ở nền sân, 1 khi quang trở ở "line".

Các tín hiệu 0 hoặc 1 này được đưa đến mô đun xử lý trung tâm của robot để robot điều khiển bám "line". Việc làm như vậy sẽ giảm tải rất nhiều cho mô đun xử lý trung tâm, bởi khi này mô đun xử lý trung tâm chỉ cần đọc các chân IO đưa về là 0 hoặc 1.

Ví von ví dụ này như bạn có tiền, bạn thuê người giúp việc giúp bạn dọn dẹp nhà cửa, nấu ăn cho gia đình bạn để bạn có thời gian tập trung đi làm các công việc khác quan trọng hơn trong cuộc sống của bạn. Đến bữa cơm, bạn về nhà bạn chỉ cần ngồi mát ăn bát cơm, nhà cửa sạch sẽ, bạn được nghỉ ngơi thư giãn khiến đầu óc bạn được minh mẫn, xử lý các công việc khác 1 cách hiệu quả hơn. Nhưng bạn phải mất thêm tiền thuê người giúp việc :))).

### Sơ đồ nguyên lý, sơ đồ mạch in của mô đun xử lý tín hiệu (ADC Module):


