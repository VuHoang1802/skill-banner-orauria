# Quy trình thiết lập thương hiệu

Giải thích ngắn rằng câu trả lời sẽ được lưu cục bộ để dùng lại. Mỗi lần hỏi tối đa năm câu liên quan, dùng ngôn ngữ của người dùng và không hỏi lại dữ liệu đã có. Nếu chưa biết, ghi `unknown`, không đoán.

Trạng thái dữ liệu: `verified` là được người dùng cung cấp hoặc duyệt; `observed` là quan sát từ tài sản hoặc nguồn chính thức nhưng chưa duyệt; `suggested` là đề xuất chưa duyệt. Trước khi đặt onboarding thành `complete`, tóm tắt hồ sơ và xin người dùng xác nhận.

## Nội dung cần thu thập

1. Tên chính thức, cách viết, mô tả, website, thị trường, ngôn ngữ và người duyệt.
2. Nhóm khách hàng, vấn đề giải quyết, động lực mua, phân khúc giá, tính cách thương hiệu và đối thủ không nên bắt chước.
3. Logo gốc: ưu tiên SVG/AI/EPS/PDF, PNG trong suốt, biến thể nền sáng/tối, biểu tượng, wordmark và đơn sắc. Lưu nguyên trạng tại `brand/assets/logos/original/`; bản xử lý đặt tại `derived/` và ghi rõ nguồn gốc.
4. Màu chính, phụ, nhấn, trung tính, màu cấm; mã màu; font, weight, giấy phép, font thay thế và quy tắc typography. Màu lấy mẫu từ ảnh giữ trạng thái `observed` đến khi được duyệt.
5. Phong cách ảnh, ánh sáng, góc máy, nền, chất liệu, đạo cụ, con người, minh họa, icon, hình khối, texture, bóng, khoảng trống và mẫu thích/không thích. Ảnh tham khảo thương hiệu lưu trong `brand/assets/references/`; ảnh sản phẩm chỉ lưu tại `products/<product-id>/images/reference/`.
6. Giọng văn, từ ngữ, tagline, CTA, claim, bằng chứng, tên sản phẩm, từ cấm, giới hạn pháp lý, quy tắc giá, giảm giá, bảo hành, chứng nhận và thành phần bắt buộc trên banner.
7. Kênh, kích thước, tỷ lệ, mục tiêu chiến dịch, số concept, mô hình tạo ảnh và việc chữ được render bởi AI hay thêm sau.

## Lưu dữ liệu

Sau mỗi nhóm câu trả lời được duyệt: cập nhật `brand/brand-profile.yaml`; ghi quy tắc chi tiết vào file Markdown tương ứng; thêm tài sản vào `brand/asset-manifest.yaml` cùng nguồn, trạng thái và mục đích; cập nhật `onboarding.last_updated`; chỉ đặt `complete` sau khi người dùng duyệt bản tóm tắt.
