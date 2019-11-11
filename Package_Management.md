Package Management lưu trữ các chương trình phần mềm, file cấu hình và thông tin về các dependencies. Theo dõi các bản cập nhật và nâng cấp để tránh các lỗi về bảo mật.
Các tính năng của PMS
`package download`: cho phép users tải về các gói phần mềm từ nhà cung cấp tin cậy.
`Dependency resolution`: gói meta data cun
`A standard binary package format`
`Common installation and configuration locations`
`Additional system-related configuration and functionality`
`Quality control`
## Quản lý Package bằng RPM
RPM Package Manager (RPM) Gói cài đặt cho các hệ điều hành Linux họ Fedora,RedHat… Ví dụ: Centos OS

| Commands | Result |
|----------|--------|
| rpm -ivh [package.rpm] | Cài đặt gói package.rpm |
| rpm -e [package] | Gỡ bỏ rpm package |
| rpm -qa | Liệt kê tất cả các rpm package trong hệ thống. |
| rpm -qi [package] | Thu thập thông tin gói rpm package |
| rpm -U [package.rpm] | Nâng cấp gói package.rpm mà không thay đổi cấu hình file |
| rpm -F [package.rpm] | Nâng cấp gói package.rpm nếu nó đã được cài đặt |
| rpm -V [package] | Kiểm tra kích thức file, quyền, loại, chủ sở hữu, nhóm, mã MD5 và lần cuối chỉnh sửa |
| rpm -q [package] –changelog | Hiển thị lịch sử sửa đổi của gói rpm |

## YUM packages
YUM là phương pháp cài đặt cho các hệ điều hành Linux họ Fedora,RedHat… Ví dụ: Centos OS

| Commands | Result |
|----------|--------|
| yum -y install [package] | Tải và Cài đặt gói tin |
| yum remove [package] | Gỡ bỏ rpm package |
| yum list | Liệt kê tất cả các rpm package trong hệ thống. |
| yum update [package]| Cập nhật 1 gói rpm chỉ định |
| yum search [package | Tìm gói rpm trên kho. |

## DEB packages 
Gói ứng dụng cho các hệ điều hành Linux họ Debian, Ubuntu…

| Commands | Result |
|----------|--------|
| dpkg -i [package.deb] | Cài đặt/nâng cấp |
| dpkg -r [package] | Gỡ bỏ rpm package |
| dpkg -l | Liệt kê tất cả các rpm package trong hệ thống. |
| dpkg -s [package] | Thông tin gói tin |

## APT packages (Debian, Ubuntu, …)
Phương pháp cài đặt ứng dụng cho các hệ điều hành Linux họ Debian, Ubuntu…

| Commands | Result |
|----------|--------|
| apt-get install [package] | Cài đặt/nâng cấp |
| apt-get remove [package] | Gỡ bỏ rpm package |
| apt-get update | Cập nhật gói tin |
| apt-get upgrade | Nâng cấp tất cả gói tin đã cài đặt |

