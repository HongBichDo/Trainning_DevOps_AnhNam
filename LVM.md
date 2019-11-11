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
* Tạo physical volume
