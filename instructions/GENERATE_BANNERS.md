# Tạo prompt banner

## Điều kiện đầu vào

Đọc các file dùng chung trong `brand/` và `products/<product-id>/product.yaml`. Chỉ dùng thông tin đã được phê duyệt hoặc xác minh. Xem template là cảm hứng về bố cục, ánh sáng, typography, đạo cụ và hiệu ứng; không sao chép watermark, logo bên thứ ba hoặc claim không có nguồn. Quy tắc thương hiệu luôn được ưu tiên.

## Chuyển đổi prompt theo ảnh sản phẩm

Mỗi prompt phải bắt đầu chính xác bằng câu: “Sử dụng ảnh sản phẩm làm tham chiếu, cắt 100% sản phẩm trong ảnh tham chiếu ra không thay đổi gì cả.”

Áp dụng cho từng prompt:

1. Xem sản phẩm được tách từ ảnh tham chiếu là nguồn hình ảnh duy nhất.
2. Xóa mọi mô tả của prompt nguồn về hình dáng, cấu trúc, bao bì, nhãn, nắp, vật chứa, chất liệu, màu, texture, hình in, logo, góc nhìn hoặc chi tiết sản phẩm; thay bằng chỉ dẫn dùng nguyên trạng sản phẩm tham chiếu.
3. Không vẽ lại, diễn giải, làm đẹp, thay nhãn, tái dựng hoặc bịa phần bị che. Giữ nguyên toàn bộ phần nhìn thấy, tỷ lệ, phối cảnh, màu, texture, nhãn, logo và bao bì.
4. Giữ bối cảnh, ý tưởng quảng cáo, bố cục, máy ảnh, ánh sáng, môi trường, đạo cụ, hiệu ứng, phân cấp và tỷ lệ khung hình nếu không xung đột với độ trung thực sản phẩm hoặc brand.
5. Thay headline, nội dung phụ, CTA, khuyến mãi và chi tiết thương hiệu bằng dữ liệu `verified`. Prompt mẫu không phải bằng chứng cho claim.
6. Chỉ đổi chi tiết bối cảnh nhỏ để phù hợp phong cách, khách hàng, thị trường, ngôn ngữ hoặc công dụng; không đổi ý tưởng cốt lõi.
7. Nếu thiếu nội dung đã xác minh, bỏ nội dung hoặc dùng placeholder rõ ràng khi manifest cho phép. Không tự nghĩ claim, giá, giảm giá, chứng nhận, thành phần, nguồn gốc hoặc cam kết.
8. Không lặp lại mô tả vật lý sản phẩm đã loại bỏ, kể cả trong negative prompt.

## Thông tin chiến dịch

Xác định ảnh sản phẩm, mục tiêu, khách hàng, kênh, tỷ lệ, headline, USP, giá hoặc khuyến mãi, CTA, nội dung pháp lý, số concept và mô hình ảnh. Không suy luận claim từ ngoại hình.

## Định dạng kết quả

Không ghi đè prompt nguồn. Lưu vào `outputs/<batch-id>/<product-id>/prompts.txt`. Mỗi prompt là một đoạn văn liên tục trên đúng một dòng; không heading, bullet, số thứ tự, metadata, giải thích hoặc code fence. Nhiều prompt cách nhau đúng một ký tự xuống dòng, không có dòng trống. Nối nội dung nhiều dòng của template bằng dấu cách, thu gọn khoảng trắng lặp và bảo đảm mọi dòng bắt đầu bằng câu bắt buộc.
