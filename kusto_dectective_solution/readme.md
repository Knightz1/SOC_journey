Link challenges: https://detective.kusto.io/inbox

## 1. The rarest book is missing!

- Mô tả: 
Có 2 bảng data là `Books` và `Shelves`:

![image](https://user-images.githubusercontent.com/91442807/236636652-c92bd703-98dc-45ee-aa43-208645c8459a.png)

![image](https://user-images.githubusercontent.com/91442807/236636661-c91e8b73-18e8-4336-b76b-0cd50e9111bc.png)

Mỗi quyển sách có `rfid` riêng và người ta tìm thấy `rfid` của cuốn `De Revolutionibus Magnis Data` trên sàn. Nhiệm vụ là tìm kệ sách để trả quyển sách này về kệ đúng.

- Hướng làm:
Xem thử 10 dòng dữ liệu đầu của `Shelves`:
![image](https://user-images.githubusercontent.com/91442807/236636804-d2fb7e6a-8551-4a97-8e9c-591875bcade3.png)

Ta thấy ở cột `rfids` chứa các `rfid` của các quyển sách trong kệ đó và `total_weigth` là tổng khối lượng của các quyển sách trong kệ.

Vậy để tìm ra kệ ta cần liệt kê các cuốn sách có trong kệ rồi cộng tổng khối lượng của nó rồi so sánh với `total_weight`, nếu khác biệt quá nhiều thì đó là kệ cần tìm.

- Giải:



