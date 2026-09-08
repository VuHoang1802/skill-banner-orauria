# Tạo prompt banner hàng loạt theo thương hiệu

Dự án chuyển prompt sáng tạo thành prompt hình ảnh cho một hoặc nhiều sản phẩm thuộc cùng thương hiệu.

## Đặt dữ liệu ở đâu

- Logo: `brand/assets/logos/original/`
- Quy tắc thương hiệu: `brand/brand-profile.yaml`, `brand/logo-rules.md`, `brand/visual-language.md`, `brand/voice-and-copy.md`
- Ảnh sản phẩm: `products/<product-id>/images/reference/`
- USP và nguồn: `products/<product-id>/product.yaml`
- Prompt mẫu: `library/prompt-templates/*.txt`
- Cấu hình batch: `jobs/<batch-id>/manifest.yaml`
- Prompt kết quả: `outputs/<batch-id>/<product-id>/prompts.txt`

Đọc `instructions/BATCH_WORKFLOW.md` để vận hành. Sao chép thư mục `_template` khi thêm sản phẩm hoặc chiến dịch; không sửa template gốc. Mỗi prompt đầu ra là một đoạn văn trên đúng một dòng, không tiêu đề, metadata hoặc dòng trống. Dự án không huấn luyện mô hình ảnh.
