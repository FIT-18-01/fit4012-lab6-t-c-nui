# Peer Review Response

## Đã nhận xét
- Kiểm tra và xác nhận hệ thống AES socket đã sử dụng AES-CBC với padding PKCS#7.
- Xác minh các tệp bắt buộc đã có trong repository.
- Đề xuất sửa `receiver.py` để loại bỏ timeout trên socket lắng nghe trước khi `accept()`.

## Đã chỉnh sửa
- Thêm tệp bắt buộc `peer-review-response.md`.
- Đã sửa `receiver.py` để server chờ kết nối đến kênh khóa và kênh dữ liệu mà không bị timeout trước khi kết nối.

## Kết luận
- Hệ thống đã hoạt động đúng trong bài kiểm tra local sender/receiver.
- Tệp yêu cầu của bài nộp hiện đã đầy đủ.
