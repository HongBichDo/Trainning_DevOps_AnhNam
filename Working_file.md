## Soạn văn bản với vi
- Chế độ command: di chuyển, cắt, dán.. phím `Esc`
- Chế độ Insert: phím `i`
- Chế độ Ex: Lưu và thoát phím `:`
## Xem nội dung file
**Hiển thị toàn bộ nội dung file với cat**
```sh
cat /etc passwd
```
Nhược điểm của cat là không xem hết được nội dung file nên buộc phải kết hợp với các câu lệnh khác.
**Lệnh more**
Lệnh more cho phép xem từng phân đoạn của file. Nhấn phím `Space` để xem hết phần nội dung còn lại
*Đối với lệnh more chỉ xem được từ đầu đến cuối. Không có lệnh để xem lại từ đầu*
**Phân trang với less**
Lệnh `less` bổ sung cho `cat` với tính năng phân trang dữ liệu giúp xem toàn bộ nội dung của một file dài. Sử dụng mũi tên lên, xuống hoặc phím `pg down` và `pg up` để cuộn văn bản. Gõ `Shift+G` để kéo xuống dưới văn bản và `g` để quay lên trên văn bản. Tìm kiếm từ khóa trong văn bản bằng phím `/`.
```sh
less /etc passwd
```
**Lệnh head**
Đọc phần đầu của file, head hiển thị 10 dòng ầu tiên. Muốn thay đổi số dòng muốn hiển thị thêm option `-n`
```sh
head -n 3 /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
```
**lệnh tail**
Hiển thị phần cuối của file
```sh
 tail -n 3 /etc/passwd
chrony:x:997:995::/var/lib/chrony:/sbin/nologin
jenkins:x:996:992:Jenkins Automation Server:/var/lib/jenkins:/bin/false
bichdth:x:1000:1000::/home/bichdth:/bin/bash
```
## Tìm kiếm file
** Lệnh find
- Tìm kiếm theo tên: option –name
```sh
find / -name root
/dev/cl/root
/proc/1/task/1/root
/proc/1/root
find /etc –name root
/etc/selinux/targeted/contexts/users/root

```
- Tìm kiếm những file có đuôi là `.conf`
```sh
find /etc –name *.conf
/etc/security/pwquality.conf
/etc/security/access.conf
/etc/security/chroot.conf
```
- Tìm kiếm theo kích cỡ file: option –size (+- đơn vị k)
```sh
find /etc –size 1000k
find /etc –size +1000k
```
- Tìm kiếm file mới bị thay đổi: option –ctime(-day)
```sh
find /etc –ctime 2
```
Ngoài ra, có thể kết hợp cả 3 option để tìm kiếm file
```sh
find /etc –size +1000 –name *.bin –ctime -100
```
## So sánh các file
Sử dụng lệnh `diff` để so sánh 2 file với các option
`-c` cung cấp 3 dòng trước và sau của sự khác nhau
`-i` bỏ qua chữ cái
`-w` bỏ qua khoảng trắng
Ngoài ra còn có thể sử dụng lệnh diff 3 để so so sánh 3 file một lúc. Sử dụng một file trung gian làm tham chiếu cho 2 file còn lại
```sh
cat file1 file2 file3
thi is file1
this IS file
this is  file
diff file2 file3
1c1
< this IS file
---
> this is  file
diff -i file2 file3
1c1
< this IS file
---
> this is  file
diff -i -w  file2 file3
diff3 -i file1 file2 file3
====
1:1c
  thi is file1
2:1c
  this IS file
3:1c
  this is  file
```
