<p align="center">
  <img src="https://user-images.githubusercontent.com/91442807/236667588-b0fad650-6aaa-4302-be3d-aaf54b549d55.png"/>
</p>

Bài này muốn tìm ra địa chỉ của 3 tên cướp đang ẩn náu sau khi cướp ngân hàng.

Database bao gồm `VIN`(vehicles ID), thời điểm và địa chỉ của xe tại thời điểm đó. Database này chứa thông tin của các phương tiện trong khoảng thời gian từ 8h->11h.

<p align="center">
  <img width="400" height="400" src="https://user-images.githubusercontent.com/91442807/236667780-a4ce5563-ba6f-4858-9751-f14512038318.png"/>
</p>

Ta biết được thời gian vụ cướp là từ `8h17-8h31` và thời gian tẩu thoát từ `8h31-8h40` và địa chỉ ngân hàng là `157th Ave / 148th Street`

Đầu tiên ta lọc các phương tiện nằm ở địa chỉ ngân hàng ở thời gian tẩu thoát:

<p align="center">
  <img width="400" height="400" src="https://user-images.githubusercontent.com/91442807/236668410-8d1325bf-ba04-4849-9ef3-fc8664831266.png"/>
</p>

Tiếp đến là `join` kết quả với bảng `Traffic` để lấy hết tất cả luồn di chuyển của các phương tiện đó trong khoảng từ `8h-11h`. Sau đó lọc ra thời gian cuối cùng của phương tiện đó được lưu:

<p align="center">
  <img width="400" height="400" src="https://user-images.githubusercontent.com/91442807/236668859-60cd4e9c-0c2d-4ef6-9bbd-eda01d79c533.png"/>
</p>

Sau đó `join` lần nữa với bảng `Traffic` để lấy thông tin về địa chỉ của phương tiện ở lần cuối cùng đó rồi lọc tiếp ở mỗi địa chỉ có bao nhiêu phương tiện vì cuối cùng 3 tên cướp sẽ tụ lại với nhau ta được:

<p align="center">
  <img width="400" height="400" src="https://user-images.githubusercontent.com/91442807/236669089-e3fe10c9-2816-44f3-82e6-a5adb6800a66.png"/>
</p>




