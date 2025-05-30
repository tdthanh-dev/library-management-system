# 📚 TÀI LIỆU PHÂN TÍCH THỰC THỂ HỆ THỐNG QUẢN LÝ THƯ VIỆN

**Ngày tạo:** 28/05/2025  
**Người tạo:** tdthanh.dev  
**Thông tin thêm:** https://github.com/tdthanh-dev/  
**Phiên bản:** 1.0

## 1. MỞ ĐẦU

Trong quá trình phát triển Hệ thống Quản lý Thư viện Trực tuyến cho Trường Đại học Công nghệ Thông tin, việc xác định và phân tích các thực thể là bước quan trọng đầu tiên trong giai đoạn thiết kế hệ thống. Tài liệu này sẽ trình bày chi tiết về tất cả các thực thể cần thiết, mối quan hệ giữa chúng, cũng như các quy tắc kinh doanh được áp dụng.

Hệ thống quản lý thư viện này được thiết kế để phục vụ ba nhóm người dùng chính: sinh viên, giảng viên và nhân viên thư viện. Mỗi nhóm có những nhu cầu và quyền hạn khác nhau, điều này được phản ánh rõ ràng trong cấu trúc dữ liệu và thiết kế các thực thể.

## 2. PHÂN TÍCH CÁC THỰC THỂ CHÍNH

### 2.1 Thực thể User (Người dùng)

Thực thể User đóng vai trò trung tâm trong hệ thống, đại diện cho tất cả các cá nhân có thể tương tác với thư viện. Thực thể này được thiết kế để phục vụ nhiều loại người dùng khác nhau với các đặc quyền riêng biệt.

Mỗi người dùng trong hệ thống được xác định duy nhất thông qua một ID tự tăng và email. Trường email không chỉ đóng vai trò là phương tiện đăng nhập mà còn là kênh liên lạc chính để gửi thông báo về tình trạng mượn trả sách. Mật khẩu được lưu trữ dưới dạng đã được mã hóa để đảm bảo tính bảo mật.

Thông tin cá nhân bao gồm họ tên được tách thành hai trường firstName và lastName để thuận tiện cho việc hiển thị và tìm kiếm. Trường userCode lưu trữ mã số sinh viên (MSSV) hoặc mã số giảng viên (MSGV), đây là định danh quan trọng trong môi trường trường học.

Đặc biệt quan trọng là trường userType, sử dụng kiểu enum để phân loại người dùng thành STUDENT, TEACHER, LIBRARIAN, hoặc ADMIN. Phân loại này quyết định quyền hạn và giới hạn của từng người dùng trong hệ thống. Ví dụ, sinh viên chỉ được mượn tối đa 5 cuốn sách trong 14 ngày, trong khi giảng viên có thể mượn 10 cuốn trong 30 ngày.

### 2.2 Thực thể Book (Sách)

Thực thể Book chứa đựng tất cả thông tin cần thiết về mỗi đầu sách trong thư viện. Thiết kế này cân bằng giữa tính đầy đủ của thông tin và hiệu suất truy vấn.

Mã ISBN được sử dụng như một định danh toàn cầu duy nhất cho mỗi đầu sách, tuân thủ tiêu chuẩn quốc tế. Thông tin cơ bản như tên sách, tác giả, nhà xuất bản và năm xuất bản giúp người dùng dễ dàng tìm kiếm và nhận diện sách.

Một điểm đặc biệt quan trọng trong thiết kế là việc quản lý số lượng sách. Hệ thống sử dụng hai trường totalCopies và availableCopies để theo dõi tổng số bản và số bản có sẵn. Điều này cho phép thư viện quản lý chính xác tình trạng sách và ngăn chặn việc cho mượn khi không còn bản sẵn có.

Trường shelfLocation lưu trữ vị trí vật lý của sách trong thư viện, giúp nhân viên nhanh chóng tìm thấy sách khi cần. Trường price được lưu trữ để tính toán phí phạt tối đa khi sách bị hư hỏng hoặc mất.

### 2.3 Thực thể Category (Thể loại)

Thực thể Category được thiết kế để hỗ trợ phân loại sách theo hệ thống phân loại thư viện. Thiết kế này hỗ trợ cấu trúc phân cấp với trường parentCategoryId, cho phép tạo ra các thể loại con.

Ví dụ, thể loại "Công nghệ" có thể có các thể loại con như "Lập trình", "Mạng máy tính", "Trí tuệ nhân tạo". Cấu trúc này giúp người dùng dễ dàng duyệt sách theo chủ đề và hỗ trợ việc tìm kiếm nâng cao.

### 2.4 Thực thể Loan (Phiếu mượn)

Thực thể Loan là trung tâm của quy trình mượn trả sách, lưu trữ tất cả thông tin về mỗi giao dịch mượn sách. Thiết kế này phải đảm bảo tính chính xác và khả năng theo dõi chi tiết mọi hoạt động.

Mỗi phiếu mượn liên kết một người dùng với một cuốn sách thông qua userId và bookId. Ngày mượn (loanDate) được ghi nhận tự động khi tạo phiếu, trong khi ngày hạn trả (dueDate) được tính toán dựa trên loại người dùng - 14 ngày cho sinh viên và 30 ngày cho giảng viên.

Trường status sử dụng enum để theo dõi trạng thái phiếu mượn: ACTIVE (đang mượn), RETURNED (đã trả), OVERDUE (quá hạn). Hệ thống sẽ tự động cập nhật trạng thái OVERDUE cho các phiếu mượn vượt quá ngày hạn trả.

Tính năng gia hạn được quản lý thông qua renewalCount và isExtended. Mỗi người dùng chỉ được gia hạn một lần và chỉ khi sách chưa quá hạn và không có ai đặt trước.

### 2.5 Thực thể Reservation (Đặt trước)

Thực thể Reservation giải quyết tình huống khi sách đã hết bản sẵn có nhưng người dùng vẫn muốn mượn. Hệ thống đặt trước hoạt động theo nguyên tắc "ai đến trước được phục vụ trước".

Mỗi đặt trước có thời hạn (expiryDate) và vị trí trong hàng đợi (queuePosition). Khi có sách trả về, hệ thống tự động thông báo cho người đầu tiên trong hàng đợi và giữ sách trong 3 ngày. Nếu không đến lấy, sách sẽ được chuyển cho người tiếp theo.

### 2.6 Thực thể Fine (Phí phạt)

Thực thể Fine quản lý tất cả các khoản phạt phát sinh trong hệ thống. Phần lớn phí phạt đến từ việc trả sách muộn, được tính theo công thức 5,000 VNĐ mỗi ngày mỗi cuốn sách.

Hệ thống tự động tính toán số tiền phạt dựa trên số ngày quá hạn và cập nhật trạng thái từ PENDING sang PAID khi người dùng thanh toán. Trong một số trường hợp đặc biệt, admin có thể miễn phạt (WAIVED) với lý do cụ thể.

## 3. PHÂN TÍCH MỐI QUAN HỆ

### 3.1 Quan hệ One-to-Many

Hệ thống có nhiều quan hệ một-nhiều quan trọng. Mỗi User có thể có nhiều Loan, phản ánh thực tế rằng một người có thể mượn sách nhiều lần theo thời gian. Tương tự, mỗi Book có thể xuất hiện trong nhiều Loan khác nhau khi được mượn và trả nhiều lần.

Quan hệ giữa Loan và Fine cũng là một-nhiều, vì một phiếu mượn có thể phát sinh nhiều khoản phạt khác nhau (trả muộn, làm hư sách, mất sách). Điều này cho phép hệ thống quản lý chi tiết các khoản phí.

### 3.2 Quan hệ Many-to-Many

Quan hệ nhiều-nhiều chính trong hệ thống là giữa Book và Category. Một cuốn sách có thể thuộc nhiều thể loại (ví dụ, một cuốn sách về AI vừa thuộc "Công nghệ" vừa thuộc "Khoa học máy tính"), và một thể loại chứa nhiều cuốn sách khác nhau.

Để thực hiện quan hệ này, hệ thống sử dụng bảng trung gian BookCategory với các trường bổ sung như ngày phân loại và người thực hiện, giúp theo dõi lịch sử thay đổi.

## 4. CÁC THỰC THỂ HỖ TRỢ

### 4.1 Hệ thống Thông báo

Thực thể Notification đóng vai trò quan trọng trong việc duy trì liên lạc với người dùng. Hệ thống gửi thông báo cho nhiều sự kiện: nhắc nhở trước hạn trả sách 3 ngày, thông báo quá hạn, xác nhận mượn/trả thành công, và thông báo khi có sách đặt trước sẵn sàng.

EmailLog lưu trữ chi tiết mọi email được gửi, bao gồm trạng thái gửi và lý do thất bại nếu có. Điều này giúp admin theo dõi và khắc phục sự cố liên lạc.

### 4.2 Hệ thống Kiểm toán

AuditLog ghi lại mọi thay đổi quan trọng trong hệ thống, từ việc tạo mới, cập nhật đến xóa dữ liệu. Mỗi bản ghi bao gồm thông tin về người thực hiện, thời gian, và chi tiết thay đổi. Điều này đảm bảo tính minh bạch và khả năng truy vết khi cần thiết.

### 4.3 Cấu hình Hệ thống

SystemSetting cho phép quản trị viên điều chỉnh các tham số hệ thống mà không cần thay đổi code. Ví dụ, mức phí phạt hàng ngày, thời gian mượn tối đa, số lượng sách được mượn tối đa có thể được điều chỉnh thông qua bảng này.

## 5. QUY TẮC KINH DOANH VÀ RÀNG BUỘC

### 5.1 Ràng buộc về Người dùng

Hệ thống áp dụng các quy tắc nghiêm ngặt cho việc mượn sách. Sinh viên được phép mượn tối đa 5 cuốn sách trong thời gian 14 ngày, trong khi giảng viên có hạn mức 10 cuốn trong 30 ngày. Người dùng không được mượn sách mới khi còn nợ phí phạt chưa thanh toán.

### 5.2 Ràng buộc về Sách

Số lượng sách sẵn có không được phép âm và luôn phải nhỏ hơn hoặc bằng tổng số sách. Hệ thống không cho phép xóa sách đang được mượn và tự động cập nhật số lượng sẵn có khi có giao dịch mượn/trả.

### 5.3 Tính toán Phí phạt

Phí phạt được tính tự động với mức 5,000 VNĐ mỗi ngày cho mỗi cuốn sách quá hạn. Tuy nhiên, tổng phí phạt không vượt quá 50% giá trị sách để tránh gánh nặng quá lớn cho người dùng.

## 6. CHIẾN LƯỢC HIỆU SUẤT

### 6.1 Indexing

Để đảm bảo hiệu suất truy vấn, hệ thống sử dụng các index chiến lược. Index được tạo trên các trường thường xuyên được tìm kiếm như email, mã số sinh viên, ISBN, và tiêu đề sách. Đặc biệt, full-text index được sử dụng cho việc tìm kiếm nội dung sách.

### 6.2 Partitioning

Đối với các bảng có lượng dữ liệu lớn như Loan và AuditLog, hệ thống có thể áp dụng partitioning theo thời gian để cải thiện hiệu suất truy vấn và quản lý dữ liệu.

## 7. KẾT LUẬN

Thiết kế thực thể của Hệ thống Quản lý Thư viện này cân bằng giữa tính đầy đủ, hiệu suất và khả năng mở rộng. Cấu trúc dữ liệu được thiết kế để hỗ trợ tất cả quy trình kinh doanh của thư viện từ cơ bản đến nâng cao, đồng thời đảm bảo tính toàn vẹn dữ liệu và khả năng theo dõi chi tiết.

Với 12 thực thể chính và các bảng trung gian, hệ thống có thể xử lý hiệu quả các yêu cầu của một thư viện hiện đại, từ quản lý cơ bản đến báo cáo phức tạp và phân tích dữ liệu. Thiết kế này cũng đủ linh hoạt để thích ứng với các yêu cầu thay đổi trong tương lai.
