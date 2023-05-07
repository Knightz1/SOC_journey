

<p align="center">
   <img src="https://user-images.githubusercontent.com/91442807/236638918-702aebf2-6aad-409c-a237-b182569e7ad1.png" />
</p>

- Mô tả:

Bài này muốn ta kiểm tra xem có gian lận phiếu bầu hay không và sửa lại cho đúng.

Chỉ có một cột `Votes`:

<p align="center">
   <img width="400" height="400" src="https://user-images.githubusercontent.com/91442807/236639374-5fed2c05-37c2-45b5-8d3c-bd117e43f35f.png" />
</p>

Chạy cái script tính % vote mà đề cho thử:

<p align="center">
   <img width="400" height="400" src="https://user-images.githubusercontent.com/91442807/236639672-44d9eaf9-338b-498b-be9e-6e44af022199.png" />
</p>

Ta thấy được của `Poppy` là cao nhất.

Kiểm tra số lượt bầu tại từng thời điểm của mỗi địa chỉ ip ở từng thành viên thì thấy của `Poppy` cao bất thường:

<p align="center">
   <img width="400" height="400" src="https://user-images.githubusercontent.com/91442807/236640514-0f711cc1-8154-40cc-b12b-361137688cf4.png" />
</p>

- Ta sẽ lọc những phiếu bầu không hợp lệ và chỉ ra dùng `series_decompose_anomalies` (những con số bất thường sẽ hiện thì là số 1)

<p align="center">
   <img width="400" height="400" src="https://user-images.githubusercontent.com/91442807/236640129-e2b8befb-ee25-4bba-a1d7-71476fcbaac6.png" />
</p>

Kết quả:

<p align="center">
   <img width="400" height="400" src="https://user-images.githubusercontent.com/91442807/236641572-e7b6dd4d-2b31-451b-8214-efdd19c78165.png" />
</p>
