**Sử dụng `cat` để xem các cấu hình về hệ thống**
## Các lệnh kiểm tra thông tin hệ thống Linux
| Commands | Result |
|----------|--------|
| cat /etc/os-release | Kiểm tra thông tin |
| cat /proc/cpuinfo | 	Kiểm tra thông tin CPU |
| cat /proc/meminfo | Kiểm tra thông tin về RAM |
| cat /proc/version | Kiểm tra phiên bản của Kernel |
| uname -a | Kiểm tra các thông tin về Kernel |
| cat /etc/redhat-release | Kiểm tra phiên bản Centos |
| free -m | Kiểm tra dung lượng RAM còn trống |
| df -h | Hiển thị thông tin file hệ thống |
| hostname | Xem tên máy |
| lspci | Xem thông tin mainboard   /sbin/ifconfig Xem các địa chỉ IP của máy |

Kiểm tra thông tin
```sh
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"
```

Để xem các thông tin về phần cứng cần xuất nội dung các tập tin `proc` ra màn hình
```sh
cat /proc/cpuinfo
model name      : Intel(R) Core(TM) i5-8250U CPU @ 1.60GHz
cpu MHz         : 1800.001
cache size      : 6144 KB
```

```sh
cat /proc/version
Linux version 3.10.0-1062.1.1.el7.x86_64 (mockbuild@kbuilder.bsys.centos.org) (gcc version 4.8.5 20150623 (Red Hat 4.8.5-39) (GCC) ) #1 SMP Fri Sep 13 22:55:44 UTC 2019

```
```sh
free -m
        total        used        free      shared  buff/cache   available
Mem:            990         487          62           6         440         343
Swap:          2047           0        2047

```
Thông tin về bộ nhớ đangđược sử dụng và dung lượng trống là bao nhiêu. Swap là bộ nhớ hoán đổi. Khi nào RAM dùng nhiều và đầy thì có thể chuyển qua sử dung Swap. 
```sh
hostname
BichDTH
```
```sh
```
```sh
```