# Bai_kiem_tra_so2
Phần mở đầu:
  - Họ và tên: Hoàng Nhất Long
  - MSSV: K235480106046
  - Lớp: K59KMT.K01
  - Đề tài: Quản lý nhà phân phối công ty
  * Cách làm:
  1. Thiết kế và khởi tạo cấu trúc dữ liệu
  2. Xây dựng hàm và vận dụng xây dựng hệ thống
  3. Xây dựng Store Procedure
  4. Trigger và Xử lý logic nghiệp vụ
  5. Cursor và xử lý nghiệp vụ

Phần 1: Khởi tạo bảng
  - Chủ đề quản lý: Hệ thống quản lý nhà phân phối công ty
+ Đăng nhập vào hệ thống và tạo mới database bằng GUI
+ Tên database: QuanLyNhaPhanPhoi_K235480106046
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/d49b71ee-e68d-468c-bcc1-02baaeca17e9" />
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/44b9b2cd-c9bb-49df-bc13-aaa4ae575df2" />

  - Tạo bảng:
    + NhaPhanPhoi: gồm các trường: MaNPP (PK), TenNPP (không để trống), MaSoThue (không được trùng), Diachi, Email, SDT, NgayHopTac, TrangThai (ngừng hợp tác/đang hợp tác/đang xem xét)
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/8da5ccb2-97af-420d-a5c3-c0f4e62b2936" />
    + SanPham: Gồm các trường: MaSP (PK), MaNPP (FK), TenSP (Không để trống), DonGia (giá cung cấp), DonVi, SoLuong (số lượng cung cấp), NgayNhap, TrangThai (còn nhập/tạm ngừng nhập/đang xem xét)
 <img width="959" height="538" alt="image" src="https://github.com/user-attachments/assets/7ae4a111-51e0-4199-8e2b-d4151f73a60d" />
    + DonHang: Gồm các trường: MaDH (PK), MaNPP (FK), NgayDat, TongTien, TrangThai (Đã thanh toán/Chờ xử lý/Đã hủy)
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/20c0352d-ac9d-40f3-9887-76625aea1146" />
    + ChiTietDonHang: Gồm các trường: MaCT (PK), MaDH (FK), MaSP (FK), SoLuong (số lượng mua), DonGia (giá mua)
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/7d19137b-948c-4b07-82fb-5bb60d20b91b" />

  - Nhập một vài thông tin vào các bảng:
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/160cd8a9-f17d-49c6-8336-65c76f22abbf" />

---


Phần 2: Xây dựng Function
- Trong SQL Server có nhiều loại hàm function build_in như:
  + Aggregate Functions
  + Configuration Functions
  + Cursor Functions
  + Date and Time Functions
  + Hierarchy Id Functions
  + Mathematical Functions
  + Metadata Functions
  + Other Functions
  + Rowset Functions
  + Security Functions
  + String Functions
  + System Statistical Functions
  + Text and Image Functions
  + Vector Functions
- Một vài system functions build_in em tìm hiểu được:
  + Len(): nằm trong String Functions, trả về kết quả là độ dài của một chuỗi string
  + Upper()/Lower: Nằm trong String Functions, chuyển về dạng chữ hoa/ chữ thường
  + Replace(): Thay thế ký tự này bằng ký tự khác
  + ASCII(): trả về mã số của ký tự
  + Char(): Đưa vào một con số sẽ trả về ký tự tương ứng trong bảng mã ASCII
  + Space(): Trả về một chuỗi gồn một số khoảng trắng nhất định
  + Getdate(): nằm trong Date and time functions: Lấy ngày giờ hiện tại của hệ thống
  + Dateadd(): Cộng thêm ngày/tháng/năm vào một mốc thời gian
  + Day(), Month(), Day(): Trả về giá trị ngày, tháng, năm. Dùng để tách ngày, tháng, năm của một mốc thời gian
  + Datename(): Trả về mội chuỗi ký tự đại diện cho một phần cụ thể của ngày tháng
  + Sum()/Avg()/: Nằm trong Aggregate functions, dùng để tính tổng/tính trung bình cộng
  + Count(): Đếm số lượng dòng
  + Max()/Min(): Tìm giá trị lớn nhất, nhỏ nhất
  + Abs(): Nằm trong mathematical Functions, Lấy giá trị tuyệt đối của một số
  + Pi(): trả về số PI
  + Power(): Tính lũy thừa của một số
  + Sqrt(): Tính căn bậc hai của một số


- Mục đích của việc tự viết hàm là để tạo ra công cụ tử giải quyết công việc, ngoài ra còn nhằm có thể tái sử dụng và có tính đóng gói. Thay vì phải viết đi viết lại một công thức phức tạp hoặc một logic định dạng khác nhau, ta chỉ cần gọi lại hàm đã viết giúp code sạch hơn và dễ dàng sửa lỗi.
- Có 3 loại hàm chính:
  + Scalar Function: dùng khi cần tính toán đơn giản, hàm sẽ trả về một giá trị duy nhất
  + Inline table-valued function: Dùng khi cần trả về 1 bảng dữ liệu hay một hàng đơn giản khi muốn lọc dữ liệu
  + Multi-statement table-valued function: Dùng khi để lấy dữ liệu ra một bảng nhưng logic quá rắc rối và phức tạp
- Tuy có nhiều hàm riêng nhưng vẫn không thể bao quát được tất cả công việc của hệ thóng. Việc tự viết hàm có thể đơn giản hóa việc truy vấn và chuẩn hóa dữ liệu, ngoài ra còn thể hiện sự tính toán logic trong từ công việc.
- Viết scalar function: 
  Hiện tại trong bảng DonHang có một trường TongTien đang cần tự động tính dựa vào trường SoLuong và DonGia của bảng ChiTietDonHang. Em sẽ viết một hàm function để tính TongTien và cập nhập vào trường TongTien. Khi đã có hàm function, em khai thác hàm bằng cách thực hiện update vào trường dữ liệu TongTien.
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/21edcd7b-6bf0-4abd-a90c-9034e2591b8f" />
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/41586b75-3146-4398-bee8-40bb2145cbe7" />
  *Kiểm tra kết quả:
  <img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/52996ab3-2a90-4049-bebc-b1889203113e" />

- Viết Inline Table-valued Function: Viết hàm trả về danh sách các nhà phân phối đang hợp tác và đang xem xét từ bảng NhaPhanPhoi. Khi đã có hàm, em khai thác bằng SELECT và truyền giá trị vào hàm.
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/ce874458-19d0-44b2-a56f-2d3a1d7526f1" />
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/1615a3dd-a61f-4806-a3da-d33ebfa89211" />
  *Kiểm tra kết quả:
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/01e4698c-9266-40b6-b9c5-86e90ecf5ad2" />


- Viết Multi-statement Table-valued Functions: Viết hàm phân loại xếp hạng nhà phân phối theo giá trị TongTien và đặt nhà cung cấp VIP theo TongTien > 1 tỷ. Để thực hiện sắp xếp, em sẽ dùng hàm rownumber() và cách sắp xếp giảm dần desc, dùng left join để có thể lấy được tất cả nhà phân phối trong bảng, dùng group by để gom nhóm các nhà phân phối (nếu có nhiều đơn hàng). Cuối cùng sử dụng select và order by để khai thác hàm đã viết:
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/20b80811-0cb9-40d1-b352-055e4169830c" />
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/0255490f-5483-4d2c-9ac5-cd9475a6e925" />

  *Kết quả thực hiện:
  <img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/6da68a07-8491-4c04-a937-99407093ff57" />

---
Phần 3: Xây dựng Store Procedure



  

  


