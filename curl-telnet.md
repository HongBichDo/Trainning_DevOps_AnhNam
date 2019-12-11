# curl 
## curl là gì?
- curl (client URLs) công cụ tranfer dữ liệu từ server đến đâu và từ đâu đến server
- hỗ trợ các giao thức: FPT, HTTP, HTTPS, SMTP, IMAP
- chạy bằng command
 Một trong những chức năng cơ bản nhất của curl là giúp người dùng tải xuống một trang web. Ngoài ra nó còn dùng để vận chuyển các tập tin, hình ảnh, dữ liệu. Đồng thời curl còn có thể kiểm tra cookies nào đã được tải trên URL.

## Cách sử dụng curl
### Kiểm tra version trên máy

```sh
curl --version
```

### Hiển thị nội dung trang web
Cách đơn giản nhất của `curl` là hiển thị nội dung của trang. Ví dụ xem nội dung trang google.com

```sh
curl http://google.com/
```

Nó sẽ kết xuất mã nguồn của trang chủ. Nếu không xác định protocol thì mặc định là HTTP. 

```sh
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="http://www.google.com/">here</A>.
</BODY></HTML>
```

Để xem thêm chi tiết về một yêu cầu (header được gửi và quá trình kết nối) flags `-v` là chế độ verbose 

```sh
curl -v http://google.com/
```

Thông tin chi tiết về một số giao thức, host hiển thị

```sh
*   Trying 2404:6800:4005:804::200e...
* TCP_NODELAY set
* Connected to google.com (2404:6800:4005:804::200e) port 80 (#0)
> GET / HTTP/1.1
> Host: google.com
> User-Agent: curl/7.55.1
> Accept: */*
>
< HTTP/1.1 301 Moved Permanently
< Location: http://www.google.com/
< Content-Type: text/html; charset=UTF-8
< Date: Thu, 05 Dec 2019 15:35:27 GMT
< Expires: Sat, 04 Jan 2020 15:35:27 GMT
< Cache-Control: public, max-age=2592000
< Server: gws
< Content-Length: 219
< X-XSS-Protection: 0
< X-Frame-Options: SAMEORIGIN
<
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="http://www.google.com/">here</A>.
</BODY></HTML>
* Connection #0 to host google.com left intact
```

### Tải file trên web

Để tải nội dung của trang web về client, thêm option -o

```sh
curl -o google.html http://google.com/
```

Câu lệnh trên sẽ tải nội dung trang http://google.com và lưu vào file google.html tại thư mục hiện tại.
Để tải tập tin trên internet về máy
```sh
curl -o ubuntu.iso http://releases.ubuntu.com/16.04.1/ubuntu-16.04.1-desktop-amd64.iso
```
Trong đó:
- `myfile.zip` để đổi tên file tải về.
- ``: đường dẫn
Hiển thị thông tin quá trình tải 
Để hiển thị tiến trình trong quá trình tải ra stdout, thêm option --progress

```sh
curl -o ubuntu.iso http://releases.ubuntu.com/16.04.1/ubuntu-16.04.1-desktop-amd64.iso --progress
```

### Request/Response HTTP
- Client tạo một request HTTP đến server chứ phương thức (POST, GET, HEAD), tiêu đề... Phương thức GET lấy tài nguyên từ server, POST để gửi dữ liệu đến server để xử lý mới một số dữ liệu.
- Server phản hồi chứa nội dung trang web client request chứa mã trạng thái, tiêu đề, nội dung.
- HTTP là giao thức TCP đảm bảo dữ liệu được truyền đi. HTTPS sử dụng giao thức SSL/TLS giúp bảo mật dữ liệu.
- Sử dụng tên miền ánh xạ đến địa chỉ IP qua giao thức `DNS`

### Đặt title cho yêu cầu HTTP

```sh
curl -H 'X-My-Custom-Header: 123' https://httpbin.org/get
```

Option `-H` để thay đổi tiêu đề theo yêu cầu HTTP. Dữ liệu được trả về với đúng tiêu đề vừa đặt.

```sh
{
  "args": {},
  "headers": {
    "Accept": "*/*",
    "Host": "httpbin.org",
    "User-Agent": "curl/7.55.1"
  },
  "origin": "117.0.135.15, 117.0.135.15",
  "url": "https://httpbin.org/get"
}
```
Trang web https://httpbin.org/get cho phép xem chi tiết các yêu cầu HTTP gửi tới nó.

### Thay đổi phương thức yêu cầu

Để thay đổi phương thức gửi yêu cầu (POST mà không có dữ liệu), option `x` 

```sh
curl -X POST https://httpbin.org/post
```

Phương thức `HEAD` khôngđược đặt với option này mà thay thế bằng tùy chọn `-I`

**Ví dụ**: Truy cập https://reqres.in/ để lấy API test.
Đường dẫn https://reqres.in/api/users?page=2 trả về đoạn JSON chứa các thông tin

```sh
{"page":2,"per_page":6,"total":12,"total_pages":2,"data":[{"id":7,"email":"michael.lawson@reqres.in","first_name":"Michael","last_name":"Lawson","avatar":"https://s3.amazonaws.com/uifaces/faces/twitter/follettkyle/128.jpg"}
```
Sử dụng `curl` kiểm tra API trên
```sh
curl https://reqres.in/api/users?page=2
```

Để thay đổi phương thức POST
```sh
curl -X POST https://reqres.in/api/users -d'{ "name": "morpheus","job": "leader"}'
```
Nhận thấy thông tin chuỗi JSON

### Sử dụng curl với user/pass
Proxy cho phép kết nối server thông qua máy chủ proxy mà không cần đến thông tin username/password
Cài đặt proxy
```sh
export http_proxy = http:
```

# Tìm hiểu về Telnet
## Telnet là gì?
Telnet (teletype network) cung cấp khả năng giao tiếp giữa các thiết bị trên internet.
Telnet cung cấp kết nối từ xa, đảm nhiệm việc gửi các lệnh/dữ liệu đến các kết nối mạng.

Khi telnet vào một máy khác bằng quyền admin thì có thể cấu hình như đang sử dụng  máy đó.

## Cú pháp

`telnet host port`

Ví dụ muốn telnet đến địa chỉ IP là `192.168.56.101` với port 23

`telnet 192.168.56.101 23`

Sau đó nhập password để sử dụng như máy tính của mình.

## Resource 
- https://www.cyberciti.biz/faq/linux-unix-curl-command-with-proxy-username-password-http-options/