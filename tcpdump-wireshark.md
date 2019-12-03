Tìm hiểu lệnh tcpdump trên Linux

# tcpdump là gì?

- `tcpdump`: hỗ trợ phân tích các gói dữ liệu mạng theo dòng lệnh. Cho phép chặn và hiển thị các gói tin được truyền đi hoặc nhận trên một mạng máy tính.
- Có thể lưu ra file và đọc bằng Wireshark.

# Sử dụng tcpdump

- Cài đặt trên CentOS: 
`yum install tcpdump -y`
- Một số lệnh cơ bản
 - Các interface đang hoạt động
 `tcpdump -D`
 - Bắt gói tin trên interface
 `tcpdump -i <interface>`
Ví dụ: bắt gói tin trên card `enp0s3`
 **Các thông số**
 - Packet capture: số lượng gói tin bắt được và xử lý.
 - Packet received by filter: số lượng gói tin nhận được bởi bộ lọc
 - Packet dropped by kernel: số lượng packet đã bị dropped bởi cơ chế bắt gói tin của HĐH

**Định dạng chung một dòng giao thức tcpdump**
`time-stamp src > dst:  flags  data-seqno  ack  window urgent options`

 - time-stamp: thời gian gói tin được capture
 - src, dst: IP máy nhận và gửi
 - flags: 
  - S(SYN): sử dụng trong giao thức bắt tay 3 bước của giao thức TCP
  - ACK: thông báo bên nhận đã nhận được dữ liệu thành công
  - FIN: đóng kết nối TCP
  - PUSH: đánh dấu việc truyền dữ liệu
  - RST: thiết lập lại đường truyền
 - data-sqeno: số sequence number của gói dữ liệu hiện tại
 - ACK: mô tả số sequence number tiếp theo của gói tin do máy gửi truyền
 - window: vùng nhớ đệm có sẵn theo hướng khác trên kết nối này
 - urgent: dữ liệu khẩn cấp trong gói tin

- Bắt n gói tin với tùy chọn -c
`tcpdump -c n -i enp0s3`
- Lưu file .pcap(Wireshark)
 `tcpdump -i enp0s3 -w /opt/capture.pcap`
- bắt các gói tin TCP
`tcpdump -i enp0s3 tcp -c 5`
- Bắt gói tin theo port
`tcpdump -i enp0s3 port 22 -c 5 -n`
- Bắt gói tin theo địa chỉ nguồn và đích
 `tcpdump -i emp0s3 src 192.168.100.1`

## Resource 
- https://secure.vinahost.vn/ac/knowledgebase/248/TCPDUMP-va-cac-th-thut-s-dng.html