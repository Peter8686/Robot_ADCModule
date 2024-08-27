# ADC Module - Ứng dụng cảm biến quang trở trong dò đường cho Robot

## Intro

Đầu tiên, đây là 1 dự án miễn phí nhằm hỗ trợ các bạn học viên, sinh viên áp dụng công nghệ dò đường cho robot sử dụng cảm biến quang trở.
Công nghệ dò đường cho robot sử dụng các cảm biến quang trở hay hồng ngoại,...v.v đã có từ rất lâu. Tuy nhiên để có thể áp dụng một cách hiệu quả, lựa chọn được cảm biến có độ ổn định và chính xác cao thì đối với các bạn học viên, sinh viên có thể còn gặp nhiều khó khăn.

## Nguyên lý hoạt động của quang trở và ứng dụng trong dò đường robot

Quang trở là 1 cảm biến thay đổi giá trị điện trở theo cường độ ánh sáng chiếu vào nó. Cường độ ánh sáng càng mạnh thì điện trở của quang trở càng nhỏ và ngược lại.
Ánh sáng chiếu vào các màu sắc khác nhau sẽ bị hấp thụ 1 phần khác nhau, còn lại là chúng phản xạ trở lại dẫn đến cường độ ánh sáng phản xạ trở lại là khác nhau. Các robot dò đường thường có những đường "line" để đi theo. Và màu sắc của các đường "line" sẽ khác biệt với màu nền. Giả sử trong các sân chơi robot, màu "line" sẽ là màu trắng, màu nền sân là màu xanh lá. Nếu dùng 1 đèn led chiếu vào "line" và màu nền sân, để cảm biến quang trở gần đó thu lại ánh sáng phản xạ từ "line" và nền sân, ta sẽ thấy giá trị điện trở của quang trở sẽ có sự khác biệt, chính là bởi vì ánh sáng phản xạ của "line" và màu nền sân là khác nhau. Dựa vào nguyên lý như vậy, ta có thể áp dụng quang trở để phân biệt "line" và nền sân.

![Schematic](Image/FBline.png)

Mô tả thực tế

## Từ sự thay đổi về điện trở của quang trở, làm thế nào để vi điều khiển biết được?

Bằng cách mắc mạch theo kiểu cầu phân áp dưới đây, ta cấp cho cầu phân áp điện áp tham chiếu VREF, khi quang trở LDR9 có sự thay đổi về điện trở, điện áp rơi (ADCIN) trên quang trở cũng sẽ thay đổi theo. Đưa giá trị điện áp này vào ngoại vi ADC của vi điều khiển, chúng ta sẽ xác định được giá trị này.

![Schematic_pcb](Image/schematic pcb.png)

## Thiết kế phần cứng cho mô đun dò đường robot sử dụng quang trở

