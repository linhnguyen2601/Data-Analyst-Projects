# Vietnam Surveilance and Security Market 2020 Analysis | Excel & Power Query

![image](https://github.com/user-attachments/assets/cd72fc0c-dd95-40a6-9774-3cb15272f146)

## 1. Overview

### 1.1 Business Requirement

Tập trung vào camera an ninh, camera giám sát, camera IP, 

### 1.2 Dataset introduction

The dataset shows import data of security market in the first half of 2020.

Tổng số dòng: 

Các cột:

Ngày
Mã Cty NK
Mã hang 	
Tên hang
DVT
Lượng
Trị giá
Đơn giá
Thị trường xuất khẩu
Cửa khẩu
DKGH (Điều kiện giao hàng)
Mã PTTT
Mục đích sử dụng
Tên cty xuất khẩu

## 2. Data cleaning

### 2.1 Check null, dupplicate

### 2.2 Filtering

Thực hiện lọc trên các cột:

| Ngay | Ma Cty NX | Cong ty NK | Ma hang| Ten hang| DVT | Luong | Tri gia(USD)| Thi truong xuat khau| Cua khau| DKGD | Ma PTTT | Muc dich su dung| Ten cong ty XK|
| --- | --- | --- | --- | --- |--- |  --- | --- | --- |   --- |   --- |   --- | --- | --- | 
| | | x| x| x| x| x | |||||x||

- Công ty nhập khẩu:

Loại bỏ cá nhân và các văn phòng đại diện

- Mã hàng: Bỏ chọn các mã 85258031 & 85258051

	85258031: Mã HS camera ghi hình ảnh cho phát thanh

	85258039: Mã HS camera ghi hình ảnh loại khác

	85258040: Mã HS camera truyền hình

	85258051: Mã HS camera kỹ thuật số DSLR

	85258059: Mã HS camera kỹ thuật số loại khác\


Link tham khảo: https://projectshipping.vn/nhap-khau-camera-thiet-bi-giam-sat-an-ninh/

- Mục đích sử dung:
  Filter các mục đích sử dụng sau:

| STT | Loại | Miêu tả | Loại khỏi dataset|
| --- | --- |  --- |   --- |  
| 1 | Chuyển tiêu thụ nội địa khác |Chủ yếu là Bộ phận chụp hình của ĐTDĐ và Camera truyền hình| Có |
| 2 | Hàng gửi kho ngoại quan ||Không|
| 3 | Hàng nhập khẩu khác ||Không|
| 4 | Nhập hàng xuất khẩu bị trả lại ||Có|
| 5 | Nhập kinh doanh của doanh nghiệp đầu tư ||Không|
| 6 | Nhập kinh doanh sản xuất ||Không|
| 7 | Nhập kinh doanh tiêu dùng ||Không|
| 8 | Nhập linh kiện ô tô tham gia Chương trình ưu đãi thuế NK ||Có|
| 9 | Nhập nguyên liệu của doanh nghiệp chế xuất từ nước ngoài ||Có|
| 10 | Nhập nguyên liệu của doanh nghiệp chế xuất từ nội địa ||Có|
| 11 | Nhập nguyên liệu sản xuất xuất khẩu ||Có|
| 12 | Nhập nguyên liệu để gia công cho thương nhân nước ngoài ||Có|
| 13 | Nhập tạo tài sản cố định của doanh nghiệp chế xuất ||Không|
| 14 | Tái nhập hàng đã tạm xuất ||Có|
| 15 | Tạm nhập máy móc, thiết bị phục vụ thực hiện các dự án có thời hạn ||Có|

- Đơn vị tính:
  
![image](https://github.com/user-attachments/assets/9c97723c-b233-44fc-8887-d079c9efd13a)

- Lượng:

Loại bỏ các đơn hàng có lượng nhập khẩu < 10

- Tên hàng:
  DUPLICATE COLUMN & TRANSFORM COLUMN
  
Filter các hàng hóa có từ khóa: ô tô, điện thoại di động, máy tính bảng, máy tính, lenovo, ĐTDĐ, robot, máy ảnh, máy chụp hình, máy quay phim, xe hơi,
xe máy, ôtô, máy ảnh, 

- Tạo cột đơn giá trung bình để loại bỏ các đơn hàng có đơn giá quá thấp => dễ nhầm lẫn sang các loại linh kiện:

Loại bỏ các đơn giá trung bình < $2

