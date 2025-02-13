# Banking payment, security architecture, risk management


# Rủi ro mô hình hiện tại

Rủi ro an toàn thông tin của mô hình banking payment hiện tại

![alt text](images/1_security_risks.png)

1. Thiếu Phần Mềm Antivirus/Firewall Chuyên Dụng.
2. Điểm Đơn Lẻ Hỏng Hóc (Single Point of Failure) - Nếu router tích hợp firewall hoặc thiết bị cân bằng tải hỏng dẫn đến sự cố ngừng trệ toàn bộ mạng.
3. Mô Hình Domain Không Được Quản Lý Chặt Chẽ.
4. Không Có Chính Sách Sao Lưu Và Phục Hồi Dữ Liệu.
5. Không Có Chính Sách Vận Hành - dẫn đến việc thực hành quản lý hệ thống không nhất quán, từ đó tạo ra các lỗ hổng an ninh.
6. Không Có Chính Sách An Ninh Thông Tin - nhân viên có thể không nhận thức được vai trò của mình trong việc duy trì an ninh, dẫn đến các thực hành không an toàn.
7. Trung Tâm Dữ Liệu Tập Trung - Tất cả máy chủ đều đặt tại một trung tâm dữ liệu có thể rủi ro nếu không có địa điểm phục hồi sau thảm họa.
8. Nguy Cơ Tấn Công DDoS.
9. Giám Sát Và Cảnh Báo Không Đủ - có thể có sự chậm trễ hoặc không phản ứng trước các mối đe dọa an ninh đang diễn ra.
10. Phân đoạn mạng không đủ - kẻ xâm nhập có thể dễ dàng lan truyền từ một phần của mạng sang các phần khác.

## Rủi ro liên quan đến mất mát dữ liệu

### Attacker:
- Tấn công social engineering.
- Tấn công giả mạo.
- Tấn công vào các lỗ hổng bảo mật SQL.
- Tấn công vào nhân viên, mua chuộc, dụ dỗ, đe dọa,...
- Tấn công hệ thống bằng malware.
- Tấn công vật lý: đánh cắp tài sản, tài liệu giấy, phá hoại hệ thống điện,...

### Nhân viên:
- Sử dụng thiết bị cá nhân, các phần mềm trao đổi nội dung thông tin, nhắn tin có dữ liệu ra ngoài.
- Nhân viên cài cắm thiết bị lạ, software lạ.
- Làm mất thiết bị.
- Nhân viên truy cập dữ liệu trái phép.
- Chưa có chính sách chống social engineering

## Giải pháp

### Mô hình tổng thể
![alt text](images/2_security_arachitecture.png)

### Mô hình chi tiết

![alt text](images/3_security_arachitecture_detail.png)

### Traffic flow

![alt text](images/4_trafic_flow.png)

## XÂY DỰNG CHÍNH SÁCH

* IDS: Đặt 1 IDPS trước các public gateway để filter các traffic public đi từ bên ngoài vào mạng nội bộ, đồng thời giảm tải traffic cho router gateway. 

* Firewall: Đặt firewall phía sau router để giám sát các traffic mạng đi đến mạng nội bộ. Dùng NGFW để filter cũng như phát hiện các cuộc tấn công dựa vào các signature base. Ngoài ra, NGFW còn có khả năng đọc vào payload của các gói tin, dựa vào đó chúng ta có thể ngăn chặn các cuộc tấn công liên quan đến tầng application.

### Chính sách cho Firewall

- 1: Tất cả các giao dịch không được ủy quyền đều sẽ bị chặn.
- 2: Tất cả các cổng không cần thiết sẽ bị đóng.
- 3: Địa chỉ IP nằm ngoài danh sách trắng sẽ bị chặn.
- 4: Thời gian không hoạt động tối đa được cho phép là 15 phút.
- 5: Các phiên bản phần mềm của firewall phải được cập nhật định kỳ.
- 6: Được yêu cầu xác thực hai yếu tố để truy cập vào hệ thống quản lý firewall.
- 7: Không cho phép quyền truy cập SSH từ internet công cộng.
- 8: Ghi lại và lưu trữ tất cả các sự kiện truy cập.
- 9: Tỉ lệ gói tin bị từ chối trên tổng số gói tin phải được giám sát.
- 10: Đánh giá và kiểm tra cấu hình firewall ít nhất mỗi quý.




