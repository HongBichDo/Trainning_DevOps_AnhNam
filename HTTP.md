
# HTTP - Hypertext-transfer-protocol
 
## HTTP là gì?
HTTP là giao thức truyền tải dữ liệu (văn bản, hình ảnh, âm thanh) giữa Web server và Web client và ngược lại dùng cho World Wide Web . HTTP sử dụng cổng 80. 

![HTTP](HTTP_client_server.PNG)


## Cách thức hoạt động của HTTP
HTTP nằm trong tầng Application Layer của mô hình OSI. Cơ chế chính của HTTP là Request-Response: Web client gửi Request đến Web server, Web server xử lý và trả về response cho client.

- Bước 1: HTTP client khởi tạo một request bằng cách thiết lập kết nối TCP đến cổng 80 trên server. Server chấp nhận kết nối, sau khoảng thời gian RTT (Round Trip Time) không có phản hồi từ server thì client gửi lại yêu cầu
- Bước 2: Client gửi yêu cầu lấy thông tin đường dẫn. Server lấy các đối tượng yêu cầu trả về cho Client
- Bước 3: Server đóng kết nối TCP khi chắc chắn client đã nhận được thông điệp
- Bước 4: Client nhận thông điệp chứa các tập tin HTML và hiển thị đối tượng


## HTTP methods
HTTP định nghĩa các phương thức để chỉ ra các hành động thực hiện.

### HTTP Request
Người dùng nhập địa chỉ URL xác nhận tìm kiếm tài nguyên, HTTP request bao gồm các thông tin sau: Request method, URL Request

- `GET`: lấy thông tin server sử dụng URL đã cung cấp chứa thông tin về trạng thái và nội dung yêu cầu.
- `HEAD`: tương tự `GET` nhưng không có nội dung thư, sử dụng lấy thông tin meta trong header mà không cần chuyển toàn bộ nội dung.
- `POST`: sử dụng khi upload hoặc submit web form, nhóm tin. Gửi dữ liệu lên máy chủ xử lý thông tin qua các biểu mẫu HTML
- `PUT`: thay tất cả tài nguyên đích hiện tại bằng nôi dung tải lên
- `DELETE`: Xóa tất cả các dữ liệu tài nguyên đích được chỉ ra trong URL
- `CONNECT`: Thiết lập một kết nối tới máy chủ được xác định bởi URL
- `OPTIONS`: Mô tả các thông tin tùy chọn cho tài nguyên đích
- `TRACE`: Thực hiện một vài lần kiểm tra để dẫn đến cùng một tài nguyên đích

- `URL Request`: Là một dạng tài nguyên định danh có thể là đường dẫn tuyệt đối hoặc tương đối.
URL được gửi qua Internet sử dụng bộ mã ASCII.

### HTTP Response
Sau khi nhận được và phân tích request từ client, server phản hồi lại HTTP Response là những mã trạng thái gồm 3 chữ số: xác định loại phản hồi

| Mã trạng thái | Mô tả | Giải thích | 
|----------|-----|--------|
| **1xx** | **Information** | **Yêu cầu đã được nhận và đang được tiếp tục xử lý** |
| **2xx | **Success** | **Hành động xử lý thành công** |
| 200 | OK | Yêu cầu hợp lệ |
| 202 | Accepted | Yêu cầu được chấp nhận để xử lý, nhưng quá trình xử lý không hoàn chỉnh. |
| 204 | No Content | Một mã trạng thái và một tiêu đề đưa ra trong phản hồi, nhưng không có thực thể nội dung trong phản hồi. |
| 205 | Reset Content | Trình duyệt nên xóa các biểu mẫu sử dụng cho giao dịch này để thêm dữ liệu vào. |
| 206 | Partial Content | Máy chủ đang trả về một phần dữ liệu với kích cỡ được yêu cầu. |
| **3xx | Redirection | Phải thực hiện thêm hành động để hoàn thành yêu cầu** |
| 301 | Moved Permanently | Trang được yêu cầu đã chuyển sang một đường dẫn mới. |
| 302 | Found | Trang được yêu cầu đã tạm thời di chuyển đến một đường dẫn mới. |
| 303 | See Other | Trang được yêu cầu có thể được tìm thấy dưới một đường dẫn khác. |
| **4xx |  Client Error | Yêu cầu có cú pháp không chính xác hoặc không đầy đủ** |
| 400 | Bad Request | Máy chủ không hiểu yêu cầu. |
| 401 | Unauthorized | Trang yêu cầu cần phải đăng nhập tài khoản và mật khẩu. |
| 403 | Forbidden | Trang yêu cầu hiện bị cấm truy cập. |
| 404 | Not Found | Máy chủ không thể tìm thấy trang được yêu cầu. |
| 405 | Method Not Allowed | Yêu cầu không được phép. |
| 408 | Request Timeout | Yêu cầu vượt quá thời gian được đưa ra bởi máy chủ để chờ xử lý. |
| **5xx | Server Error| Lỗi từ máy chủ khi không thể hoàn thành một yêu cầu hợp lệ** |
| 500 | Internal Server Error | Máy chủ ở trong tình trạng quá tải. |
| 501 | Not Implemented | Yêu cầu đã được nhận và đang được tiếp tục xử lýMáy chủ không hỗ trợ chức năng được yêu cầu. |
| 502 | Bad Gateway |  Máy chủ nhận được một phản hồi không hợp lệ. |
| 503 | Service Unavailable | Máy chủ đang tạm thời quá tải hoặc bảo dưỡng. |
| 504 | Gateway Timeout | Cổng đã hết thời gian. |
| 505 | HTTP Version Not Supported | Máy chủ không hỗ trợ phiên bản HTTP. |

## Thông điệp HTTP
Có 2 dạng thông điệp HTTP: HTTP Request và HTTP Response

### HTTP Request
```sh
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3
Accept-Encoding: gzip, deflate, br
Accept-Language: vi-VN,vi;q=0.9,fr-FR;q=0.8,fr;q=0.7,en-US;q=0.6,en;q=0.5
Cache-Control: max-age=0
Connection: keep-alive
Cookie: PHPSESSID=c59ddph147binrasa8l9pmqq2iqep5ut
Host: www.eclipse.org
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36

```
Trong đó:
- `Accept`: Thông báo choserver biết web-client có thể đọc dữ liệu nào
- `Accept-Encoding`: Web-client có thể đọcđược kiểu mã hóa nào
- `Accept-Language`: Ngôn ngữ của web-client, nếu không có ngôn ngữ đó trả về ngôn ngữ mặc định
- `Cache-Control`: 
- `User-Agent`: Thông báo cho web-client biết client sử dụng phiên bản trình duyệt nào. Dựa vào đó server gửi lại version phù hợp với trình duyệt trên di động.
- `Host`: địa chỉ host của server truy vấn
- `Accept`: 
- `Accept`: 
### HTTP Response

```sh
Cache-Control: no-cache, must-revalidate
Connection: keep-alive
Content-Encoding: gzip
Content-Length: 6353
Content-Type: text/html
Date: Sat, 30 Nov 2019 05:24:21 GMT
Expires: Sat, 30 Nov 2019 05:24:21 GMT
Last-Modified: Sat, 30 Nov 2019 05:24:21 GMT
Pragma: no-cache
Server: nginx
Strict-Transport-Security: max-age=15552000; includeSubDomains; preload
Vary: Accept-Encoding
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
X-Frame-Options: SAMEORIGIN
X-NodeID: www-vm2
X-Proxy-Cache: MISS
X-XSS-Protection: 1; mode=block
```
 
# HTTPS - Hypertext-transfer-protocol

## HTTPS là gì?
HTTPS (Hyper Text Transfer Protocol Secure) là phiên an toàn của HTTP có nghĩa là tất cả các giao tiếp giữa trình duyệt và trang web đều được mã hóa. HTTPS sử dụng port 443 đảm bảo các tính chất sau:
- Confidentiality: sử dụng phương thức encryption
- Integrity: sử dụng phương thức hashing đảm bảo tính toàn vẹn dữ liệu
- Authentication: sử dụng digital certificate đảm bảo server không phải giả mạo.

## Cách thức hoạt động của HTTPS

HTTPS sử dụng một trong hai giao thức bảo mật để mã hóa thông tin liên lạc - SSL (Secure Sockets Layer, tầng ổ bảo mật) hoặc TLS (Transport Layer Security, bảo mật tầng truyền tải).
Sử dụng hệ thống PKI (Public Key Infrastructure, hạ tầng khóa công khai) không đối xứng. 
Public key để mã hóa và chỉ được giải mã bằng private key. 
Private key được bảo mật tại web server, Public key được công khai cho tất cả mọi người.
- Bước 1: CLient gửi request cho một trang bảo mật (URL bắt đầu https://)
- Bước 2: Server gửi lại cho client certificate của nó
- Bước 3: CLient xác thực bằng cách kiểm tra tính hợp lệ của chữ ký số kèm theo
- Bước 4: Khi certificate đã xác thực và còn hạn sử dụng hoặc client cố tình truy cập khi đã được cảnh báo không tin cậy thì: client tự tạo ngẫu nhiên một session key rồi sử dụng public key để mã hóa session key này gửi cho server.
- Bước 5: Server sử dụng private key giải mã session key.
- Bước 6: Server và client sử dụng session key mã hóa/giải mã các thông điệp trong suốt phiên trao đổi.

## Chứng chỉ HTTPS
Khi yêu cầu kết nối HTTPS với trang web:
- Trang web gửi chứng chỉ SSL tới trình duyệt chứa Public key bắt đầu phiên bảo mật.
- Trình duyệt và trang web bắt đầu giao thức bắt tay SSL handshake thiết lập kết nối an toàn.

# So sánh HTTP và HTTPS

![HTTP](HTTP_HTTPS.PNG)

Sự khác biệt quan trọng giữa HTTP và HTTPS là chứng chỉ SSL.

| Đặc điểm | HTTP | HTTPS | 
|----------|-----|--------|
| Nguyên lý hoạt động | Mô hình client-server không bảo mật | Sử dụng các giao thức bảo mật SSL hoặc TSL |
| Port| 80| 443 |
| Hoạt động | Tầng ứng dụng | Tầng giao vận |


## Resource
- https://www.topwebviet.com/cach-thuc-giao-tiep-giua-trinh-duyet-web-voi-may-chu-web.html
- http://notes.viphat.work/tong-quan-ve-tcp-ip-va-http
- https://vnsys.wordpress.com/2016/12/16/http-la-gi-va-cach-no-lam-viec/
- https://vnsys.wordpress.com/2016/12/16/http-la-gi-va-cach-no-lam-viec/
- http://hatangmang.blogspot.com/2014/06/giao-thuc-http.html