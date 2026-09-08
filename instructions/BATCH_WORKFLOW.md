# Quy trình tạo prompt hàng loạt

## Cấu trúc thư mục

```text
brand/                              Tài sản và quy tắc thương hiệu dùng chung
products/<product-id>/product.yaml Hồ sơ, USP và nguồn của sản phẩm
products/<product-id>/images/reference/ Ảnh sản phẩm gốc
library/prompt-templates/           Prompt tham khảo
jobs/<batch-id>/manifest.yaml       Danh sách đầu vào của một lần chạy
outputs/<batch-id>/<product-id>/prompts.txt Kết quả từng sản phẩm
```

Dùng chữ thường ASCII dạng kebab-case cho `<product-id>` và `<batch-id>`. Không ghi đè logo, ảnh sản phẩm, template hoặc output cũ. Mỗi lần chạy lại phải có batch ID mới.

## Thu thập sản phẩm và USP

Sao chép `products/_template/` để tạo thư mục riêng cho từng sản phẩm. Đặt ảnh gốc vào `images/reference/`, không cắt hoặc chỉnh sửa ảnh. Hoàn thiện `product.yaml` trước khi thêm vào batch.

Ưu tiên nguồn USP theo thứ tự:

1. Tài liệu, nội dung bao bì, catalog hoặc xác nhận được người dùng phê duyệt.
2. Trang sản phẩm chính thức của thương hiệu.
3. Gian hàng được ủy quyền hoặc tài liệu bán hàng nội bộ.
4. Quan sát từ ảnh chỉ dùng cho bối cảnh hình ảnh trung tính, không dùng làm bằng chứng về chất lượng, nguồn gốc, thành phần, hiệu quả hay chứng nhận.

Mỗi dữ kiện phải có giá trị, trạng thái, loại nguồn, vị trí nguồn và ngày kiểm tra. `verified` dành cho dữ liệu được duyệt hoặc nguồn chính thức; `observed` dành cho quan sát trung tính; `pending` dành cho nội dung chờ xác nhận. Prompt chỉ được dùng claim `verified`. Giá và khuyến mãi phải có thời hạn hoặc xác nhận theo chiến dịch.

Không suy luận USP từ tên, hình dáng, đối thủ hoặc prompt mẫu. Nếu dữ kiện còn `pending`, chỉ dùng placeholder khi manifest cho phép; nếu không thì bỏ nội dung và ghi cảnh báo trong báo cáo batch.

## Chuẩn bị và chạy batch

Sao chép `jobs/_template/manifest.yaml` sang `jobs/<batch-id>/manifest.yaml`, rồi khai báo rõ sản phẩm và template. Mỗi sản phẩm phải có ít nhất một ảnh đọc được và `product.yaml` hoàn chỉnh. Có thể ghi đè headline, CTA hoặc khuyến mãi đã duyệt trong manifest mà không sửa dữ liệu catalog.

Mặc định tạo tích Descartes giữa tất cả sản phẩm bật và template được chọn. Giữ nguyên thứ tự sản phẩm trong manifest và thứ tự template trong file nguồn. Áp dụng `instructions/GENERATE_BANNERS.md` độc lập cho từng cặp; không để USP, giá, mô tả hoặc ưu đãi của sản phẩm này lọt sang sản phẩm khác.

Thứ tự ưu tiên là: quy tắc thương hiệu dùng chung → dữ liệu `verified` của sản phẩm → ghi đè chiến dịch → template tham khảo.

## Đầu ra và kiểm tra

Ghi `outputs/<batch-id>/<product-id>/prompts.txt`; mỗi prompt là một đoạn văn trên đúng một dòng và bắt đầu bằng câu ảnh tham chiếu bắt buộc. File chỉ chứa prompt, không tiêu đề, số thứ tự, metadata, code fence hoặc dòng trống.

Tạo `outputs/<batch-id>/batch-summary.yaml` ghi đường dẫn đầu vào, số lượng, claim bị bỏ, placeholder, cảnh báo và ngày tạo. Kiểm tra số dòng, câu mở đầu, dòng trống và sự tách biệt dữ liệu giữa các sản phẩm.
