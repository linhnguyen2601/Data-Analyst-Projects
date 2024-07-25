# Vietnam Surveilance and Security Market 2020 Analysis | Excel & Power Query & Pivot Table

![image](https://github.com/user-attachments/assets/cd72fc0c-dd95-40a6-9774-3cb15272f146)

## 1. Overview

### 1.1 Business Requirement

Mục tiêu của việc phân tích dataset này là phân tích dữ liệu nhập khẩu để cung cấp thông tin chi tiết hỗ trợ phòng kinh doanh trong việc nghiên cứu thị trường camera an ninh, camera giám sát tại Việt Nam cũng như xây dựng chiến lược giá cho dòng sản phẩm đang chuẩn bị tung ra thị trường của công ty. 

Đầu ra báo cáo cần làm rõ:

- Tổng số lượng camera nhập khẩu chính ngạch (qua hải quan) tại Việt Nam trong 6 tháng đầu năm 2020 là bao nhiêu?
- Xác định xu hướng nhập khẩu theo thời gian.
- Những hãng nào đang xuất khẩu vào Việt Nam với số lượng lớn nhất, là bao nhiêu, giá trị như thế nào?
- Nguồn gốc xuất xứ những hãng đó từ nước nào?
- Những hãng đó đang xuất khẩu vào Việt Nam thông qua công ty xuất khẩu nào (Chính hãng phân phối tại Việt Nam hay thông qua đại lý?)
- Các đại lý nhập khẩu camera có xu hướng nhập khẩu như thế nào?

Dataset bao gồm các trường thông tin: ngày, công ty nhập khẩu, mã hàng, tên hàng, số lượng, đơn vị tính, giá trị, mục đích sử dụng, và công ty xuất khẩu.

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

```
= Table.TransformColumns(#"Filtered Muc dich su dung",{{"Ten hang", Text.Lower, type text}})
```
  
Filter các hàng hóa có từ khóa: ô tô, ôtô, điện thoại di động, đtdđ, camera lùi, máy tính, robot, máy ảnh, máy chụp hình, máy quay phim, xe hơi,
xe máy,cụm camera, hành trình, máy quay, hội nghị, camera sau, phụ tùng, mã vạch, tuần tra, lùi, linh kiện, kiểm tra sản phẩm, lắp trong xe, lùi, kính hiển vi.

![image](https://github.com/user-attachments/assets/5e7b00e2-c158-4905-ab79-9aa603cecc23)

- Tạo cột đơn giá trung bình để loại bỏ các đơn hàng có đơn giá quá thấp => dễ nhầm lẫn sang các loại linh kiện:

Loại bỏ các đơn giá trung bình < $2

Dataset ban đầu:

|Số dòng| Tổng số lượng |
|---|---|
|16,088| 59,105,770|

Dataset sau khi thực hiện lọc:

|Số dòng| Tổng số lượng |
|---|---|
| 4,597 | 1,930,877|

## 2. Data analysis

### 2.1 Data overview

Trong 6 tháng đầu năm 2020 có khoảng gần 2 triệu camera an ninh, camera giám sát 
Phân bổ theo số lượng theo các quốc gia xuất khẩu camera vào Việt Nam

Trong tổng số gần 2 triệu camera được nhập khẩu vào Việt Nam trong 6 tháng đầu năm 2020, 

### 2.2 Phân bổ theo số lượng theo các hãng camera được xuất khẩu vào Việt Nam

Phân tích theo camera Brand
- Add conditional column: lọc theo tên hãng và tên công ty

<img width="683" alt="image" src="https://github.com/user-attachments/assets/9dbed37e-549b-4164-afde-84ffb4d125f8">


|Số dòng| Tổng số lượng |% trên tổng dataset|
|---|---|---|
|Số dòng có thể nhận diện được tên hãng camera| 4,010 |87.23%|
|Số lượng| 1,890,638|97.91%|


