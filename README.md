# RangDongTest
# Quy trình xử lý dữ liệu

## I. Thông tin về các trường dữ liệu
Dưới đây là mô tả các trường dữ liệu chính:

- **`Date`**: Ngày ghi nhận doanh thu và kế hoạch (theo tháng/quý/năm), thường bắt đầu từ ngày 1 mỗi tháng.
- **`Department`**: Các phòng ban. Chỉ các phòng `BH1`, `BH2`, `PXK` có dữ liệu doanh thu. Các phòng ban khác chưa được xác định rõ.
- **`Ma_Nhom_NSP1` – `NSP1_Code` – `NSP1_Name`**:  
  - Ba cột này có quan hệ 1-1.  
  - Ví dụ: `L01` tương ứng với `A001` và `1 - SP Công nghệ nền`.
- **`NSP2_Code` – `NSP2_Name`**:  
  - Hai cột này có quan hệ 1-1.  
  - Có quan hệ 1-n với các cột liên quan đến `NSP1`.  
  - Ví dụ: Với `NSP1_Code = A001`, các giá trị `NSP2_Name` có thể là:  
    - `Sản phẩm LED nền`  
    - `SP Khác`  
    - `Thiết bị điện`  
    - `Máng đèn`  
    - `Phích cao cấp`  
    - `Phích phổ thông`  
    - `Ruột phích`  
    - `Chao, choá`  
    - `Ballat đèn Huỳnh quang`
- **`Deliver`**: Doanh thu thực tế.  
- **`Deliver_Plan`**: Doanh thu dự kiến.  
- **`Created_At`**: Thời gian tạo bản ghi.

---

## II. Quy trình xử lý dữ liệu
Dưới đây là các bước xử lý dữ liệu bằng Python:

1. **Sửa định dạng tên tiếng Việt**:  
   - Khi đọc dataframe, sửa lỗi định dạng tiếng Việt cho hai cột `NSP1_Name` và `NSP2_Name`.

2. **Chuyển đổi kiểu dữ liệu**:  
   - Điều chỉnh các cột về kiểu dữ liệu phù hợp (ví dụ: `Date` sang datetime, `Deliver` và `Deliver_Plan` sang số).

3. **Loại bỏ cột không cần thiết**:  
   - Xóa cột `Created_At` khỏi dataframe.

4. **Tách dữ liệu thành 2 dataframe**:  
   - `deliver_df`: Chứa dữ liệu doanh thu thực tế (`Deliver`).  
   - `plan_df`: Chứa dữ liệu doanh thu dự kiến (`Deliver_Plan`).

5. **Xử lý giá trị bất thường**:  
   - Trong `deliver_df`: Xử lý các hàng có `Deliver < 0` hoặc giá trị `null`.  
   - Trong `plan_df`: Xử lý tương tự với `Deliver_Plan`.

---

## III. Xây dựng mô hình OLAP
- **Công nghệ sử dụng**: Power Query.  
- **Mục tiêu**: Tạo mô hình phân tích đa chiều để hỗ trợ báo cáo.

### Các bảng Dimensions
1. **`Dim_Time`**: Chứa thông tin thời gian (ngày, tháng, quý, năm).  
2. **`Dim_Department`**: Chứa danh sách các phòng ban.  
3. **`Dim_PlanType`**: Phân loại dữ liệu (thực tế hoặc kế hoạch).  
4. **`Dim_NSP`**:  
   - Chứa thông tin nhóm sản phẩm.  
   - Tạo cột mới `NSP_Code` bằng cách nối `NSP1_Code` và `NSP2_Code` (ví dụ: `A001 – B001`).

### Các bảng Fact
1. **`Fact_Deliver`**: Lưu dữ liệu doanh thu thực tế.  
2. **`Fact_DeliverPlan`**: Lưu dữ liệu doanh thu dự kiến.

![image](https://github.com/user-attachments/assets/be21d3bd-e69a-462a-a139-b6279537007e)
Mô hình OLAP

---

## IV. Tạo Dashboard
- **Công cụ**: Power BI.   
  ![image](https://github.com/user-attachments/assets/7e459cb4-3c0f-4d47-a43c-376608ffdb0c)
![image](https://github.com/user-attachments/assets/88a14d14-660d-450a-b112-785fa79cb36c)

- Link Dashboard: Đang cập nhật

