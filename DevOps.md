# DevOps????
* Hiểu gì về DevOps ??
-  Developer code + code + code : development
- Code done >> test +  deploy trước khi bàn giao sản phẩm cho khách hàng: operations
- Nếu tách biệt 2 quá trình này ra: code xong >> test, deploy >> không đạt yêu cầu quay lại code đến khi test OK. Nếu đạt yêu cầu thì Ok không sao cả. Nhưng nếu không >> mất time, công sức... DevOps kết hợp 2 quá trình này lại với nhau. Cả 2 đều được thực hiện song song với nhau. Coder, Tester Sysadmin hỗ trợ nhau cho đến khi sản phẩm được hoàn thành.
* DevOps = Dev + Ops

# DevOps Concepts
## Build Automation
- deploy code = script/tool
- command - line tool, không phụ thuộc IDE

## CI
- auto test detect issue khi merge code
- commit code >> CI thực hiện build, test source code 
- CI phát hiện bug, developer fix bug tránh ảnh hưởng người khác

## CD
* Continuous Delivery

* Continuous Deployment
## program language:
* Java 
* JS 

## OS concepts
* Virtualization:
- config mạng 
- cách check info  :
    + CPU/ RAM/ 
    + os  :lamf sao biết vm đang vô là os gì , 32/64bit 
    + disk : check space / check disk / sector /cách mount disk
    + set up firewall/ check / các issue về firewall search ra  
    + set up dns /cách check cho mỗi os / các issue về dns nếu gặp
    + folder log system/ service nằm ở đâu / service sau khi được cài đặt mặc định đi đâu / log sẽ ra chỗ nào / làm sao check được service đó đang chạy hay không ....
- Linux

## Networking & Security
* Networking : IP / subnetmask / các hop  và 1 số command check network trong linux như :
    + traceroute 
    + nc 
    + nslookup
    + ping 
    + trace
    + telnet 
    + curl
* ISO Model, HTTP, HTTPS, TCP/IP
- cũng phải hiểu rõ nhá 
- http khác https ở đâu 
- trong devops thì cần quan tâm gì về nó : 
- Http port đi cùng nó là gif , có cần SSL không 
- HTTPS port đi cùng nó là gì , có cần SSL không 
- cách generate SSL như thế nào 
- các cách gen SSL 

## What is and how to setup 
* Web Server : Apache, Tomcat 
- Cách install / manage nó 
- Apache/Tomcat khác Nginx như thế nào 
- cách set up nó

* set up : 
- Đặt tên domain ( link tới SSL ở trên - nếu có)
- setup sao cho chạy được source 
- apache / nginx cơ bản cần setup cái gì / ở đâu / log access ở đâu / log error ở đâu , config map IP với domain chỗ nào

## Infastructure as Code
* Docker
* Kubernetes: quản lý service (quản lý container....)

## CI/CD Tool
* Jenkins: 
- admin system jenkins 
- start jenkins như thế nào 
- install jnekins , log access ở đâu , secret token default nằm chỗ nào 
- access jenkins khi mất user/pwd
- start success / như nào là fail  >> log ???
- quá trình jenkins start nó process những gì?
