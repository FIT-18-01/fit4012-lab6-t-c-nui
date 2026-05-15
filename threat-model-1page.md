# Threat Model - Lab 6 AES-CBC Socket

## Thông tin nhóm

- Thành viên 1: Nguyễn Vân Đạt
- Thành viên 2: TODO_STUDENT

## Assets

Các tài sản cần bảo vệ gồm plaintext, AES key, IV, ciphertext, file đầu vào/đầu ra và log hệ thống. Ngoài ra, tính toàn vẹn của gói tin (length header + payload) cũng là tài sản quan trọng.

## Attacker model

Đối tượng tấn công có thể nghe lén trên mạng LAN, bắt gói tin ở key channel hoặc data channel. Họ có thể sửa ciphertext, phát lại packet cũ hoặc đọc log nếu có quyền truy cập máy.

## Threats

Các mối đe dọa chính gồm:
- Lộ khóa nếu key channel bị nghe lén hoặc key/IV gửi plaintext.
- Tampering khi ciphertext bị sửa dẫn đến dữ liệu giải mã sai hoặc bị lỗi.
- Replay attack khi packet cũ bị gửi lại làm Receiver xử lý dữ liệu không mong muốn.
- Log leakage nếu log vô tình ghi key hoặc dữ liệu nhạy cảm.
- No authentication khi Receiver không xác thực Sender nên dễ bị giả mạo.

## Mitigations

Biện pháp giảm thiểu gồm:
- Không gửi key plaintext trong hệ thống thật; dùng TLS hoặc cơ chế trao đổi khóa an toàn.
- Dùng AES-GCM hoặc thêm MAC để xác thực dữ liệu và phát hiện sửa đổi.
- Không ghi key thật vào log; lọc log nhạy cảm.
- Thêm nonce/timestamp để giảm replay.
- Bổ sung xác thực Sender.

## Residual risks

Rủi ro còn lại: key channel chỉ là mô phỏng, chưa có TLS hay xác thực nên vẫn có khả năng bị nghe lén hoặc giả mạo; cơ chế chống replay chưa đầy đủ trong phạm vi bài lab.
