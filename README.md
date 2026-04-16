![image alt](https://github.com/lykienhuy/Data_project_aws/blob/50568ad1d431409665077931e3240bda762d2569/Architect.png)

# 🚀 Phân tích sản phẩm bán chạy nhất bằng quy trình ELT

## 📌 Tổng quan

Project này xây dựng một pipeline **ELT (Extract - Load - Transform)** trên AWS nhằm xử lý dữ liệu thô và phục vụ phân tích.

Hệ thống cho phép tự động ingest dữ liệu, load vào data warehouse, transform và trực quan hóa dữ liệu phục vụ **business insight**.

---

## 🏗️ Kiến trúc hệ thống

- **Amazon S3**: Lưu trữ raw data do user upload  
- **AWS Lambda**: Tự động trigger khi có dữ liệu mới  
- **Amazon Redshift**: Data warehouse để lưu trữ và transform dữ liệu  
- **Amazon QuickSight**: Công cụ visualize dữ liệu  
- **VPC + Private Subnet**: Tăng tính bảo mật cho hệ thống  

---

## 🔄 Luồng xử lý dữ liệu

### 1. User upload raw data lên S3
- Dữ liệu thô được đẩy vào S3 bucket

### 2. Lambda được trigger
- S3 event notification kích hoạt Lambda  
- Lambda đóng vai trò điều phối (**không xử lý dữ liệu**)  

### 3. Lambda trigger Stored Procedure trong Redshift
- Lambda gọi 2 stored procedure:
  - `copy_from_s3`
  - `transform`

### 4. Load dữ liệu (EL) và Transform (T)
- Redshift thực thi `copy_from_s3`  
  - Sử dụng lệnh `COPY` để load dữ liệu từ S3 vào bảng staging  

- Redshift thực thi `transform`  
  - Xử lý, làm sạch và tổng hợp dữ liệu  
  - Chuẩn bị dữ liệu phục vụ phân tích  

### 5. Visualization
- QuickSight kết nối với Redshift thông qua VPC connection
- Hiển thị các dashboard như:
- Sản phẩm bán chạy nhất  

---

## 🎯 Kết quả đạt được

- Tự động hóa pipeline dữ liệu end-to-end  
- Áp dụng đúng mô hình ELT 
- Dữ liệu được xử lý nhanh và sẵn sàng cho BI  
- Hỗ trợ phân tích và ra quyết định kinh doanh  

---

## Công nghệ sử dụng

- AWS S3  
- AWS Lambda  
- Amazon Redshift  
- Amazon QuickSight  
- VPC, Private Subnet  

---
