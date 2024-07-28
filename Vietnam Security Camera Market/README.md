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
  
Filter out các hàng hóa có từ khóa: ô tô, ôtô, điện thoại di động, đtdđ, camera lùi, máy tính, robot, máy ảnh, máy chụp hình, máy quay phim, xe hơi, xe máy,cụm camera, hành trình, máy quay, hội nghị, camera sau, phụ tùng, mã vạch, tuần tra, lùi, linh kiện, kiểm tra sản phẩm, lắp trong xe, lùi, kính hiển vi, camera trước

![image](https://github.com/user-attachments/assets/5e7b00e2-c158-4905-ab79-9aa603cecc23)

- Tạo cột đơn giá trung bình = Tri gia (USD)/ Luong (Trị giá/Lượng) 

Created a column for average unit price.
Filtered out orders with an average unit price lower than $2, as these may be mistaken for components or sample items, which are typically priced below $2.

Tạo cột đơn giá trung bình để loại bỏ các đơn hàng có đơn giá thấp hơn 2 vì dễ nhầm lẫn sang các loại linh kiện cũng như giá cho các hàng mẫu/thường là dưới $2

Dataset sau khi thực hiện lọc các giá trị không phù hợp so với dataset ban đầu:

Dataset ban đầu:

||Số dòng| Tổng số lượng |
|---|---|---|
|Dataset ban đầu|16,088| 59,105,770|
|Dataset sau khi lọc| 4,478 | 1,921,405|
|%| 27.83%|3.25%|

## 2. Data analysis

### 2.1 Data overview

Nearly 2 million security and surveillance cameras were imported into Vietnam. These imports were facilitated by over 400 manufacturing and trading companies.The total import value exceeded 50 million USD.

China: Dominated the market with over 96% of the import quantity and more than 74% of the import value.
Singapore: Contributed 1% of the import quantity and 10% of the import value.
South Korea: Accounted for 0.37% of the import quantity and 1% of the import value.

Trong 6 tháng đầu năm 2020 có khoảng gần 2 triệu camera an ninh, camera giám sát được nhập khẩu vào Việt Nam thông qua hơn 400 công ty sản xuất và thương mại. Tổng giá trị nhập khẩu là hơn 50 triệu USD.

Trong đó, Trung Quốc là quốc gia xuất khẩu lớn nhất vào Việt Nam, chiếm gần như tuyệt đối thị trường với hơn 96% lượng xuất khẩu và hơn 74% về giá trị. Theo sau là Singapore (1% về lượng và 10% về giá trị) và Hàn Quốc (0.37% về lượng và 1& về giá trị)

### 2.2 Phân bổ theo số lượng theo các hãng camera được xuất khẩu vào Việt Nam

Để phân tích theo hãng camera: 
- Add conditional column: lọc theo tên hãng và tên công ty

<img width="683" alt="image" src="https://github.com/user-attachments/assets/9dbed37e-549b-4164-afde-84ffb4d125f8">


|Số dòng| Tổng số lượng |% trên tổng dataset|
|---|---|---|
|Số dòng có thể nhận diện được tên hãng camera| 4,013 |87.99%|
|Số lượng| 1,902,xxx|99.00%|
|Trị giá (USD)| 44,695,xxx|90.30%|


There are nearly 60 camera brands imported into Vietnam. Among them, the primary market is dominated by Chinese brands, with Dahua and Hikvision being the two largest exporters to Vietnam (accounting for 86.37% in quantity and 75% in value), along with their subsidiary brands. Additionally, there are other smaller Chinese brands.


- Hikvision camera brands: Hikvision, Hilook, Ezviz

- Dahua camera brands: Dahua, Imou, Kbone, KBvision


Additionally, there are cameras from the following brands:

South Korea: Hanwha Techwin: Hanwha, Wisenet

Vietnamese cameras manufactured by Chinese companies: Huviron, Hiviz, FPT, Vantech

#

Có gần 60 hãng camera nhập khẩu vào Việt Nam. Trong đó, với 1 thị trường chủ yếu từ các hãng Trung Quốc, hai hãng camera xuất khẩu lớn nhất vào Việt Nam là Dahua và Hikvision (chiếm 86.37% về lượng và 75% về giá trị) và các hãng con của hai hãng này. Ngoài ra là các hãng nhỏ khác của Trung Quốc

Các hãng camera của Hivision: Hikvision, Hilook, Ezviz, 
Các hãng camera của Dahua: Dahua, Imou, Kbone, KBvision

Ngoài ra còn có các camera của các hãng từ:
Hàn Quốc: Hanwha Techwin: Hanwha, Wisenet

Camera Việt Nam gia công bới NSX TQ: Huviron, Hiviz, FPT, Vantech

|STT|Thương hiệu camera|Hãng camera|% lượng camera|% giá trị camera|
|---|---|---|---|---|
|1|Hikvision|Hikvision|23.xx%|24.xx%|
|2|Dahua|Dahua|21.xx%|14.xx%|
|3|Ezviz|Hivision|17.xx%|13.xx%|
|4|KBvision|Dahua|10.xx%|6.xx%|
|5|Imou|Dhua|8.xx%|6.xx%|
|6|Kbone|Dahua|4.xx%|3.xx%|

### 2.3 Phân bổ số lượng và giá trị camera theo nhà nhập khẩu

Các công ty nhập khẩu chỉ kinh doanh/phân phối các sản phẩm từ 1 hãng camera nhất định và 2-3 hiệu camera của hãng đó, tương ứng là 2-3 công ty xuất khẩu. 

Theo thống kê có hơn 400 công ty nhập khẩu, tuy nhiên chỉ tính riêng Top 10 nhà nhập khẩu tại Việt Nam 
 đã chiếm 80% lượng camera nhập khẩu vào VN và 57% về giá trị). Và top 10 nhà NK này cũng chỉ phân phối camera của hai hãng là Dahua và Hikvision.

|STT|Nhà nhập khẩu|Hãng camera|% lượng camera|% giá trị camera|
|---|---|---|---|---|
|1|CôNG TY Cổ PHầN CôNG NGHệ DSS VIệT NAM|Dahua (Dahua, Imou)|17.xx%|11.xx%|
|2|Công Ty Cổ Phần Nhà An Toàn|Hikvision (Hikvision, Ezviz)|15.xx%|13.xx%|
|3|Cty TNHH Thương Mại Kỹ Thuật Lê Hoàng|Hikvision (Hikvision, Ezviz)|10.xx%|7.xx%|
|4|CôNG TY CP CôNG NGHệ DSS MIềN NAM|Dahua (Dahua, Imou)|9.xx%|6.xx%|
|5|CôNG TY TNHH Kỹ THUậT KB SECURITY|Dahua (KBvision, Kbone)|7.xx%|4.xx%|
|6|Công Ty TNHH Thương Mại Kỹ Thuật Tin Học Anh Ngọc|Hikvision (Ezviz)|6.xx%|5.xx%|
|7|CôNG TY TNHH XUấT NHậP KHẩU ĐồNG VăN|Dahua (Dahua, Kbone, KBvision)|4.xx%|2.xx%|
|8|CôNG TY TNHH SảN XUấT & THươNG MạI LONG HòA| Dahua (Dahua, Kbone, KBvision)|3.xx%|1.xx%|
|9| Công Ty TNHH Đầu Tư Và Phát Triển Phương Việt| Hikvision|3.xx%|2.xx%|
|10| CôNG TY Cổ PHầN PHáT TRIểN GIA PHáT VIệT NAM| Hikvision|1.xx%|1.xx%|

### 2.4 Phân bổ số lượng và giá trị theo phân khúc giá

Giá camera nhập khẩu vào Việt Nam rất đa dạng, từ giá thấp nhất là $2/camera đến camera chuyên dụng giá cao nhất là $12,000/camera.

#### 2.4.1 Phân tích giá trung bình trên hai hãng camera Hikvision và Dahua:

|Hãng camera|Hiệu camera|Tỷ lệ phân bổ|Giá Trung bình|
|---|---|---|---|
|Dahua|Dahua|24.xx%|108.xx|
|Hikvision|Hivision|27.xx%|70.xx|
|Dahua|KBvision|11.xx%|36.xx|
|Hikvision|Ezviz|20.xx%|30.xx|
|Dahua|KBone|5.xx%|22.xx|
|Dahua|Imou|9.xx%|22.xx|
|Hikvision|Hilook||21.xx|

Từ bảng giá trung bình trên ta thấy hai hãng Dahua và Hivision có phân cấp giá rõ rệt cho các hiệu camera khác nhau, từ loại cao cấp đến phân khúc phổ thông.

Tuy nhiên trong khi các phân khúc giá thấp hơn của Dahua và Hikvision có sự cạnh tranh tương đối về giá (KBvision vs Ezviz, KBone vs Imou) thì giá trung bình của hai thương hiệu Dahua và Hikvision đang chênh lệch nhau tương đối lớn.

Vì vậy ta check giá camera lớn nhất của hai hãng camera này thì thấy:

- Các camera có giá nhập khẩu lớn nhất của Dahua bị tính thêm chi phí bản quyền phần mềm camera trong 1 số đơn hàng, trong khi các đơn hàng còn lại với mẫu camera tương tự thì không phải chịu chi phí bản quyền này. Vì vậy ta sẽ lấy giá trung bình camera của các model này mà không có chi phí bản quyền phần mềm.

- Camera có giá nhập khẩu lớn nhất của Hikvision là do đơn hàng này được nhập khẩu với giá bán lẻ, không phải giá nhập khẩu như đang tính ở đây nên chúng ta cũng thực hiện điều chỉnh về giá nhập đối với đơn hàng này.

Sau khi điều chỉnh giá, đơn giá TB của các thương hiệu camera như sau:

|Hãng camera|Hiệu camera|Tỷ lệ phân bổ|Giá Trung bình|
|---|---|---|---|
|Dahua|Dahua|24.xx%|94.xx|
|Hikvision|Hivision|27.xx%|68.xx|
|Dahua|KBvision|11.xx%|36.xx|
|Hikvision|Ezviz|20.xx%|30.xx|
|Dahua|KBone|5.xx%|22.xx|
|Dahua|Imou|9.xx%|22.xx|
|Hikvision|Hilook||21.xx|

Tuy số liệu đã hợp lý hơn nhưng cũng cần lưu ý rằng do cơ cấu nhập khẩu của các model của mỗi thương hiệu mà sẽ dẫn đến giá trung bình khác nhau. Vì vậy chúng ta sẽ đi sâu vào phân tích phân khúc giá của hai hãng camera Dahua và Hikvision:

|Hiệu camera|<20|20-35|35-50|50-95|>95|
|---|---|---|---|---|---|
|Dahua|81%|15.7%|2.2%|0.8%|0.4%|
|Hikvision|59.8%|23.2%|10%|4.6%|2.5%|
|KBvision|80.3%|17.3%|0.2%|1.6%|0.3%|
|Ezviz|79.3%|16.8%|3.7%|0.1%|0.2%|
|KBone|71.4%|28.6%|0|0|0|
|Imou|85.4%|14.6%|0|0|0|
|Hilook|77.1%|19.7%|3.3%|0|0|

Có thể thấy trong khi Dahua và Hikvision được định vị ở phân khúc giá cao hơn và có nhiều module giá cao thì các hãng khác như Kbone và Imou, Hilook- những dòng camera giá rẻ hầu như không có camera nào có giá nhập khẩu cao hơn $35/camera.

#### 2.4.2 Phân tích giá các hãng camera giá cao

![image](https://github.com/user-attachments/assets/157aa9f5-ec35-4e28-b8fc-5444b734f18d)


