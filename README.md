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

  - Tạo 4 bảng: Nhà phân phối, Sản phẩm, Đơn hàng và chi tiết đơn hàng
    + Bảng NhaPhanPhoi: gồm các trường: MaNPP(PK), TenNPP, DiaChi, SDT, Email, NgayHopTac, TrangThai (ngừng hợp tác/đang hợp tác/đang xem xét)
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/3dd3de49-56dd-4aa2-ab99-f47d8a72f128" />
    + Bảng SanPham: gồm các trường: MaSP(PK), TenSP, Gia, SoLuong, DonVi, NgayNhap, DonViCungCap, TrangThai (còn nhu cầu/hết nhu cầu)
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/6483c727-0b43-4967-be01-9d1f5b37b5a9" />
    + Bảng DonHang: gồm các trường: MaDon(PK), MaNPP(FK) (của bảng NhaPhanPhoi), NgayDat, TongTien, TrangThai (đã bàn giao/đang xử lý/đã hủy)
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/15208c65-1dcc-4494-9b22-d6cc38eefa34" />
    + Bảng ChiTietDonHang: gồm các trường MaDon(FK), MaSP(FK), SoLuong, DonGia, ThanhTien. Trong đó trường SoLuong và DonGia cài not null để ngăn tình trạng trường ThanhTien nhận giá trị null khi thiếu 1 trong 2 giá trị tính
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/ca2f18cd-469b-4e81-a729-969d51e31937" />


Phần 2: Xây dựng hàm Function
 


  


