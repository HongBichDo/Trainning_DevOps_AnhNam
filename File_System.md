Trên linux tất cả mọi thứ đều là file, Linux có rất nhiều file Để quản lí và tổ chức file hiệu quả linux đưa ra khái niệm file system. Các file có dạng hình cây có gốc, cành và lá.
Hai dạng file chính là file và thư mục – file chứa các thông tin của các file khác.
```sh
/root
/bin
/boot
/etc
/dev
/home
/lib
/proc
/usr
/var
```
 ## /Root 
 Là thư mục gốc của Root user. Chỉ có Root Users mới có quyền write đối với thư mục này.
 ##  User Binaries 
- Chứa nhiều ứng dụng khác nhau dùng cho cả việc bảo trì hệ thống root cũng như các lệnh thông thường. 
- Lệnh Linux phổ biến sử dụng ở chế độ Singer-user mode nằm trong thư mục này.
- Tất cả user trên hệ thống nằm tại thư mục này đều có thể sử dụng lệnh (`ps`, `ls`, `grep`)
- 
## Boot Loader Files
- Chứa các tập tin cấu hình cho quá trình khởi động hệ thống.
- Các file Kernel initrd, vmlinux, grub nằm trong /boot.
## Configuration Files
- Chứa cấu hình các tập tin cấu hình của hệ thống, các tập tin lệnh để khởi động các dịch vụ của hệ thống. Thường là các file txt có chức năng tương tự với **Control Pannel** trong Windows
- Ngoài ra /etc còn chứa shell scripts startup và shutdown, sử dụng để chạy/ngừng các chương trình cá nhân.
```sh
/etc/resolv.conf (cấu hình dns-server )
/etc/network dùng để quản lý dịch vụ network
```
- Thư mục `/etc/rc.d` chứa các scripts dùng để start, stop, kiểm tra status cho các chương trình.
## Files device
- Chứa các tập tin để nhận biết cho các thiết bị của hệ thống (device files).
- Bao gồm thiết bị đầu cuối, USB hoặc các thiết bị được gắn trên hệ thống.
```sh
ls /dev/
/dev/sda : đây là ổ đĩa SATA thứ nhất
/dev/cdrom : ổ CD
/dev/ttyS0 : cổng COM1
```
## Thư mục Home
- Thư mục chính lưu trữ các tập tin cá nhân của tất cả user.

- Ví dụ: /home/john, /home/nikita.
## System Libraries
- Chứa các file thư viện hỗ trợ các thư mục nằm dưới /bin và /sbin.
- Tên file thư viện có thể là ld* hoặc lib*.so.*.

- Ví dụ: ld-2.11.1.so, libncurses.so.5.7.
## Process Information
- Chứa đựng thông tin về quá trình xử lý của hệ thống
- Đây là một pseudo filesystem chứa đựng các thông tin về các process đang chạy
- Đây là một virtual filesystem chứa đựng các thông tin tài nguyên hệ thống.
**Kiểm tra thông tin CPU**
```sh
cat /proc/cpuinfo
```
## User Programs
- Chứa các ứng dụng, thư viện, tài liệu và mã nguồn các chương trình thứ cấp.
- `/usr/bin`: chứa các tập tin của các ứng dụng chính đã được cài đặt cho user. Nếu bạn không tìm thấy user binary tại thư mục /bin, bạn có thể tìm tại thư mục /usr/bin. Ví dụ như at, awk, cc, less, scp.
- `/usr/sbin`: có chứa các tập tin ứng dụng cho Admin hệ thống. Nếu không tìm thấy hệ nhị phân tại /sbin, bạn có thể tìm tại /usr/sbin. Chẳng hạn như atd, cron, sshd, useradd, userdel.
- `/usr/lib` chứa thư viện /usr/bin và /usr/sbin.
- `/usr/local` chứa các chương trình user mà bạn cài đặt từ nguồn.
Chẳng hạn khi bạn cài đặt apache từ nguồn, apache nằm dưới /usr/local/apache2.
## Variable Files
- Lưu lại tập tin ghi các số liệu biến đổi (variable files).
- Nội dung các tập tin được dự kiến sẽ tăng lên tại thư mục này.
`/var/log`: hệ thống tập tin log
`/var/lib`: các gói và các file dữ liệu
`/var/mail`" email
`/var/tmp`: các file tạm thời cần khi reboot
 `/var/www`: Dữ liệu cho trang web

Để biết được thư mục đang nằm trên phân vùng nào các bạn hãy sử dụng lệnh df với đối số là dấu chấm (.) biểu diễn thư mục hiện hành.
```sh
df -h .
Filesystem           Size  Used Avail Use% Mounted on
devtmpfs             484M     0  484M   0% /dev
tmpfs                496M     0  496M   0% /dev/shm
tmpfs                496M  6.9M  489M   2% /run
tmpfs                496M     0  496M   0% /sys/fs/cgroup
/dev/mapper/cl-root   37G  6.6G   31G  18% /
/dev/sda1           1014M  178M  837M  18% /boot
tmpfs                100M     0  100M   0% /run/user/0

```

