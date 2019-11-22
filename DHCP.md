# DHCP là gì?
Các thiết bị khi muốn kết nối vào mạng đều cần 1 địa chỉ IP. Địa chỉ IP được cấp phát bởi máy chủ DHCP tích hợp trên router. 
Dynamic Host Configuration Protocol (DHCP) là giao thức cấp phát địa chỉ IP một cách tự động.
# Các thành phần của DHCP
- DHCP client: thiết bị có yêu cầu kết nối mạng
- DHCP server: máy chủ hoặc router chạy dịch vụ DHCP. Quản lý sự cấp phát địa chỉ IP động.
- IP address pool: dãy địa chỉ có sẵn cho client DHCP
- Subnet: mạng con

# Nguyên lí hoạt động của DHCP
DHCP làm việc theo mô hình client/server.
- Bước 1: client gửi gói tin DHCP discover yêu cầu lấy các thông tin IP, subnet mask,default gateway... Địa chỉ nguồn 0.0.0.0, địa chỉ broadcast 255.255.255.255. Gói tin DHCP discover gửi đi toàn mạng chứa một địa chỉ MAC và tên máy client.
- Bước 2: DHCP server reply bằng gòi tin DHCP offer chứa một địa chỉ IP kèm theo là địa chỉ MAC của clientđược cấp, subnet mask, địa chỉ IP của DHCP server  
- Bước 3: Máy client chọn lọc gói tin phù hợp và phản hồi bằng DHCP request chấp nhận 
- Bước 4: DHCP server chấp nhận request bằng DHCP Ack bao gồm thông tin IP, DNS server

# Các thuật ngữ trong DHCP
- DHCP Server: máy quản lý việc cấu hình và cấp phát địa chỉ IP cho Client
- DHCP Client: máy trạm nhận thông tin cấu hình IP từ DHCP Server
- Scope: phạm vi liên tiếp của các địa chỉ IP có thể cho một mạng.
- Exclusion Scope: là dải địa chỉ nằm trong Scope không được cấp phát động cho Clients.
- Reservation: Địa chỉ đặt trước dành riêng cho máy tính hoặc thiết bị chạy các dịch vụ (tùy chọn này thường được thiết lập để cấp phát địa chỉ cho các Server, Printer,…..)
- Scope Options: các thông số được cấu hình thêm khi cấp phát IP động cho Clients như DNS Server(006), Router(003)

# Cấu trúc gói tin DHCP

# Cấu hình dịch vụ DHCP
## Resource 
- https://itforvn.com/tu-hoc-mcsa-mcse-2016-lab-4-cau-hinh-dhcp-server-va-backup-restore.html/