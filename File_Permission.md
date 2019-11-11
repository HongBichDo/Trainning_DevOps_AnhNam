## Permission đối với file/folder
**Mỗi đối tượng gắn với 3 loại quyền: read, write, execute. Mỗi quyền được chỉ định cho 3 loại Users**
* owner: mặc định là user tạo ra đối tượng
* group: nhóm user có quyền giống nhau, mặc định ban đầu là group mà owner ở trên
* other: tất cả user không thuộc 2 loại trên

## Phân loại quyền đối với file
* Read: cho phép xem đối tượng có trong thư mục.
* Write: CHo phép tạo và xóa cácđối tượng.
* Execute: cho phép chạy file
*User root có đủ cả 3 quyền đối với mọi đối tượng trên hệ thống. Ngoài ra, root có thể thay đổi (cấp hoặc tước) quyền hạn truy cập đối tượng cho bất kỳ user nào và còn có thể chuyển quyền sở hữu đối tượng qua lại giữa các user.*

## Command 

| Commands | Result | Syntax |
|----------|--------|--------|
| chmod | change mode - thay đổi quyền hạn với file | chmod [option] [MODE ] <file> |
| chown | change owner - thay đổi quyền sở hữu | chown [option] user:group <file> |
| chgrp | change group thay đổi nhóm sở | chgrp [option] <group> <file> |

## Danh sách các mode
| # | Permission | rwx |
|---|------------|-----|
| 7 | read, write and execute | rwx |
| 6 | read and write | rw- |
| 5 | read and execute | r-x |
| 4 | read only | r- |
| 3 | write and execute | -wx |
| 2 | write only | -w- |
| 1 | execute only | -x |
| 0 | none | -- |
## Example 
Tạo file abc.txt
```sh
touch abc.txt
ls -l abc.txt 
-rw-r--r-- 1 root root 0 Nov  6 18:59 abc.txt 
```
*File abc.txt vừa được tạo đang thuộc quyền sở hữu của Users root, group Users root. Sử dụng `chown` để thay đổi chủ sở hữu nhóm sở hữu*
```sh
chown bichdth.bichdth abc.txt
-rw-r--r-- 1 bichdth bichdth 0 Nov  6 18:59 abc.txt
```
Các chỉ số phân quyền của file abc.txt như sau:
`-rw`: quyền của Owner
-`-r-`: quyền của các Users thuộc group sở hữu
`-r-`: quyền cho các Users khác

```sh
Phân quyền đói với file sử dụng `chmod`
chmod 775 abc.txt
-rwxrwxr-x 1 bichdth bichdth 0 Nov  6 18:59 abc.txt
```
