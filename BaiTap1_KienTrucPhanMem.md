# Bài tập 1: Tầm quan trọng của Kiến trúc & Thuộc tính chất lượng

## 1. Tại sao trước khi bắt đầu dự án, việc chọn kiến trúc lại là "bước sống còn"?
Đối với một startup đang đứng giữa ngã ba đường (ra mắt nhanh hay xây dựng bền vững), kiến trúc phần mềm chính là bản thiết kế móng của một ngôi nhà. Việc lựa chọn kiến trúc đóng vai trò sống còn vì:
* **Định hình sự phát triển dài hạn (Scalability & Evolution):** Nếu chọn sai kiến trúc, khi startup phát triển và lượng người dùng tăng đột biến, hệ thống sẽ sụp đổ.
* **Quản lý rủi ro và "Nợ kỹ thuật" (Technical Debt):** Việc code nhanh để ra mắt (Quick and Dirty) sẽ tạo ra nợ kỹ thuật. Một kiến trúc tốt giúp giảm thiểu rủi ro hệ thống.
* **Ảnh hưởng trực tiếp đến chi phí và nhân sự:** Kiến trúc quyết định công nghệ sử dụng, cách triển khai server, và cấu trúc team.

## 2. Các loại kiến trúc phần mềm phổ biến
* **Kiến trúc nguyên khối (Monolithic Architecture):** Toàn bộ ứng dụng (UI, xử lý logic, database access) được đóng gói vào một khối duy nhất. Ưu điểm là dễ test, dễ deploy ở giai đoạn đầu, phù hợp với startup cần ra mắt sản phẩm nhanh.
* **Kiến trúc vi dịch vụ (Microservices Architecture):** Hệ thống được chia thành nhiều dịch vụ nhỏ, độc lập. Ưu điểm là khả năng mở rộng tuyệt vời, một dịch vụ lỗi không kéo theo cả hệ thống.
* **Kiến trúc phân tầng (Layered/N-Tier Architecture):** Chia ứng dụng thành các tầng (Presentation, Business Logic, Data Access). Ưu điểm là dễ bảo trì và thay thế từng thành phần.

## 3. Các thuộc tính chất lượng (Quality Attributes) của phần mềm
Để đánh giá một "Kiến trúc tốt", chúng ta phải nhìn vào các yếu tố phi chức năng (Non-functional):
* **Scalability (Khả năng mở rộng):** Khả năng hệ thống xử lý lượng tải tăng lên (thêm user, thêm dữ liệu) mà không bị giảm hiệu suất.
* **Availability (Tính sẵn sàng):** Tỷ lệ thời gian hệ thống hoạt động bình thường so với tổng thời gian.
* **Maintainability (Khả năng bảo trì):** Mức độ dễ dàng khi sửa lỗi, nâng cấp, hoặc thêm tính năng mới.
* **Performance (Hiệu năng):** Tốc độ phản hồi của hệ thống và khả năng xử lý đồng thời.
* **Security (Bảo mật):** Khả năng chống lại các cuộc tấn công, bảo vệ dữ liệu người dùng và kiểm soát quyền truy cập.