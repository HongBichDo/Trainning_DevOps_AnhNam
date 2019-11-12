
Hầu hết các máy tính ngày nay đều có một card Ethernet để nối vào mạng LAN. Khi cài đặt Linux, thiết bị này được gọi là eth0. 
`ip a`: địa chỉ IP
`ip route` : default gateway
`cat /etc/resolv.conf`: khai báo DNS
Trên máy linux thường có 2 card mạng nằm tại `etc/sysconfig/network-scripts`trong đó có 2 file cần chú ý như sau:
- `ifcfg-lo`: LOOPBACK
- `ifcfg-enp0s3`: cấu hình mạng LAN (tùy thuộc vào máy tính)

## Cấu hình địa chỉ IP
Thông thường khi cài đặt Linux xong sẽ có địa chỉ IP là động. Muốn cấu hình IP tĩnh làm như sau:
```sh
ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
   link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
   inet 127.0.0.1/8 scope host lo
   valid_lft forever preferred_lft forever
   inet6 ::1/128 scope host
   valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
   link/ether 08:00:27:1d:ea:ec brd ff:ff:ff:ff:ff:ff
   inet 10.0.2.15/24 brd 10.0.2.255 scope global noprefixroute dynamic enp0s3
   valid_lft 85680sec preferred_lft 85680sec
   inet6 fe80::6260:2512:3a6d:9ddb/64 scope link noprefixroute
   valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
   link/ether 08:00:27:6d:28:b5 brd ff:ff:ff:ff:ff:ff
   inet 192.168.56.101/24 brd 192.168.56.255 scope global noprefixroute dynamic enp0s8
   valid_lft 994sec preferred_lft 994sec
   inet6 fe80::440:1403:1f5c:c295/64 scope link noprefixroute
   valid_lft forever preferred_lft forever

```

## Route
```sh
ip route
default via 10.0.2.2 dev enp0s3 proto dhcp metric 100
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100
```
## Thay đổi địa chỉ IP
```sh
cd /etc/sysconfig/network-scripts
ls 
vi ifcfg-enp0s3
```
Onboot = yes >> bật khi máy tính khởi động
Thêm một số cài đặt vào file `ifcfg-enp0s3` sau đórestart lạiservice để nhận địa chỉ IP mới.
```sh
IPADDR =192.168.56.101 
NETMASK =255.255.255.0
GATEWAY=192.168.56.1
Services network restart
Restarting network (via systemctl):                        [  OK  ]
```

## Các lệnh Troubleshoot mạng cơ bản
`ip a`
`ping`
`nslookup`
`telnet`

Ping đến địa chỉ IP là 192.168.56.101 xem có phản hồi hay không.
```sh
ping 192.168.56.101
PING 192.168.56.101 (192.168.56.101) 56(84) bytes of data.
64 bytes from 192.168.56.101: icmp_seq=1 ttl=64 time=0.066 ms
64 bytes from 192.168.56.101: icmp_seq=2 ttl=64 time=0.255 ms
64 bytes from 192.168.56.101: icmp_seq=3 ttl=64 time=0.209 ms
64 bytes from 192.168.56.101: icmp_seq=4 ttl=64 time=0.117 ms
64 bytes from 192.168.56.101: icmp_seq=5 ttl=64 time=0.118 ms
```
Để tra cứu bản DNS xem có trả về địa chỉ hay không sử dụng `nslookup`. Cần cài đặt trước khi sử dụng
```sh
yum install bind-utils
nslookup
> facebook.com
Server:         192.168.1.1
Address:        192.168.1.1#53

Non-authoritative answer:
Name:   facebook.com
Address: 157.240.13.35
Name:   facebook.com
Address: 2a03:2880:f139:183:face:b00c:0:25de
> facebook.com
Server:         192.168.1.1
Address:        192.168.1.1#53

Non-authoritative answer:
Name:   facebook.com
Address: 157.240.13.35
Name:   facebook.com
Address: 2a03:2880:f139:183:face:b00c:0:25de
```
Kiểm tra facebook có đang sử dụng dịch vụ https hay không, sử dụng lệnh `telnet`
```sh
yum install telnet -y
telnet facebook 80
Trying 125.235.4.59...
```
Dịch vụ http đang được sử dụng ở port 80. Khi telnet facebook ở port 80 dòng lệnh `Trying` ở trạng thái đứng yên tức là không sử dụng dịch vụ. Để thoát `Crtl + ] quit`
