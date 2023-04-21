## Phương phác xác thực Kerberos trong AD (Active Directory)
```
- Bước 1: User cấp username, password và domain name cho máy client.
- Bước 2: Client tiến hành đóng gói thông tin thành 1 package hoặc có tên khác là ‘authenticator’, chứa các thông tin liên quan tới client, bao gồm username, ngày giờ (timestamp)… Ngoài username ra thì tất cả các info khác đều được mã hoá bằng password của người dùng.
- Bước 3. Client gửi encrypted authenticator đó tới KDC (Key Distribution Center).
- Bước 4. KDC check xem username nào đang gửi request tới, rồi nó lấy password của username đó đang được lưu trong databases, tiến hành decrypt thằng ‘authenticator’ với password đó. Nếu KDC có thể decrypt được thì danh tính của thằng user được xác minh là đúng.
- Bước 5. Nếu verify thành công thì thằng KDC (cụ thể là AS – Authentication Server) sẽ tạo ra 1 ticket, nó cũng được encrypted và gửi lại về client (encrpyt bằng key của KRBTGT (key này chính là hash của password krbtgt user trên AD)), ticket đó được gọi là Ticket Granting Ticket (TGT).
- Bước 6. Ticket sau khi nhận được lưu trữ trong Kerberos tray của client và được sử dụng để truy cập vào Server trong 1 thời gian nhất định (thường là 8 tiếng). Đến đây thì người dùng đã được xác thực trong domain.
```


## Các phương pháp tấn công 

### 1. Silver ticket

Khi khách hàng cần sử dụng một dịch vụ, họ sẽ yêu cầu TGS(Ticket Granting Service). Quá trình này sẽ thông qua 2 request là
`KRB_TGS_REQ` và `KRB_TGS_REP`

TGS được mã hóa bằng `NT hash` của `account đang chạy dịch vụ đó (service account)` 

- Do đó nếu có thể lấy được `NT hash` của  `service account`, có thể tạo được một TGS giả mạo.

Sơ đồ mô tả cách tấn công:

![image](https://user-images.githubusercontent.com/91442807/233393185-439d77aa-71b0-4aaa-93b3-c59a50c15640.png)

- Detect:
```
Ticket Encryption type = 0x17 
Ticket options = 0x40810000
```
![image](https://user-images.githubusercontent.com/91442807/233650263-3f229438-03e4-419c-bd56-2c2ba87b04ea.png)


### 2. Golden ticket

Giả mạo TGT(Ticket-Granting Ticket)

- Với `TGT`, người dùng có thể yêu cầu `TGS` cho bất kì dịch vụ nào.

- Để có thể giả mạo `TGT`, ta cần biết key đã mã hóa nó và đó là hash của `krbtgt(Active Directory Key Distribution Service Account) account` .

Sơ đồ tấn công.

![image](https://user-images.githubusercontent.com/91442807/233398079-152b9e09-4aa7-4444-ae35-f9e82897a8b4.png)

- Detect:
```
Fake/blank acount name
```

![image](https://user-images.githubusercontent.com/91442807/233650183-2ceac33f-00c3-4f08-9190-e8b523a55887.png)



### 3. AS-REP Roasting
Muốn thực hiện kiểu tấn công này, phải đạt được điều kiện cần thiết, đó là `Tài khoản không yêu cầu Kerberos pre-authentication`.

- Cái trường hợp mà bị tắt cái `pre-authentication` rất hiếm hầu như ko xảy ra nên cách tấn công này hầu như không được sử dụng.

Dù sao trong trường hợp nó bị tắt:

- Bất kì ai cũng có thể yêu cầu `TGT` dựa trên tên của một số tài khoản đã biết (fuzz hay gì đó...) và kết quả trả về `KRB_AS_REP` 

![image](https://user-images.githubusercontent.com/91442807/233421281-e5afc358-ccf8-48f5-8957-fae957162b02.png)

- Khi lấy được `KRB_AS_REP` thì attacker có thể lấy password của user dựa trên phần encrypt (bằng brute force,....)

### 4. Kerberoasting

Attacker (lúc này đã được xem như `domain user` hợp lệ), yêu cầu `Kerberos service ticket` cho bất kì dịch vụ nào, lấy được `TGS` từ bộ nhớ và crack được thông tin tài khoản sử dụng các công cụ có sẵn.

- Theo thiết kế của Kerberos, `TGS` sẽ được mã hóa bằng `NTLM hash của service account` mà `service account` là `domain user account` và `host user account`.
- Kerberoasting chỉ có tác dụng với `domain user` bởi vì mật khẩu của `host user` có độ dài 128 kí tự và đổi mỗi 30 ngày -> rất khó để crack.

- Detect:
```
Domain user yêu cầu một số lượng lớn service ticket (eventID 4769).
Phân tích gói TGS-REQ trong Windows Event Logs để tìm các hành vi đáng ngờ (như RC4).
```

