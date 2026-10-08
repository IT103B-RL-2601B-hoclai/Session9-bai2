 BÁO CÁO PHÂN TÍCH LỖI VÀ TEST CASES (BÀI 2)

1. Phân tích nguyên nhân kỹ thuật

- Lỗi 1 (Lấy giá phòng): Dòng lệnh `const basePrice = bookingReservation.priceKey;` dùng Dot Notation khiến JavaScript tìm khóa có tên nguyên văn là "priceKey", dẫn đến trả về `undefined` và làm tổng tiền bị tính thành `NaN`. Sửa thành `bookingReservation[priceKey]`.
- Lỗi 2 (Xử lý voucher): Gán `bookingReservation.discountCode = undefined;` chỉ làm thuộc tính mang giá trị `undefined` chứ không xóa khỏi đối tượng, dẫn đến kiểm tra `'discountCode' in bookingReservation` vẫn ra `true`. Phải dùng toán tử `delete bookingReservation.discountCode;` để loại bỏ hoàn toàn.
- Lỗi 3 (Duyệt vòng lặp): Dòng `bookingReservation.key` trong vòng lặp `for...in` cố định tìm khóa tên là "key" (không tồn tại) nên in ra toàn bộ giá trị là `undefined`. Sửa thành Bracket Notation `bookingReservation[key]` để lấy giá trị theo biến `key` động.

2. Bảng Test Cases đối chứng

| Trường hợp kiểm thử | Dữ liệu đầu vào | Kết quả sai thực tế | Kết quả đúng mong đợi |
| --- | --- | --- | --- |
| Voucher không hợp lệ (!isVoucherValid) | isVoucherValid: false, checkInHour: 9 | discountCode: undefined, 'discountCode' in obj là true, các giá trị in ra bị undefined | discountCode bị xóa hẳn, 'discountCode' in obj là false, in đầy đủ các thuộc tính và giá trị thực tế |
| Voucher hợp lệ (isVoucherValid) | isVoucherValid: true, checkInHour: 9 | Thuộc tính discountCode còn nhưng vòng lặp for..in vẫn in ra undefined | discountCode: SUMMER10 được giữ nguyên, 'discountCode' in obj là true, in đầy đủ thông tin chuẩn |