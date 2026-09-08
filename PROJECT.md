# Thư viện prompt banner theo thương hiệu

Đây là dự án độc lập với nền tảng AI, dùng để xây dựng kho kiến thức thương hiệu và kết hợp kho đó với prompt tham khảo nhằm tạo prompt banner hàng loạt. Dự án không huấn luyện mô hình.

## Nguồn dữ liệu chuẩn

- `brand/`: nhận diện, logo, font, giọng văn và quy tắc hình ảnh dùng chung; không lưu USP riêng của sản phẩm.
- `products/<product-id>/`: hồ sơ, ảnh tham chiếu và USP có nguồn của từng sản phẩm.
- `library/prompt-templates/`: prompt nguồn chỉ dùng làm cảm hứng.
- `jobs/<batch-id>/manifest.yaml`: khai báo đầu vào và thiết lập của batch.
- `instructions/`: quy trình thiết lập, tạo prompt đơn và chạy batch.
- `outputs/<batch-id>/<product-id>/`: kết quả; không dùng làm dữ liệu đầu vào.

Không ghi đè tài sản gốc hoặc tự nghĩ ra claim, giá, chứng nhận, font, màu hay biến thể logo.

## Định tuyến công việc

1. Đọc `brand/brand-profile.yaml`.
2. Nếu chưa hoàn tất thiết lập, làm theo `instructions/ONBOARDING.md`.
3. Khi cập nhật thương hiệu, chỉ sửa file liên quan trong `brand/` và ghi nguồn.
4. Với một sản phẩm, làm theo `instructions/GENERATE_BANNERS.md`.
5. Với nhiều sản phẩm, làm theo `instructions/BATCH_WORKFLOW.md` và manifest; không tự quét thư mục để đoán đầu vào.
