# Bai_kiem_tra_so2
## Phần mở đầu:
| Thông tin |    Nội Dung     |
|-----------|-----------------|
|Họ và tên  | Hoàng Nhất Long |
|MSSV       | K235480106046   |
|Lớp        | K59KMT.K01      |
|Đề tài     | Quản lý nhà phân phối công ty|
|Tên database | QuanLyNhaPhanPhoi_K235480106046 |

  * Cách làm:
  1. Thiết kế và khởi tạo cấu trúc dữ liệu
  2. Xây dựng hàm và vận dụng xây dựng hệ thống
  3. Xây dựng Store Procedure
  4. Trigger và Xử lý logic nghiệp vụ
  5. Cursor và xử lý nghiệp vụ

## Giới thiệu đề tài
  Xây dựng hệ thống quản lý nhà phân phối công ty, gồm các bảng NhaPhanPhoi (Nhà phân phối), SanPham (sản phẩm), DonHang (Đơn hàng) và ChiTietDonHang (Chi tiết đơn hàng). Trong mỗi bảng sẽ có khóa chính và khóa ngoại để các bảng có thể liên kết với nhau.
  
## Phần 1: Khởi tạo bảng
  - Chủ đề quản lý: Hệ thống quản lý nhà phân phối công ty
+ Đăng nhập vào hệ thống và tạo mới database bằng GUI
+ Tên database: QuanLyNhaPhanPhoi_K235480106046
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/d49b71ee-e68d-468c-bcc1-02baaeca17e9" />
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/44b9b2cd-c9bb-49df-bc13-aaa4ae575df2" />

  - Tạo bảng:
    + NhaPhanPhoi: gồm các trường: MaNPP (PK), TenNPP (không để trống), MaSoThue (không được trùng), Diachi, Email, SDT, NgayHopTac, TrangThai (ngừng hợp tác/đang hợp tác/đang xem xét)
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/8da5ccb2-97af-420d-a5c3-c0f4e62b2936" />
<br>
    + SanPham: Gồm các trường: MaSP (PK), MaNPP (FK), TenSP (Không để trống), DonGia (giá cung cấp), DonVi, SoLuong (số lượng cung cấp), NgayNhap, TrangThai (còn nhập/tạm ngừng nhập/đang xem xét)
 <img width="959" height="538" alt="image" src="https://github.com/user-attachments/assets/7ae4a111-51e0-4199-8e2b-d4151f73a60d" />
 <br>
    + DonHang: Gồm các trường: MaDH (PK), MaNPP (FK), NgayDat, TongTien, TrangThai (Đã thanh toán/Chờ xử lý/Đã hủy)
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/20c0352d-ac9d-40f3-9887-76625aea1146" />
<br>
    + ChiTietDonHang: Gồm các trường: MaCT (PK), MaDH (FK), MaSP (FK), SoLuong (số lượng mua), DonGia (giá mua)
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/7d19137b-948c-4b07-82fb-5bb60d20b91b" />

  - Nhập một vài thông tin vào các bảng:
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/160cd8a9-f17d-49c6-8336-65c76f22abbf" />

---

## Phần 2: Xây dựng Function
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
<br>

- Có 3 loại hàm chính:
  + Scalar Function: dùng khi cần tính toán đơn giản, hàm sẽ trả về một giá trị duy nhất <br>
  + Inline table-valued function: Dùng khi cần trả về 1 bảng dữ liệu hay một hàng đơn giản khi muốn lọc dữ liệu <br>
  + Multi-statement table-valued function: Dùng khi để lấy dữ liệu ra một bảng nhưng logic quá rắc rối và phức tạp <br>
<br>
- Tuy có nhiều hàm riêng nhưng vẫn không thể bao quát được tất cả công việc của hệ thóng. Việc tự viết hàm có thể đơn giản hóa việc truy vấn và chuẩn hóa dữ liệu, ngoài ra còn thể hiện sự tính toán logic trong từ công việc.
<br>
- Viết scalar function: 
  Hiện tại trong bảng DonHang có một trường TongTien đang cần tự động tính dựa vào trường SoLuong và DonGia của bảng ChiTietDonHang. Em sẽ viết một hàm function để tính TongTien và cập nhập vào trường TongTien. Khi đã có hàm function, em khai thác hàm bằng cách thực hiện update vào trường dữ liệu TongTien.
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/21edcd7b-6bf0-4abd-a90c-9034e2591b8f" />
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/41586b75-3146-4398-bee8-40bb2145cbe7" />
  *Kiểm tra kết quả:
  <img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/52996ab3-2a90-4049-bebc-b1889203113e" />
<br>
- Viết Inline Table-valued Function: Viết hàm trả về danh sách các nhà phân phối đang hợp tác và đang xem xét từ bảng NhaPhanPhoi. Khi đã có hàm, em khai thác bằng SELECT và truyền giá trị vào hàm.
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/ce874458-19d0-44b2-a56f-2d3a1d7526f1" />
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/1615a3dd-a61f-4806-a3da-d33ebfa89211" />
  *Kiểm tra kết quả:
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/01e4698c-9266-40b6-b9c5-86e90ecf5ad2" />

<br>
- Viết Multi-statement Table-valued Functions: Viết hàm phân loại xếp hạng nhà phân phối theo giá trị TongTien và đặt nhà cung cấp VIP theo TongTien > 1 tỷ. Để thực hiện sắp xếp, em sẽ dùng hàm rownumber() và cách sắp xếp giảm dần desc, dùng left join để có thể lấy được tất cả nhà phân phối trong bảng, dùng group by để gom nhóm các nhà phân phối (nếu có nhiều đơn hàng). Cuối cùng sử dụng select và order by để khai thác hàm đã viết:
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/20b80811-0cb9-40d1-b352-055e4169830c" />
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/0255490f-5483-4d2c-9ac5-cd9475a6e925" />

  *Kết quả thực hiện:
  <img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/6da68a07-8491-4c04-a937-99407093ff57" />

---
## Phần 3: Xây dựng Store Procedure
- Trong SQL Server có hỗ trợ rất nhiều Systerm Store Procedure có sẵn. Một vài loại không trả về dữ liệu, có loại trẩ về dữ liệu thông qua tham số output và có loại trả về dữ liệu của lệnh select bên trong sp đó. Em có thể tìm thấy danh sách trong phần Programmability -> Stored procedures -> System Stored Procedures
- Một vài System sp em tìm hiểu được:
  + sys.sp_columns: Liệt kê thông tin tất cả các cột trong một bảng
  + sys.sp_addlogin/sys.sp_droplogin: Thêm hoặc xóa một tài khoản đăng nhập vào sql server
  + sys.sp_password: thay đổi mật khẩu cho một tài khoản
<br>
- Viết một Store Procedure đơn giản để thực hiện lệnh Insert haocjw Update dữ liệu: Dựa vào trường TongTien của bảng DonHang để xếp hạng các nhà phân phối từ cao xuống thấp, đồng thời thêm một trường rank để xếp loại 'VIP' nếu nhà phân phối đó có TongTien đơn hàng > 1 tỷ. Đầu tiên cần kiểm tra xem đã tồn tại cột rank chưa, nếu chưa thì thêm trường rank. Sau đó sử dụng một bảng tạm thời để cập nhập rank dựa trên tính toán và update dữ liệu. Cuối cùng hiển thị từ cao xuống thấp để kiểm tra. Sử dụng EXEC để chạy
  *Thêm cột Rank vào bảng:
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/94dcc1ab-083a-403d-bdb6-e115ad08e55f" />
  *Viết SP:
  <img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/e341378a-55ae-49e2-bf2a-373638d868a5" />
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/ea2c11e6-7e4e-4b58-ac48-9626505a4184" />
  *Kết quả thực hiện:
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/1d91ff54-d409-44a3-96aa-fb96ead7d04d" />

<br>
- Viết một Store Procedure có sử dụng tham số output để trả về một giá trị tính toán: Tính toán số lượng chênh lệch giữa lượng hàng có thể cung cấp (SoLuong của bảng SanPham) và lượng hàng đã nhập vào (SoLuong của bảng ChiTietDonHang). Đầu tiên cần khai báo một vài biến tham số, sau đó tính tổng số lượng được đặt và tính toán sự chênh lệnh. Sau khi tạo logic kiểm tra trạng thái cảu sản phẩm, thự thi và hiển thị kết quả:
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/ac901c1a-8407-4806-a517-6dbc626fd9ab" />
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/59baaa33-244a-4969-ab8f-f851cc47b657" />
  *Kết quả thực hiện:
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/750744cf-4770-40a7-91e8-6a0ec1606338" />
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/74675eaf-dcce-40a2-9a2d-1e521b157f4c" />
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/aed4aa6b-04c8-4888-b8e9-11d80fd5a46f" />

<br>
- Viết 1 Store Procedure trả về một tập kết quả từ lệnh select sau khi đã join nhiều bảng: Thực hiện kết nối 3 bảng DonHang, NhaPhanPhoi và ChiTietDonHang để lấy ra báo cáo doanh thu trong một khoảng thời gian.
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/21545c68-70cc-4755-ad8f-7cb3f144e682" />
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/1102fb0d-4c28-413e-b0f0-782ee6257f9f" />
  *Kết quả thực hiện:
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/26195cb5-2a99-439b-b7aa-4d39fda8b725" />

---
## Phần 4: Trigger và xửu lý logic nghiệp vụ
- Viết một trigger tự động tính lại TongTien ở bảng HoaDon khi thay đổi dữ liệu SoLuong và DonGia ở bảng ChiTietDonHang. Tạo một bảng tạm để chứa hóa đơn bị thay đổi, sau đó cập nhập lại cột TongTien. Cuối cùng là thêm dữ liệu và kiểm tra kết quả.
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/d2bdf46d-51c3-40de-be7a-883b8ec529b1" />
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/f738e12f-18e6-46e7-8393-227dfd676370" />
*Trigger hoạt động
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/6d78fb2d-ee0c-4cfd-88b0-0b242e15c48b" />

*Chèn thêm dữ liệu vào bảng ChiTietDonHang và kiểm tra lại kết quả TongTien:
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/f665fe0f-6d3b-43f1-9dc7-1aac5735c8de" />
<br>
<br>
- Kiểm tra Trigger vòng lặp và quan sát hiện tượng đệ quy:
  + Tạo Trigger ở bảng A (bảng ChiTietDonHang), khi insert vào bảng sẽ cập nhập vào nagr B (DonHang):
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/2f7deb58-7c51-421e-b50c-e9d4e135b9f8" />
<br>
  + tạo trigger ở bảng B cập nhập dữ liệu sang bảng A:
<img width="959" height="538" alt="image" src="https://github.com/user-attachments/assets/875b5a0b-2d64-476e-ad54-450804d2d69a" />
<br>
  + Insert dữ liệu vào bảng B
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/89bb6536-1612-4493-b1e5-dd67181a5373" />
<br>
=> Thông báo hệ thống: <img width="359" height="28" alt="image" src="https://github.com/user-attachments/assets/5386ad06-f568-4599-943f-506d507309ff" />
 - Mã lỗi:<br>
+ msg217, level 16: Đây là lỗi mức độ trung bình đã bị hệ thống cưỡng bức dừng lại. <br>
+ maximum ... (limit 32): Xảy ra vòng lặp vô hạn khi 2 trigger gọi nhau, nhưng hệ thống chỉ giới hạn 32 lần lặp, khi quá 32 lần sẽ tự ngắt <br>
=> Nhận xét: Đây là lỗi đệ quy gián tiếp xảy ra do thiết kế các trigger phụ thuộc nhua theo vòng tròn, đó là một sai lầm về kiến trúc. Ngoài ra dựa trên logic khi thiết kế hệ thống, dữ liệu từ bảng A không đủ để có thể thay đổi bảng B, Dữ liệu chỉ cho phép đi từ A đến B việc đi ngược lại đã làm xung đột dữ liệu <br>
=> Kết luận: Trigger là con dao 2 lưỡi, nếu không thể kiểm soát có thể gây ra lỗi hệ thống nếu không nắm rõ.


## Phần 5: Cursor và duyệt dữ liệu
   








  

  


