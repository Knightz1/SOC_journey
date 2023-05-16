## Rule

### Header
- Rule Action: Log, alert, pass, activate, or dynamic. Phổ biến nhất là `alert` giúp ghi lại gói tin và hành động xảy ra rồi cảnh báo cho admin.

- Protocol: ip, icmp, udp, tcp

- IP Addresses: có thể tạo list như `[192.168.1.0/24,10.1.1.0/24]`, dùng `any` để nhận bất kì địa chỉ 

- Port: có thể tạo dãy địa port như `1:1024`

- Direction Operators: `->` là phổ biến nhất, nằm bên trái dấu là source, bên phải là destination

### Option
