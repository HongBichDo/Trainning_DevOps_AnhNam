Iptables Linux firewall được sử dụng trong Linux để theo dõi lưu lượng truy cập đến và đi ở một máy chủ. Dựa trên các rules để ngăn chặn quyền truy cập vào hệ thống. Iptables sử dụng để định nghĩa các rules cho người dùng.
Iptables là một ứng dụng dòng lệnh và là firewall của Linux. Một gói tin khi đã được xác định để gửi đi đều có các `target` như sau:
- `ACCEPT` gói tin được phép đi qua
- `DROP` gói tin không được phép qua
- `RETURN` bỏ qua target hiện tại và quay lại 
Trên Linux có sẵn 1 firewall là Framework lọc gói tin là netfilter (theo IP và Port) sử dụng IPtable thiết lập các luật của firewall.

## Cài đặt iptables
Iptable được cài đặt sẵn trongLinux. 
Đối với CenOS7 cần disable firewalld trước khi sử dụng iptables. 
 ```sh
rpm –qa | grep firewalld
systemctl stop firewalld 
systemctl disable firewalld 
```
Cài đặt iptables trên hệ thống và enable 
```sh
rpm –qa | grep iptables
Yum install iptables-services –y
systemctl enable iptables
systemctl start iptables
systemctl status iptables
```
## Kiểm tra trạng thái hiện tại của iptables
Để kiểm tra trạng thái hiện tại của iptables dùng lệnh `iptables -L`. Option `-L` để liệt kê tất cả các bộ rules.
```sh
iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination
ACCEPT     all  --  anywhere             anywhere             state RELATED,ESTABLISHED
ACCEPT     icmp --  anywhere             anywhere
ACCEPT     all  --  anywhere             anywhere
ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:ssh
REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination
REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
```
Cả 3 chainsđược thiết lập mặc định là ACCEPT và không có rules nào cả. 

## Thiết lập mở port 80 
Thông tin các port đang được mở trên Linux tại `/etc/sysconfig/iptables`. Để mở port 80 cho http cần thêm dòng `-A INPUT -p tcp -m state --state NEW -m tcp --dport 80 ` 
```sh
vi /etc/sysconfig/iptables
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 22
-A INPUT -p tcp -m state --state NEW -m tcp --dport 80 
-j ACCEPT
-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
COMMIT
```
Để mở port cần restart lại dịch vụ iptable bằng lệnh `systemctl restart iptables` sau đó kiểm tra lại trạng thái
```sh
iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination
ACCEPT     all  --  anywhere             anywhere             state RELATED,ESTA                                                                                     BLISHED
ACCEPT     icmp --  anywhere             anywhere
ACCEPT     all  --  anywhere             anywhere
ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:                                                                                     ssh
ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:                                                                                     http
REJECT     all  --  anywhere             anywhere             reject-with icmp-h                                                                                     ost-prohibited

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination
REJECT     all  --  anywhere             anywhere             reject-with icmp-h                                                                                     ost-prohibited

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
```
Như vậy là cổng 80 đã được mở thành công !

##  Lọc các gói tin dựa trên nguồn của nó
Nếu muốn cho phép hay từ chối các gói tin dựa trên một IP nào đó sử dụng tham số `-s`
```sh
iptables -A INPUT -s 192.168.1.3 -j ACCEPT
iptables -A INPUT -s 192.168.1.4 -j DROP
iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination
ACCEPT     all  --  anywhere             anywhere             state RELATED,ESTABLISHED
ACCEPT     icmp --  anywhere             anywhere
ACCEPT     all  --  anywhere             anywhere
ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:ssh
ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:http
REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited
ACCEPT     all  --  192.168.1.3          anywhere
DROP       all  --  192.168.1.4          anywhere
```
 ## Xóa các rules
 Có thể xóa oàn bộ các rules để tạo mới từ đầu với `iptables -F` hoặc xóa từng rules sử dụng tham số -D
 ```sh
 iptables -L --line-numbers
 Chain INPUT (policy ACCEPT)
num  target     prot opt source               destination
1    ACCEPT     all  --  anywhere             anywhere             state RELATED,ESTABLISHED
2    ACCEPT     icmp --  anywhere             anywhere
3    ACCEPT     all  --  anywhere             anywhere
4    ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:ssh
5    ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:http
6    REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited
7    ACCEPT     all  --  192.168.1.3          anywhere
8    DROP       all  --  192.168.1.4          anywhere
 ```
 Các số thứ tự tương ứng với từng bộ rules. Nếu bạn muốn cho phép nhận gói tin từ địa chỉ 192.168.1.4 sử dụng lệnh
 ```sh
 iptables -D INPUT 8
 Chain INPUT (policy ACCEPT)
target     prot opt source               destination
ACCEPT     all  --  anywhere             anywhere             state RELATED,ESTABLISHED
ACCEPT     icmp --  anywhere             anywhere
ACCEPT     all  --  anywhere             anywhere
ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:ssh
ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:http
REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited
ACCEPT     all  --  192.168.1.3          anywhere
 ```

## Lưu trữ các thay đổi
Các iptables rules sau khi tạo ra sẽ được lưu vào bộ nhớ. Khi reboot máy chủ cần thực hiện lưu lại những bộ rules này.
Để lưu vào cấu hình hệ thống sử dụng
`/sbin/iptables-save`