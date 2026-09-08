---
name: usp-product
description: Nhập một URL trang sản phẩm, thu thập nội dung mô tả và ảnh sản phẩm từ nguồn chính thức, rồi tạo hoặc cập nhật hồ sơ USP theo schema của dự án. Dùng khi người dùng gọi /usp_product hoặc yêu cầu nhập sản phẩm từ website; không tự biến nội dung chưa được xác nhận thành claim verified.
---

# Nhập USP từ trang sản phẩm

Skill này xử lý yêu cầu dạng:

```text
/usp_product https://example.com/products/product-slug
```

Đọc `PROJECT.md`, `brand/brand-profile.yaml` và `products/_template/product.yaml` trước khi sửa file. Nếu onboarding thương hiệu chưa hoàn tất, vẫn có thể thu thập sản phẩm nhưng phải báo rõ trạng thái onboarding và không tạo banner chính thức.

## Mục tiêu

Từ URL sản phẩm, tạo một thư mục sản phẩm có:

- `products/<product-id>/product.yaml`: tên, loại, giá, USP, copy được công bố, nguồn và trạng thái dữ liệu.
- `products/<product-id>/images/reference/`: ảnh sản phẩm gốc tải từ trang chính thức, không crop, retouch, đổi tên làm mất phần mở rộng hoặc ghi đè ảnh đã có.

## Quy trình

1. Kiểm tra URL là trang sản phẩm cụ thể, không phải trang danh mục. Nếu URL chuyển hướng, ghi URL cuối cùng làm `source_location` và báo cho người dùng.
2. Đọc HTML/rendered content, JSON-LD (`Product`), Open Graph và các ảnh được dùng bởi trang. Ưu tiên tên sản phẩm, mô tả, loại, giá hiện tại, SKU, thông tin bao bì, thành phần, chứng nhận và các lợi ích được trang chính thức viết rõ.
3. Lấy ảnh sản phẩm từ `og:image`, JSON-LD `image`, gallery sản phẩm hoặc ảnh chính trong nội dung. Tải ảnh có độ phân giải tốt nhất; giữ nguyên bản gốc và ghi URL nguồn nếu schema hoặc asset manifest hỗ trợ.
4. Tạo `product-id` dạng chữ thường ASCII kebab-case, ổn định theo slug sản phẩm. Nếu thư mục đã tồn tại, đọc và cập nhật có chọn lọc; không xóa dữ liệu người dùng đã xác nhận.
5. Sao chép cấu trúc từ `products/_template/product.yaml`. Ghi nguồn cho mỗi dữ kiện:
   - `source_type: official_product_page`
   - `source_location: <URL trang sản phẩm cuối cùng>`
   - `checked_at: <YYYY-MM-DD>`
6. Dữ liệu trích nguyên văn hoặc rõ ràng từ trang có thể đánh dấu `observed` trước khi người dùng duyệt. Chỉ đánh dấu `verified` cho claim khi người dùng xác nhận, hoặc dự án đã quy định nguồn chính thức đủ để xác minh trường đó. Giá/khuyến mãi phải kèm thời hạn nếu trang có nêu; nếu không, không coi là khuyến mãi lâu dài.
7. Không suy luận USP từ tên, ảnh, màu sắc, đánh giá không có nguồn, SEO text mơ hồ hoặc thông tin của sản phẩm khác. Không nhập claim tuyệt đối như “tốt nhất”, “100%”, “an toàn”, “chữa trị” nếu trang không ghi rõ và người dùng chưa duyệt.
8. Trước khi ghi claim mới vào hồ sơ, báo tóm tắt dữ liệu đã trích, ảnh đã tải, dữ liệu còn thiếu và các claim cần người dùng duyệt. Nếu người dùng chỉ yêu cầu crawl, có thể lưu ở trạng thái `observed`/`pending` và không tự chạy tạo banner.

## Quy tắc ảnh

- Ảnh dùng làm reference phải là ảnh sản phẩm, không phải banner quảng cáo, logo riêng hoặc ảnh lifestyle không có sản phẩm.
- Không cắt nền, chỉnh màu, xóa watermark hay ghép nhiều ảnh.
- Nếu chỉ tải được ảnh thumbnail hoặc URL bị chặn, báo lỗi và yêu cầu người dùng cung cấp ảnh gốc; không dùng ảnh thay thế mà không thông báo.
- Đặt tên dễ truy vết, ví dụ `product-front.jpg`, `product-back.jpg`, `product-gallery-01.jpg`; cập nhật đúng các đường dẫn tương đối trong `reference_images`.

## Báo cáo sau khi chạy

Trả lời người dùng bằng:

1. URL đã đọc và URL cuối cùng sau redirect (nếu có).
2. `product-id` và đường dẫn `product.yaml`.
3. Danh sách ảnh đã tải và ảnh nào được chọn làm `primary`.
4. Bảng ngắn các facts/USP đã trích cùng trạng thái `observed`, `pending` hoặc `verified`.
5. Các claim cần người dùng xác nhận trước khi dùng làm banner.
6. Bước tiếp theo, ví dụ: “Xác nhận các USP trên, sau đó chạy `/batch_banner ...`” hoặc dùng workflow tạo batch hiện có.

Không tạo prompt banner, không tạo batch và không đánh dấu `onboarding: complete` chỉ vì đã crawl xong một URL.
