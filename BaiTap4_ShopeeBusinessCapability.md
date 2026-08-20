# Bài tập 4: Phân rã Shopee theo Khả năng kinh doanh (Business Capability)

## 1. Mở đầu: Tư duy của Kiến trúc sư trưởng
Khi tiếp cận một siêu ứng dụng (Super App) như Shopee, thay vì nhảy ngay vào việc thiết kế database hay chọn công nghệ, kiến trúc sư sẽ nhìn vào bức tranh kinh doanh (Business Domain). Phương pháp phân rã theo **Khả năng kinh doanh (Business Capability)** giúp chia hệ thống thành các module (Service) có tính độc lập cao, mỗi module giải quyết trọn vẹn một bài toán nghiệp vụ cụ thể và không bị chồng chéo chức năng.

Tư duy phân rã này không chỉ áp dụng cho một hệ sinh thái khổng lồ, mà hoàn toàn có thể thu nhỏ để áp dụng làm khung sườn cho các dự án thương mại điện tử chuyên biệt (chẳng hạn như một hệ thống kinh doanh đồ nội thất), nơi bạn cũng cần tổ chức dữ liệu cấu trúc chặt chẽ từ thông tin hàng hóa đến quản lý giao vận đồ cồng kềnh.

## 2. Danh sách 6 Module (Service) nghiệp vụ chính của Shopee

Dưới đây là 6 module cốt lõi được bóc tách từ quy trình kinh doanh của Shopee:

### 1. User Account & Identity Service (Module Quản lý Người dùng & Định danh)
*   **Trách nhiệm:** Chịu trách nhiệm toàn bộ về vòng đời của một tài khoản. Module này phân định rõ ranh giới giữa Người mua (Buyer) và Người bán (Seller), đồng thời quản lý xác thực (Authentication), phân quyền, thông tin cá nhân và lịch sử địa chỉ.
*   **Điểm độc lập:** Các service khác khi cần thông tin user chỉ lưu `UserID` và gọi sang module này để lấy data, không tự quản lý mật khẩu hay email.

### 2. Product Catalog Management Service (Module Quản lý Danh mục & Sản phẩm)
*   **Trách nhiệm:** Nơi lưu trữ và hiển thị "Mặt tiền" của sàn. Quản lý thông tin chi tiết của hàng triệu sản phẩm, biến thể (màu sắc, kích thước, chất liệu), cấu trúc danh mục, giá cả và tồn kho hiện tại (Inventory).
*   **Điểm độc lập:** Tách biệt hoàn toàn việc "trưng bày sản phẩm" với việc "bán sản phẩm".

### 3. Order Management Service - OMS (Module Quản lý Đơn hàng)
*   **Trách nhiệm:** Trái tim của hệ thống e-commerce. Quản lý toàn bộ vòng đời của một đơn hàng từ lúc người dùng nhấn nút "Đặt hàng" (Checkout), chờ xác nhận, đóng gói, cho đến khi hoàn thành hoặc hoàn trả.
*   **Điểm độc lập:** Nhận dữ liệu đầu vào từ Giỏ hàng (Cart) và điều phối các module khác (Thanh toán, Giao vận) để hoàn tất quy trình.

### 4. Payment & Wallet Service (Module Thanh toán & Ví điện tử)
*   **Trách nhiệm:** Xử lý dòng tiền. Module này tính toán tổng tiền cuối cùng, tích hợp với các cổng thanh toán bên thứ 3 (Napas, Visa/Mastercard) và quản lý hệ thống ví nội bộ (ShopeePay, Shopee Xu).
*   **Điểm độc lập:** Chỉ quan tâm đến trạng thái giao dịch (Thành công/Thất bại), không cần biết khách hàng mua sản phẩm gì.

### 5. Logistics & Shipping Service (Module Quản lý Giao vận)
*   **Trách nhiệm:** Quản lý hành trình vật lý của gói hàng. Module này lo việc tính toán phí ship dựa trên khoảng cách và cân nặng, tích hợp API với các đơn vị vận chuyển (SPX, GHTK, GHN), và cập nhật mã vận đơn (Tracking).
*   **Điểm độc lập:** Nhận lệnh từ Order Service và làm việc trực tiếp với đối tác bên ngoài để đảm bảo hàng đến tay người mua.

### 6. Promotion & Marketing Service (Module Quản lý Khuyến mãi)
*   **Trách nhiệm:** Chịu trách nhiệm cho các chiến dịch Flash Sale, quản lý Voucher (miễn phí vận chuyển, giảm giá shop, hoàn xu), và các quy tắc giảm giá phức tạp (logic áp dụng nhiều mã cùng lúc).
*   **Điểm độc lập:** Module này cung cấp API để Checkout/Cart gọi sang hỏi: "Với giỏ hàng này thì được giảm bao nhiêu tiền?", giữ cho logic tính toán đơn hàng không bị phình to.

## 3. Kết luận
Bằng cách phân rã theo Khả năng kinh doanh, mỗi Service trên có thể được giao cho một Team phát triển độc lập. Họ có thể tự chọn công nghệ (Java, C#, PHP...) và tự deploy mà không làm "chết" các module khác, đáp ứng đúng triết lý của hệ thống phân tán và kiến trúc Microservices.