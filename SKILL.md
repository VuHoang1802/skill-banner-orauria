---
name: brand-banner-prompts
description: Sắp xếp tài sản thương hiệu, thu thập USP đã xác minh cho nhiều sản phẩm và chuyển đổi hàng loạt prompt template thành prompt hình ảnh đúng thương hiệu. Dùng khi thiết lập thương hiệu, nhập catalog, chuẩn bị batch hoặc tạo bộ prompt; không huấn luyện mô hình hay tạo ảnh nếu chưa được yêu cầu.
---

# Tạo prompt banner theo thương hiệu

Đọc `PROJECT.md` làm nguồn định tuyến chuẩn. Nếu onboarding chưa hoàn tất, làm theo `instructions/ONBOARDING.md`.

Với một sản phẩm, đọc `instructions/GENERATE_BANNERS.md`. Với batch, đọc `instructions/BATCH_WORKFLOW.md` và manifest được chọn. Kiến thức thương hiệu luôn ưu tiên hơn mẫu tham khảo.

Khi người dùng gọi `/usp_product <url>` hoặc yêu cầu nhập sản phẩm từ website, đọc `skills/usp-product/SKILL.md` và thực hiện workflow crawl nội dung/ảnh theo nguồn chính thức. Skill này tạo hoặc cập nhật `products/<product-id>/product.yaml`; không tự biến dữ liệu chưa được xác nhận thành claim `verified` và không tự tạo banner.

Không tự nghĩ ra quy tắc hoặc dữ kiện thương mại, không sửa bản gốc duy nhất của tài sản và không tạo ảnh nếu người dùng chưa yêu cầu.
