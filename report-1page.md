# Report 1 page - Lab 6 AES-CBC Socket

## Thông tin nhóm

- Thành viên 1: Nguyễn Vân Đạt
- Thành viên 2: TODO_STUDENT

## Mục tiêu

Mục tiêu của bài lab là xây dựng cơ chế gửi/nhận dữ liệu qua socket theo mô hình Sender/Receiver. Dữ liệu được mã hóa bằng AES-CBC và áp dụng PKCS#7 padding để đảm bảo khối hợp lệ. Kênh trao đổi khóa được tách riêng với kênh dữ liệu và có tiêu đề độ dài rõ ràng. Hệ thống được kiểm thử bằng các ca hợp lệ và ca lỗi (sai khóa, sửa dữ liệu). Cuối cùng, nhóm phân tích điểm yếu bảo mật quan sát được trong quá trình triển khai.

## Phân công thực hiện

Thành viên 1 (Nguyễn Vân Đạt) phụ trách triển khai Sender, logic mã hóa AES-CBC/PKCS#7 và định dạng gói dữ liệu có length header. Thành viên 1 cũng tổng hợp log chạy mẫu và viết phần kết luận kỹ thuật. Thành viên 2: TODO_STUDENT. Cả nhóm cùng rà soát yêu cầu, chạy test tổng hợp và đối chiếu kết quả với mô tả đề bài.

## Cách làm

Sender đọc input, tạo IV ngẫu nhiên và mã hóa plaintext bằng AES-CBC, sau đó thêm PKCS#7 padding trước khi mã hóa. Khóa được gửi qua key channel riêng, còn dữ liệu (IV + ciphertext) đi qua data channel với tiêu đề độ dài cố định để Receiver đọc đúng số byte. Receiver đọc length header, nhận đủ payload, tách IV/ciphertext rồi giải mã và loại padding để khôi phục dữ liệu gốc. Quy trình xử lý lỗi được thêm để báo sai khóa hoặc dữ liệu bị sửa.

## Kết quả

Chạy mẫu cho thấy Receiver nhận đúng nội dung gốc, log hiển thị quá trình gửi khóa và dữ liệu theo đúng thứ tự kênh. Các test dương tính về padding và giao thức kênh khóa/kênh dữ liệu đều qua. Các test âm tính như sai khóa và sửa dữ liệu cho kết quả thất bại đúng kỳ vọng. Output và log khớp với sample output yêu cầu.

## Kết luận

Về kỹ thuật, cần tuân thủ chặt chẽ định dạng header và cách xử lý padding khi truyền dữ liệu theo khối. Về bảo mật, việc tách kênh khóa/dữ liệu giúp giảm rủi ro lẫn lộn nhưng vẫn cần kiểm tra toàn vẹn để phát hiện sửa đổi. AES-CBC không tự xác thực nên phải kết hợp cơ chế kiểm tra dữ liệu nếu mở rộng bài toán thực tế.
