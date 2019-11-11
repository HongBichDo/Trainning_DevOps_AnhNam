## LVM trong Linux
LVM (Logical Volume Manager) là một kỹ thuật cho phép tạo ra các vùng không gian đĩa cứng ảo khiến cho việc thay đổi dung lượng dễ dàng hơn. LVM giúp bạn:
- Nới rộng hoặc thu hẹp không gian lưu trữ mà không cần phải chia lại partition trên đĩa cứng.
- Gom nhiều ổ đĩa cứng vật lý thành một ổ đĩa ảo có dung lượng lớn hơn.
Sử dụng LVM để có thể gom nhiều đĩa cứng vật lý thành một đĩa ảo với dung lượng lớn. Đồng thời còn có thể tạo ra các vùng dung lượng lớn nhỏ tùy ý. Có thể thay đổi các vung dung lượng đó dễ dàng hơn.
Tuy nhiên, LVM có các bước thiết lập phức tạp và khó khăn. Hệ thống khởi động chậm nếu gắn nhiều đĩa cứng và thiết lập nhiều LVM. Khi các đĩa cứng bị hỏng, khả năng mất dữ liệu cao.
## Mô hình LVM
- Physical volumes: là những đĩa cứng vật lý hoặc partition trên nó như: `/dev/sda` hoặc `/dev/sdb1`.
- Volume groups: là một nhóm bao gồm các Physical volumes. Volume group được xem như 1 “ổ đĩa ảo”.
- Logical volumes: Một Volume Groupđược chia thành nhiều Logical volume. Nó được dùng cho các để mount tới hệ thống tập tin (File System) và được format với những chuẩn định dạng khác nhau như ext2, ext3, ext4…
- File systems: hệ thống tập tin quản lý các file và thư mịc trên ổ đĩa. Chúngđược mount tới các Logical Volume trong LVM.

## Tạo và quản lý Logical Volume Manager
### Physical volume
Chạy lệnh sau để tạo physical volume(PV) trên `/dev/sdb`, `/dev/sdc`, và `/dev/sdd`
```sh
fdisk -l
Disk /dev/sda: 42.9 GB, 42949672960 bytes, 83886080 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: dos
Disk identifier: 0x000a75ce

Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048     2099199     1048576   83  Linux
/dev/sda2         2099200    83886079    40893440   8e  Linux LVM
```
Để liệt kê các physical volume(PV) mới được tạo, chạy như sau:
```sh
pvs 
PV         VG Fmt  Attr PSize   PFree
/dev/sda2  cl lvm2 a--  <39.00g 4.00m
```
Để có được thông tin chi tiết về mỗi physical volume(PV), sử dụng lệnh sau `pvdisplay`
Xem thông tin chi tiết về physical volume(PV) /dev/sda. Chúng ta thực hiện như sau:
```sh
pvdisplay /dev/sda
--- Physical volume ---
  PV Name               /dev/sda2
  VG Name               cl
  PV Size               <39.00 GiB / not usable 3.00 MiB
  Allocatable           yes
  PE Size               4.00 MiB
  Total PE              9983
  Free PE               1
  Allocated PE          9982
  PV UUID               brEcMX-44Zb-5J1d-v8Yd-w92z-aqsX-mAXEcd
```
### Volume Group
```sh
vgdisplay
--- Volume group ---
  VG Name               cl
  System ID
  Format                lvm2
  Metadata Areas        1
  Metadata Sequence No  3
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                2
  Open LV               2
  Max PV                0
  Cur PV                1
  Act PV                1
  VG Size               <39.00 GiB
  PE Size               4.00 MiB
  Total PE              9983
  Alloc PE / Size       9982 / 38.99 GiB
  Free  PE / Size       1 / 4.00 MiB
  VG UUID               HorZNX-m19L-Tdpz-9ceU-38cF-Dc6F-uNIFhu
```
- VG Name: tên volume Group
- Format: kiến trúc LVM được sử dụng
- Total PE: Tổng dung lượng có
Để kiểm tra số lượng physical volume(PV) dùng để tạo volume group sử dụng `vgs`
```sh
vgs
VG #PV #LV #SN Attr   VSize   VFree
cl   1   2   0 wz--n- <39.00g 4.00m
```  
Khi tạophysical Volume, cần xem xét dung lượng sao cho phù hợp nhu cầu sử dụng.

### Logical Volume
Xem danh sách logical volume vừa được tạo với lệnh `lvs`
```sh
lvs
LV   VG Attr       LSize  Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
root cl -wi-ao---- 36.99g
swap cl -wi-ao----  2.00g
```
- LV: Tên logical volume
- Data%: Phần trăm dung lượng logical volume được sử dụng
- Lsize: Kích thước logical volume

