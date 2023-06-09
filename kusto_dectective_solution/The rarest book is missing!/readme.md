Link challenges: https://detective.kusto.io/inbox

## 1. The rarest book is missing!

- Mô tả: 

Có 2 bảng data là `Books` và `Shelves`:
<p align="center">
 <img src="https://user-images.githubusercontent.com/91442807/236636652-c92bd703-98dc-45ee-aa43-208645c8459a.png"/>
</p>

<p align="center">
<img src="https://user-images.githubusercontent.com/91442807/236636661-c91e8b73-18e8-4336-b76b-0cd50e9111bc.png">
 </p>

Mỗi quyển sách có `rfid` riêng và người ta tìm thấy `rfid` của cuốn `De Revolutionibus Magnis Data` trên sàn. Nhiệm vụ là tìm kệ sách để trả quyển sách này về kệ đúng.

- Hướng làm:
Xem thử 10 dòng dữ liệu đầu của `Shelves`:
<p align="center">
 <img width="400", height="400" src="https://user-images.githubusercontent.com/91442807/236636804-d2fb7e6a-8551-4a97-8e9c-591875bcade3.png"/>
</p>


Ta thấy ở cột `rfids` chứa các `rfid` của các quyển sách trong kệ đó và `total_weigth` là tổng khối lượng của các quyển sách trong kệ.

Vậy để tìm ra kệ ta cần liệt kê các cuốn sách có trong kệ rồi cộng tổng khối lượng của nó rồi so sánh với `total_weight`, nếu khác biệt quá nhiều thì đó là kệ cần tìm.

- Giải:

Để liệt kê từng quyển trong mỗi kệ, ta dùng lệnh `mv_expand`:

<p align="center">
 <img width="400", height="400" src="https://user-images.githubusercontent.com/91442807/236637208-c309ccf1-5f84-43b0-b93c-d73ca4f51d10.png"/>
</p>

Ở trên liệt kê ra từng `rfid` của từng quyển trên kệ `1395`.

Tiếp đến ta kết hợp với bảng `Books` dựa trên `rfid` để lấy `weight_gram` của từng quyển dùng lệnh `join`:

<p align="center">
 <img width="400" height="400" src="https://user-images.githubusercontent.com/91442807/236637393-7c9fc4cf-be9e-4d0a-ad78-b2dbf9935561.png"/>
</p>

Tiếp đến là cộng khối lượng từng quyển trên mỗi kệ lại dùng lệnh `summarize`:

<p align="center">
 <img width="400", height="400" src="https://user-images.githubusercontent.com/91442807/236637504-b22d80b9-26bb-476b-abdb-ecf19da4a3bb.png"/>
</p>

Tiếp đến là tiến hành so sánh xem kệ này có weight bị lệch nhiều nhất:

<p align="center">
 <img width="400", height="400" src="https://user-images.githubusercontent.com/91442807/236637635-1884d855-3c3d-4b90-9a26-001f869c5fc9.png"/>
</p>

Ta được kết quả là kệ `4242`






