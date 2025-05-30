# HỆ THỐNG QUẢN LÝ THƯ VIỆN

**Phiên bản:** 1.0  
**Ngày tạo:** 28/05/2025  
**Tác giả:** tdthanh.dev

## TỔNG QUAN

Hệ thống Quản lý Thư viện là một giải pháp toàn diện được phát triển cho Trường Đại học Công nghệ Thông tin nhằm hiện đại hóa và tự động hóa tất cả các hoạt động quản lý thư viện. Hệ thống cung cấp nền tảng vững chắc cho việc quản lý danh mục sách, mượn trả, đặt trước, và các dịch vụ thư viện khác.

## CHỨC NĂNG CHÍNH

- **Quản lý sách:** Thêm, sửa, xóa và tìm kiếm sách trong thư viện
- **Quản lý người dùng:** Đăng ký, cập nhật và phân quyền người dùng (sinh viên, giảng viên, thủ thư)
- **Mượn trả sách:** Xử lý các giao dịch mượn và trả sách
- **Đặt trước sách:** Hệ thống đặt trước khi sách không có sẵn
- **Quản lý phí phạt:** Tính toán và xử lý phí phạt cho sách trả muộn hoặc hư hỏng
- **Thông báo:** Gửi thông báo cho người dùng về hạn trả sách và sách được đặt trước
- **Báo cáo và thống kê:** Tạo báo cáo về hoạt động của thư viện

## KIẾN TRÚC HỆ THỐNG

Hệ thống được thiết kế theo kiến trúc nhiều lớp:

- **Lớp giao diện:** Giao diện web và ứng dụng di động
- **Lớp API:** RESTful API cho tất cả các chức năng
- **Lớp dịch vụ:** Xử lý logic nghiệp vụ
- **Lớp dữ liệu:** Lưu trữ và quản lý dữ liệu

Dự án bao gồm các tài liệu sau:

1. **Topic.md** - Phân tích thực thể và mối quan hệ trong hệ thống
2. **Diagrams.md** - Các sơ đồ UseCase, ERD và kiến trúc hệ thống
3. **BuildingBlocks.md** - Lộ trình phát triển theo từng giai đoạn
4. **ClassDG.md** - Chi tiết về các lớp nghiệp vụ và logic xử lý
5. **APIDocumentation.md** - Tài liệu về các API endpoints
6. **UIDesign.md** - Thiết kế giao diện người dùng và wireframes
7. **TestingPlan.md** - Kế hoạch kiểm thử hệ thống

## CÔNG NGHỆ SỬ DỤNG

- **Backend:** Java Spring Boot
- **Frontend:** React.js
- **Database:** PostgreSQL
- **Cache:** Redis
- **Search:** Elasticsearch
- **Authentication:** JWT

## HƯỚNG DẪN TRIỂN KHAI

Để triển khai hệ thống:

1. Tham khảo tài liệu BuildingBlocks.md để hiểu lộ trình phát triển
2. Thiết kế database dựa trên ERD trong Diagrams.md
3. Xây dựng backend theo tài liệu ClassDG.md và APIDocumentation.md
4. Phát triển frontend dựa trên UIDesign.md
5. Kiểm thử theo TestingPlan.md

## LIÊN HỆ

Để biết thêm thông tin, vui lòng liên hệ: https://github.com/tdthanh-dev/
