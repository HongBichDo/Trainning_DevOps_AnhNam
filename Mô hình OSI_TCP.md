# Mô hình OSI
Mô hình OSI (Open Systems Interconnection Reference Model) dựa vào nguyên lý tầng cấp để kết nối truyền thông giữa các thiết bị và thiết kế giao thức mạng giữa chúng. Mỗi layer có một nhiệm vụ và chức năng cụ thể giúp tín hiệu được truyền đi nhanh chóng và bảo mật tuyệt đối.

![OSI](image/OSI.png)

## Các layer trong mô hình OSI
Mô hình OSI phân chia chức năng thành 7 layer, mỗi layer *chỉ sử dụng chức năng của tầng dưới nó* đồng thời chỉ cho phép tầng trên sử dụng các chức năng của mình.
1. Physical: chuyển đổi dữ liệu thành các tín hiệu cơ, điện, quang thành các tín hiệu nhị phân (0,1) để truyền trên đường truyền vật lý.
2. Data Link: định nghĩa các cách thức đóng gói dữ liệu cho các loại đường truyền. Tương tác với các giao thức của lớp trên, tầng DataLink sử dụng địa chỉ MAC (Mac address-Physical address) là địa chỉ đặc trưng. Thiết bị họat động là SWITCH.
3. Network: đường định tuyến, tìm đường đi tối ưu nhất cho các thực thể. Sử dụng địa chỉ IP (Logical address ). Thiết bị đặc trưng là ROUTER
4. Transport: quản lý thực hiện các tác vụ truyền dữ liệu từ source đến destination. Đảm bảo truyền dữ liệu tối ưu nhất.  
5. Session: thiết lập, duy trì, kết thúc phiên làm việc giữa hai hệ thống. Xác lập ánh xạ giữa các tên địa chỉ tạo ra sự giao tiếp giữa các máy tính khác nhau trên cơ sở các giao dịch truyền thông.
6. Presentaion: chuyển đổi các thông tin từ cú pháp người sử dụng sang cú pháp để truyền dữ liệu. Lớp này có khả năng nén dữ liệu truyền và mã hóa trước khi truyền để đảm bảo an toàn.
7. Application: cung cấp các phương tiện cho người dùng truy cập và sử dụng các dịch vụ của mô hình OSI. Các giao thức ở tầng này: HTTP, FPT, SMTP...

## Quy trình xử lý dữ liệu trong mô  hình OSI
Mô hình OSI làm việc hai chiều được sử dụng khi một máy tính nào đó nhận dữ liệu mà dữ liệu đó đi ngược trở lên từ lớp vật lý. 

![OSI_data](image/xu_ly_data.jpg)

### Phía máy gửi
**Các dữ liệu tại máy gửi được xử lý theo trình tự sau:**

- Người dùng đưa các thông tin cần truyền đi như hình ảnh, văn bản vào máy tính.
- Dữ liệu được chuyển xuống tầng Presentaion, dữ liệu được chuyển thành một dạng chung để mã hóa và nén dữ liệu.
- Tại tầng Session: bổ sung thông tin cho phiên giao dịch (gửi-nhận).
- Sau khi tầng Session thực hiện xong, dữ liệu được chuyển xuống tầng Transport. Tại tầng này, dữ liệu được cắt nhỏ thành các Segment cũng làm nhiệm cụ bổ sung thông tin về phương thức vận chuyển dữ liệu đảm bảo tính bảo mật và tin cậy khi truyền.
- Dữ liệu chuyển xuống tầng Network, các segment tiếp tục được chia nhỏ thành các gói Package khác nhau đồng thời bổ sung thông tin định tuyến đường đi cho gói tin.
- Dữ liệu được chuyển xuống tầng Data Link, mỗi Package được băm nhỏ thành nhiều Frame và bổ sung thêm các thông tin kiểm tra gói tin chứa dữ liệu để kiểm tra ở máy nhận.
- Cuối cùng, các frame này được chuyển xuống tầng Physical được chuyển thành một chuỗi các bit nhị phân (0,1) đưa lên các phương tiện truyền dẫn(dây cáp) để truyền đến máy nhận.

### Phía máy nhận
- Máy nhận kiểm tra quá trình đồng bộ và đưa chuỗi nhị phân vào vùng đệm. Thông báo cho tầng Data Link đã nhận dữ liệu.
- Data Link kiểm tra các lỗi trong Frame nhận được từ máy gửi (kiểm tra FCS có trong gói tin được gắn bên máy nhận). Sau đó kiểm tra địa chỉ MAC xem có trùng với địa chỉ máy nhận không. Nếu đúng thì gỡ bỏ Header của tầng Data Link rồi chuyển lên tầng Network.
- Tầng network kiểm tra địa chỉ trong gói tin có phải địa chỉ máy nhận không (địa chỉ IP). Đúng thì gỡ bỏ Header rồi chuyển đến tầng Transport.
- Tầng Transport hỗ trợ phục hồi lỗi và xử lý lỗi bằng cách gửi gói tin ACK,NAK. Sau khi phục hồi sửa lỗi, tầng này sắp xếp thứ tự phân đoạn và đưa dữ liệu đến tầng Session.
- Tầng Session đảm bảo dữ liệu trong gói tin nhận được toàn vẹn. Tiến hành gỡ bỏ Header của tầng này rồi gửi đến tầng Presentation.
- Tầng Presentation xử lý gói tin bằng cách chuyển đổi định dạng dữ liệu phù hợp. Sau đó gửi đến tầng Application.
- Tầng Application tiến hành xử lý và gỡ bỏ Header cuối cùng. Máy nhận nhận được dữ liệu của gói tin được truyền đi.

# Mô hình TCP/IP
TCP/ IP (Transmission Control Protocol/ Internet Protocol - Giao thức điều khiển truyền nhận/ Giao thức liên mạng), là một bộ giao thức trao đổi thông tin được sử dụng để truyền tải và kết nối các thiết bị trong mạng Internet.

Trong mô hình TCP/IP, `IP` có vai trò quan trọng cho phép máy tính gửi đi gói tin. `TCP` giúp kiểm tra các gói dữ liệu có lỗi hay không? Sau đó gửi yêu cầu truyền lại nếu có lỗi được tìm thấy.

## Các giao thức TCP/IP phổ biến

![TCP_IP](image/giaothuc_TCP.PNG)

- HTTP: sử dụng truyền dữ liệu không an toàn giữa client-server. Khi client gửi request đến server để xem website, máy chủ web nhận yêu cầu và gửi thông tin về cho client.
- HTTPS: sử dụng để truyền dữ liệu an toàn giữa client-server. Giao thức này được dùng để gửi dữ liệu một cách bảo mật như giao dịch thẻ tín dụng hoặc dữ liệu cá nhân.
- FTP: phương thức trao đổi file được sử dụng giữa hai hoặc nhiều máy tính thông qua Internet. các máy tính có thể gửi/nhận dữ liệu trực tiếp.

## Mô hình phân tầng trong TCP/IP
- Physical (còn được gọi là tầng liên kết dữ liệu)là tầng thấp nhất trong mô hình TCP/IP gồm các thiết bị giao tiếp mạng và chương trình cung cấp thông tin cần thiết để có thể hoạt động, truy nhập đường truyền qua các thiết bị.
- Network: xử lý quá trình truyền gói tin trên mạng. Bao gồm các giao thức:  IP (Internet Protocol), ICMP (Internet Control Message Protocol), IGMP (Internet Group Message Protocol).
- Transport: hoạt động qua hai giao thức chính là TCP (Transmisson Control Protocol) và UDP (User Datagram Protocol).
- Application: bao gồm các tiến trình và ứng dụng cung cấp người dùng truy cập mạng. Các dịch vụ cung cấp: telnet, FTP, WWW..

## Phương thức hoạt động
Khi truyền dữ liệu, quá trình tiến hành từ tầng trên xuống tầng dưới. Qua mỗi tầng dữ liệu được thêm vào Header (thông tin điều khiển). Khi nhận dữ liệu thì quá trình xảy ra ngược lại.
Trong các tầng khác nhau, dữ liệu mang các thuật ngữ khác nhau. Trong tầng Application là `stream`, Transport là `segment`, tầng Network là `IP Datagram`, tầng Data Link là `Frame`.

# So sánh mô hình OSI và TCP/IP

![TCP_IP](image/tcp-ip-osi.jpg)

| Tiêu chí | OSI | TCP/IP | 
|----------|-----|--------|
| Độ tin cậy | Thấp | Đáng tin cậy | 
| Bảo mật | Bảo mật cao | Nới lỏng các quy tắc | 
| Phương pháp tiếp cận | Chiều dọc | Chiều ngang | 
| Mô hình phân tầng | Các tầng hoạt động riêng biêt | kết hợp tầng session và presentation trong tầng application |
| Thiết kế mô hình | phát triển mô hình trước phát triển giao thức | các giao thức được thiết kế trước khi phát triển mô hình |
| Truyền thông | Hỗ trợ kết nối không dây và định tuyến | Chỉ hỗ trợ tryền thông không kết nối |
| Tính phụ thuộc | Độc lập | Mô hình phụ thuộc vào giao thức |   

## Resource
- https://medium.com/@totolinkvn/t%C3%ACm-hi%E1%BB%83u-c%C3%A1c-t%E1%BA%A7ng-li%C3%AAn-k%E1%BA%BFt-trong-m%C3%B4-h%C3%ACnh-osi-d8f498097e97
- https://vnpro.vn/tin-tuc/gioi-thieu-tong-quan-ve-bo-giao-thuc-tcpip-1103.html
- https://wiki.matbao.net/kb/tcp-ip-la-gi-uu-va-nhuoc-diem-cua-tcp-ip-so-voi-mo-hinh-osi/
- https://itforvn.com/bai-2-mo-hinh-osi-va-tcpip.html/