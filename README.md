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

 
 


  


