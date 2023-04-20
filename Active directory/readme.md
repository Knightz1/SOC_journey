

### KRB_AS_REQ
Người dùng sẽ gửi một request để lấy `TGT` đến `KDC` thì request đó gọi là `KRB_AS_REQ`.

- Các bước:

Để yêu cầu lấy `TGT`, người dùng sẽ gửi `username`, `timestamp(thời gian lúc yêu cầu TGT)` mã hóa cùng với hash của password.
KDC  sẽ xem `username` có nằm trong database hay không. Nếu có thì KDC sẽ lấy `hash password` để decrypt `timestamp`, nếu đúng thì nó sẽ tiến hành gửi `TGT` về cho user.

### KRB_AS_REP
Đây là quá trình `KDC` gửi `TGT` về lại cho user.

`TGT` chứa các thông tin:
```
Username 
Validity period
Generated session key
The Privilege Attribute Certificate (PAC) which contains a lot of specific information about the user, including his identifier (SID) and all the groups he is member of.
```

- TGT được encrypt cùng lúc với `KDC key`, do đó chỉ `KDC` mới có thể decrypt và đọc nội dung của `TGT`.


### 1. Silver ticket

Khi khách hàng cần sử dụng một dịch vụ, họ sẽ yêu cầu TGS(Ticket Granting Service). Quá trình này sẽ thông qua 2 request là
`KRB_TGS_REQ` và `KRB_TGS_REP`

TGS được mã hóa bằng `NT hash` của `account đang chạy dịch vụ đó (service account)` 

- Do đó nếu có thể lấy được `NT hash` của  `service account`, có thể tạo được một TGS giả mạo.

Sơ đồ mô tả cách tấn công:

![image](https://user-images.githubusercontent.com/91442807/233393185-439d77aa-71b0-4aaa-93b3-c59a50c15640.png)


### 2. Golden ticket

Giả mạo TGT(Ticket-Granting Ticket)

- Với `TGT`, người dùng có thể yêu cầu `TGS` cho bất kì dịch vụ nào.

- Để có thể giả mạo `TGT`, ta cần biết key đã mã hóa nó và đó là hash của `krbtgt(Active Directory Key Distribution Service Account) account` .

Sơ đồ tấn công.

![image](https://user-images.githubusercontent.com/91442807/233398079-152b9e09-4aa7-4444-ae35-f9e82897a8b4.png)


