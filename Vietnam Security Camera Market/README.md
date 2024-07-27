# Vietnam Surveilance and Security Market 2020| Excel & Power Query & Pivot Table

Note: The data has been processed to avoid disclosing precise information from the company's actual data.

_Lưu ý: số liệu đã được xử lý để tránh đưa thông tin chính xác từ dữ liệu của công ty lên_

![image](https://github.com/user-attachments/assets/cd72fc0c-dd95-40a6-9774-3cb15272f146)

## 1. Overview

### 1.1 Business Requirement

The goal of analyzing this dataset is to examine import data to provide detailed insights that support the sales department in researching the security camera market in Vietnam, as well as developing a pricing strategy for the company's upcoming product launch.

Report Outputs:
Total Number of Cameras Imported: Determine the total number of officially imported (through customs) cameras in Vietnam during the first six months of 2020.
Import Trends: Identify import trends over time.
Major Exporting Brands: Identify which brands are exporting the largest quantities to Vietnam, the quantities involved, and their values.
Country of Origin: Determine the countries of origin for these brands.
Export Channels: Identify through which companies these brands are exporting to Vietnam (direct distribution or through agents).
Import Trends of Dealers: Analyze the import trends of camera dealers.
Dataset Fields:
The dataset includes the following fields: date, importing company, item code, item name, quantity, unit of measure, value, purpose of use, and exporting company.

Mục tiêu của việc phân tích dataset này là phân tích dữ liệu thị trường để cung cấp thông tin chi tiết hỗ trợ phòng kinh doanh trong việc nghiên cứu thị trường camera an ninh, camera giám sát tại Việt Nam cũng như xây dựng chiến lược giá cho dòng sản phẩm đang chuẩn bị tung ra thị trường của công ty. 

Đầu ra báo cáo cần làm rõ:

- Tổng số lượng camera nhập khẩu vào Việt Nam trong 6 tháng đầu năm 2020 là bao nhiêu?
- Xác định xu hướng nhập khẩu theo thời gian.
- Những hãng nào đang xuất khẩu vào Việt Nam với số lượng là bao nhiêu, giá trị như thế nào?
- Nguồn gốc xuất xứ những hãng đó từ nước nào?
- Những hãng đó đang xuất khẩu vào Việt Nam thông qua công ty xuất khẩu nào (Chính hãng phân phối tại Việt Nam hay thông qua đại lý?)
- Các đại lý nhập khẩu camera có xu hướng nhập khẩu như thế nào?
- Camera nhập khẩu vào Việt Nam chủ yếu ở phân khúc giá nào? Đặc điểm của những phân khúc giá này là gì?
- Loại camera nào đang được nhập khẩu nhiều nhất vào Việt Nam?

Dataset bao gồm các trường thông tin: ngày, công ty nhập khẩu, mã hàng, tên hàng, số lượng, đơn vị tính, giá trị, mục đích sử dụng, và công ty xuất khẩu.

### 1.2 Dataset introduction

The dataset shows import data of security market in the first half of 2020.

Dataset này bao gồm số liệu về thị trường camera nhập khẩu của Việt Nam trong 6 tháng đầu năm 2020.

Columns/Các cột:

|STT | Tên cột | Miêu tả|
|---|---|---|
|1|Ngay|Ngày nhập khẩu|
|2|Ma Cty NX|Mã công ty nhập khẩu|
|3|Cong ty NK|Công ty nhập khẩu|
|4|Ma hang|Mã hàng|
|5|Ten hang|Tên hàng|
|6|ĐVT|Đơn vị tính|
|7|Luong|Lượng|
|8|Tri gia (USD)|Trị giá (USD)|
|9|Thi truong xuat khau|Thị trường xuất khẩu|
|10|Muc dich su dung| Mục đích sử dụng |
|11|Ten cong ty XK|Tên công ty xuất khẩu|

## 2. Data cleaning

### 2.1 Check null, duplicate

There are no null values.

There are 497 duplicate rows, accounting for approximately 3% of the dataset.

Không có giá trị null. 

Có 497 dòng bị duplicate, chiếm khoảng 3% dataset.

### 2.2 Filtering

Apply Filters on the Following Columns:

_Thực hiện lọc trên các cột:_

| Ngay | Ma Cty NX | Cong ty NK | Ma hang| Ten hang| DVT | Luong | Tri gia(USD)| Thi truong xuat khau| Muc dich su dung| Ten cong ty XK|
| --- | --- | --- | --- | --- |--- |  --- | --- | --- |   --- |   --- |  
| | | x| x| x| x| x | ||x||


- Công ty nhập khẩu:

Filter out individuals and organizations without tax codes, as well as representative offices, to focus on manufacturing, trading, and import companies.

Loại bỏ các cá nhân- tổ chức không có mã số thuế và các văn phòng đại diện với mục đích là tập trung vào các công ty sản xuất, thương mại và nhập khẩu

```
 Table.SelectRows(#"Removed Duplicates", each ([Cong ty Nhap khau] <> "Tổng Lãnh Sự Quán xxx" and [Cong ty Nhap khau] <> "VPĐD D-Link xxx" and [Cong ty Nhap khau] <> "Văn phòng đại diện xxx" and [Cong ty Nhap khau] <> "Văn phòng đại diện xxxx" and [Cong ty Nhap khau] <> "Văn phòng đại diện xxx"))
```

- Mã hàng: Filter out HS Code 85258031 & 85258051. Bỏ chọn các mã 85258031 & 85258051

	85258031: Mã HS camera ghi hình ảnh cho phát thanh

	85258039: Mã HS camera ghi hình ảnh loại khác

	85258040: Mã HS camera truyền hình

	85258051: Mã HS camera kỹ thuật số DSLR

	85258059: Mã HS camera kỹ thuật số loại khác\


Link tham khảo: https://projectshipping.vn/nhap-khau-camera-thiet-bi-giam-sat-an-ninh/


- Mục đích sử dung:

  Filter out the following purpose of use/ Filter các mục đích sử dụng sau:

| STT | Loại | Miêu tả | Loại khỏi dataset|
| --- | --- |  --- |   --- |  
| 1 | Chuyển tiêu thụ nội địa khác |Chủ yếu là Bộ phận chụp hình của ĐTDĐ và Camera truyền hình| Có |
| 2 | Hàng gửi kho ngoại quan ||Không|
| 3 | Hàng nhập khẩu khác ||Không|
| 4 | Nhập hàng xuất khẩu bị trả lại | Không xét đến các hàng xuất khẩu bị trả lại|Có|
| 5 | Nhập kinh doanh của doanh nghiệp đầu tư ||Không|
| 6 | Nhập kinh doanh sản xuất ||Không|
| 7 | Nhập kinh doanh tiêu dùng ||Không|
| 8 | Nhập linh kiện ô tô tham gia Chương trình ưu đãi thuế NK |Đối tượng đang xét đến không phải linh kiện ô tô|Có|
| 9 | Nhập nguyên liệu của doanh nghiệp chế xuất từ nước ngoài |Đối tượng đang xét đến không phải nguyên liệu sản xuất|Có|
| 10 | Nhập nguyên liệu của doanh nghiệp chế xuất từ nội địa |Đối tượng đang xét đến không phải nguyên liệu sản xuất|Có|
| 11 | Nhập nguyên liệu sản xuất xuất khẩu |Đối tượng đang xét đến không phải nguyên liệu sản xuất|Có|
| 12 | Nhập nguyên liệu để gia công cho thương nhân nước ngoài |Đối tượng đang xét đến không phải nguyên liệu sản xuất|Có|
| 13 | Nhập tạo tài sản cố định của doanh nghiệp chế xuất ||Không|
| 14 | Tái nhập hàng đã tạm xuất ||Có|
| 15 | Tạm nhập máy móc, thiết bị phục vụ thực hiện các dự án có thời hạn |Có|


- Đơn vị tính:
  
Filter out units of measure that do not align with the products being analyzed, as these units represent items outside the scope of the analysis./ Loại bỏ các đơn vị tính không phù hợp với đối tượng sản phẩm đang phân tích vì các đơn vị tính này thể hiện các mã hàng ngoài vùng phân tích

- Lượng:

Removed import orders with quantities less than 10 to exclude sample orders that do not serve commercial purposes./ Loại bỏ các đơn hàng có lượng nhập khẩu < 10 để loại bỏ các trường hợp nhập hàng mẫu không phục vụ mục đích thương mại.

- Tên hàng:

```
= Table.TransformColumns(#"Filtered Muc dich su dung",{{"Ten hang", Text.Lower, type text}})
```
  
Filter out các hàng hóa có từ khóa: ô tô, ôtô, điện thoại di động, đtdđ, camera lùi, máy tính, robot, máy ảnh, máy chụp hình, máy quay phim, xe hơi, xe máy,cụm camera, hành trình, máy quay, hội nghị, camera sau, phụ tùng, mã vạch, tuần tra, lùi, linh kiện, kiểm tra sản phẩm, lắp trong xe, lùi, kính hiển vi.

![image](https://github.com/user-attachments/assets/5e7b00e2-c158-4905-ab79-9aa603cecc23)

- Tạo cột đơn giá trung bình = Tri gia (USD)/ Luong (Trị giá/Lượng) 

Created a column for average unit price.
Filtered out orders with an average unit price lower than $2, as these may be mistaken for components or sample items, which are typically priced below $2.

Tạo cột đơn giá trung bình để loại bỏ các đơn hàng có đơn giá thấp hơn 2 vì dễ nhầm lẫn sang các loại linh kiện cũng như giá cho các hàng mẫu/thường là dưới $2

Dataset sau khi thực hiện lọc các giá trị không phù hợp so với dataset ban đầu:

Dataset ban đầu:

|Số dòng| Tổng số lượng | |Số dòng| Tổng số lượng || % số dòng| % số lượng
|---|---||---|---||---|---|
|16,088| 59,105,770|| 4,561 | 1,929,600|| 28.35%|3.26%

## 2. Data analysis

### 2.1 Data overview

Trong 6 tháng đầu năm 2020 có khoảng gần 2 triệu camera an ninh, camera giám sát được nhập khẩu vào Việt Nam thông qua... công ty nhập khẩu.


Phân bổ theo số lượng theo các quốc gia xuất khẩu camera vào Việt Nam

Trong tổng số gần 2 triệu camera được nhập khẩu vào Việt Nam trong 6 tháng đầu năm 2020, 

### 2.2 Phân bổ theo số lượng theo các hãng camera được xuất khẩu vào Việt Nam

The market, valued at roughly US$175 million in 2023, is dominated by Chinese giants Dahua and Hikvision who hold a staggering 90 per cent market share.

Để phân tích theo hãng camera: 
- Add conditional column: lọc theo tên hãng và tên công ty

<img width="683" alt="image" src="https://github.com/user-attachments/assets/9dbed37e-549b-4164-afde-84ffb4d125f8">


|Số dòng| Tổng số lượng |% trên tổng dataset|
|---|---|---|
|Số dòng có thể nhận diện được tên hãng camera| 4,013 |87.99%|
|Số lượng| 1,891,024|98.00%|


_Note: do số liệu này là số liệu không được public nên những báo cáo ở trên đây chỉ có thể cung cấp số liệu chung chung dạng % và không cung cấp số liệu chính xác_
