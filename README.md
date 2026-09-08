# Tạo prompt banner theo thương hiệu

Dự án này là một kho dữ liệu và quy trình để chuyển prompt tham khảo thành prompt banner cho một hoặc nhiều sản phẩm. Prompt đầu ra giữ đúng sản phẩm trong ảnh tham chiếu, tuân thủ nhận diện thương hiệu và chỉ sử dụng thông tin thương mại đã được xác minh.

Dự án **không huấn luyện mô hình và không tự tạo ảnh**. Kết quả là các prompt văn bản để đưa vào công cụ tạo ảnh hoặc bàn giao cho designer xử lý tiếp.

## Quy trình tổng quan

```text
Chuẩn bị tài sản → Onboarding thương hiệu → Nhập sản phẩm/USP
→ Chọn prompt tham khảo → Tạo manifest chiến dịch
→ Tạo prompt → Kiểm tra → Đưa prompt vào công cụ tạo ảnh
```

## Người dùng cần chuẩn bị gì?

### 1. Thông tin thương hiệu

Chuẩn bị các thông tin có thể xác minh hoặc phê duyệt:

- Tên chính thức, cách viết, website, thị trường, ngôn ngữ và người duyệt.
- Khách hàng mục tiêu, vấn đề sản phẩm giải quyết, động lực mua, phân khúc giá và tính cách thương hiệu.
- Logo gốc, tốt nhất là SVG/AI/EPS/PDF hoặc PNG nền trong. Không tự vẽ lại, đổi màu hay thay đổi logo gốc.
- Màu thương hiệu (mã màu), font, weight, quy tắc typography và font thay thế.
- Phong cách hình ảnh: ánh sáng, góc máy, nền, chất liệu, đạo cụ, con người, texture, bóng và khoảng trống.
- Giọng văn, tagline, CTA, claim được phép dùng, từ cấm, nội dung pháp lý và quy tắc giá/khuyến mãi.
- Kênh sử dụng, kích thước/tỷ lệ, mục tiêu chiến dịch và số concept mong muốn.

Các thông tin này được lưu trong `brand/`. Khi `onboarding.status` chưa là `complete`, hãy làm theo [instructions/ONBOARDING.md](instructions/ONBOARDING.md). Chỉ chuyển sang `complete` sau khi người dùng duyệt bản tóm tắt thương hiệu.

### 2. Dữ liệu cho từng sản phẩm

Mỗi sản phẩm cần:

- Một hoặc nhiều ảnh gốc đọc rõ, đặt tại `products/<product-id>/images/reference/`.
- Tên sản phẩm, loại sản phẩm và các thông tin mô tả cần thiết.
- USP, thành phần, chứng nhận, giá, khuyến mãi hoặc claim có nguồn cụ thể.
- Nội dung đã duyệt: headline, supporting line và CTA.
- Danh sách nội dung cấm hoặc không được xuất hiện.

Nguồn có thể là tài liệu nội bộ, bao bì, catalog, trang sản phẩm chính thức hoặc gian hàng được ủy quyền. Mỗi dữ kiện phải có trạng thái và nguồn trong `product.yaml`; chỉ dữ liệu `verified` mới được dùng như claim trong prompt. Không suy luận claim từ tên, hình dáng sản phẩm hoặc prompt mẫu.

### 3. Prompt tham khảo và chiến dịch

- Prompt tham khảo dạng `.txt` đặt tại `library/prompt-templates/`.
- Mỗi chiến dịch có một manifest riêng tại `jobs/<batch-id>/manifest.yaml`.
- Dùng chữ thường ASCII dạng kebab-case cho `product-id` và `batch-id`.
- Sao chép `_template` để tạo sản phẩm hoặc manifest mới; không sửa template gốc và không ghi đè output cũ.

## Câu lệnh mẫu để làm việc với AI

Người dùng không cần tự biết phải sửa từng file YAML hay Markdown. Hãy mở dự án này bằng một AI coding agent có quyền đọc và sửa file, sau đó dùng các câu lệnh dưới đây. AI phải đọc `PROJECT.md`, kiểm tra dữ liệu hiện có và hỏi bổ sung những thông tin còn thiếu. Mỗi lượt onboarding chỉ hỏi tối đa năm câu, không hỏi lại dữ liệu đã có và không tự đoán câu trả lời.

### Bắt đầu thiết lập thương hiệu

Nhắn cho AI:

> Bắt đầu thiết lập thương hiệu cho tôi. Hãy đọc PROJECT.md và kiểm tra brand/brand-profile.yaml, sau đó hỏi tôi từng nhóm tối đa 5 câu để thu thập các thông tin còn thiếu. Hãy cho tôi biết cần tải lên logo, font, ảnh tham khảo hoặc tài liệu nào. Sau mỗi câu trả lời đã xác nhận, hãy lưu dữ liệu vào đúng file trong brand/. Không tự suy đoán thông tin chưa biết và chưa đánh dấu onboarding complete cho đến khi tôi duyệt bản tóm tắt cuối cùng.

AI sẽ lần lượt hỗ trợ thu thập:

- Nhận diện và định vị thương hiệu.
- Logo, màu sắc, font và quy tắc sử dụng.
- Phong cách hình ảnh và mẫu tham khảo thích/không thích.
- Giọng văn, headline, CTA, claim, từ cấm và nội dung pháp lý.
- Kênh sử dụng, tỷ lệ ảnh, mục tiêu chiến dịch và mô hình tạo ảnh.

Khi AI yêu cầu tài sản, hãy tải file lên hoặc đặt file vào thư mục được AI hướng dẫn. Nếu chưa có thông tin, trả lời rõ `chưa biết`; AI sẽ lưu là `unknown` hoặc giữ trạng thái chờ, không tự điền.

### Tiếp tục một lần thiết lập chưa hoàn thành

> Tiếp tục onboarding thương hiệu từ dữ liệu hiện có. Hãy kiểm tra những mục còn thiếu hoặc chưa được tôi xác nhận, tóm tắt ngắn phần đã có và chỉ hỏi tối đa 5 câu mới trong lượt này.

### Duyệt và hoàn tất hồ sơ thương hiệu

> Hãy kiểm tra toàn bộ hồ sơ thương hiệu, liệt kê dữ liệu đã xác minh, dữ liệu quan sát được và dữ liệu còn thiếu. Cho tôi bản tóm tắt để duyệt. Chỉ sau khi tôi xác nhận, hãy cập nhật onboarding thành complete và ghi người duyệt cùng ngày cập nhật.

### Thêm một sản phẩm

> Thêm sản phẩm mới vào dự án. Hãy hỏi tôi tối đa 5 câu mỗi lượt về tên sản phẩm, ảnh gốc, loại sản phẩm, USP, nguồn chứng minh, nội dung được duyệt, giá/khuyến mãi và claim bị cấm. Hướng dẫn tôi đặt ảnh vào đúng thư mục, tạo product-id dạng kebab-case và cập nhật product.yaml. Chỉ đánh dấu verified cho dữ liệu tôi xác nhận hoặc có nguồn chính thức; không suy luận USP từ ảnh hay tên sản phẩm.

Nếu đã có sẵn dữ liệu, có thể nhắn cụ thể hơn:

> Thêm sản phẩm [tên sản phẩm]. Tôi sẽ cung cấp ảnh sản phẩm, đường dẫn trang chính thức, USP và nội dung quảng cáo đã duyệt. Hãy kiểm tra dữ liệu còn thiếu, tạo thư mục sản phẩm đúng cấu trúc và hỏi lại những điểm chưa rõ trước khi dùng làm claim.

### Nhập sản phẩm trực tiếp từ website bằng `/usp_product`

Khi có nhiều sản phẩm trên website, người dùng chỉ cần gửi URL trang sản phẩm:

> `/usp_product https://phacheviet.com/products/bot-matcha-novia-xanh`

AI sẽ đọc trang sản phẩm chính thức, trích tên/loại sản phẩm, giá, mô tả, USP được công bố và metadata ảnh; tải ảnh sản phẩm gốc vào `products/<product-id>/images/reference/`; rồi tạo hoặc cập nhật `products/<product-id>/product.yaml` theo đúng schema của dự án.

AI phải báo lại URL đã đọc, product-id, các ảnh đã tải, dữ kiện đã trích và trạng thái từng claim. Nội dung crawl từ website không mặc nhiên là claim `verified`: người dùng cần xác nhận các USP muốn dùng cho banner. AI không được lấy ảnh banner/lifestyle thay cho ảnh sản phẩm, không cắt/chỉnh sửa ảnh gốc, không suy luận USP từ hình ảnh và không tự tạo prompt banner sau bước crawl.

Nếu URL không phải trang sản phẩm cụ thể, ảnh bị chặn hoặc chỉ có thumbnail, AI phải báo rõ và yêu cầu URL/ảnh gốc thay thế. Quy tắc chi tiết nằm tại [skills/usp-product/SKILL.md](skills/usp-product/SKILL.md).

### Kiểm tra dữ liệu trước khi tạo prompt

> Kiểm tra mức độ sẵn sàng của thương hiệu và sản phẩm [product-id] để tạo banner. Không tạo prompt ở bước này. Hãy báo rõ file hoặc dữ liệu còn thiếu, claim nào chưa verified, ảnh nào không đọc được và nội dung nào cần tôi phê duyệt.

### Tạo prompt cho một sản phẩm

> Tạo [số lượng] concept banner cho sản phẩm [product-id], dùng prompt tham khảo [tên file hoặc all], cho kênh [kênh sử dụng] với tỷ lệ [tỷ lệ ảnh]. Hãy đọc toàn bộ quy tắc thương hiệu và dữ liệu sản phẩm đã verified, tạo batch-id mới, không ghi đè output cũ, rồi lưu prompt và batch-summary đúng cấu trúc dự án. Nếu thiếu dữ liệu quan trọng, hãy hỏi tôi trước khi tạo.

### Tạo prompt hàng loạt

> Tạo batch banner mới cho các sản phẩm [danh sách product-id]. Dùng các template [tên file hoặc all], mục tiêu [mục tiêu chiến dịch], kênh [kênh], tỷ lệ [tỷ lệ ảnh] và [số lượng] concept cho mỗi sản phẩm. Hãy kiểm tra đầu vào, tạo manifest mới, chỉ dùng claim verified, giữ dữ liệu từng sản phẩm tách biệt và lưu kết quả cùng batch-summary trong outputs/.

### Yêu cầu AI giải thích kết quả

> Tóm tắt batch [batch-id]: số prompt đã tạo cho từng sản phẩm, template đã dùng, claim bị loại, placeholder và cảnh báo. Chỉ giải thích trong cuộc trò chuyện; không sửa nội dung prompts.txt nếu tôi chưa yêu cầu.

Các câu trong dấu `[]` là phần người dùng thay bằng dữ liệu thực tế. Có thể viết tự nhiên hơn; điều quan trọng là nêu sản phẩm, mục tiêu, kênh, tỷ lệ, số concept và các nội dung chiến dịch đã được duyệt.

## Quy trình sử dụng

### Bước 1 — Thiết lập thương hiệu

1. Đặt logo nguyên bản vào `brand/assets/logos/original/`.
2. Cập nhật `brand/brand-profile.yaml` và các file quy tắc trong `brand/`.
3. Ghi tài sản vào `brand/asset-manifest.yaml` nếu có.
4. Xác nhận bản tóm tắt onboarding trước khi tạo prompt chính thức.

### Bước 2 — Thêm sản phẩm

Sao chép `products/_template/` thành `products/<product-id>/`, đặt ảnh vào thư mục `images/reference/` và hoàn thiện `product.yaml`. Không cắt, chỉnh sửa hoặc thay thế ảnh gốc tham chiếu.

### Bước 3 — Tạo batch

Sao chép `jobs/_template/manifest.yaml` thành `jobs/<batch-id>/manifest.yaml`, sau đó khai báo brand profile, template, sản phẩm bật, ghi đè đã duyệt cho headline/CTA/promotion, tùy chọn placeholder và thư mục output.

Mặc định, hệ thống tạo một prompt cho mỗi cặp **sản phẩm × template** được bật. Với một sản phẩm, chỉ cần bật một sản phẩm trong manifest.

### Bước 4 — Tạo và kiểm tra prompt

Áp dụng [instructions/GENERATE_BANNERS.md](instructions/GENERATE_BANNERS.md) cho từng prompt và [instructions/BATCH_WORKFLOW.md](instructions/BATCH_WORKFLOW.md) cho toàn batch. Mỗi prompt phải bắt đầu bằng câu:

> Sử dụng ảnh sản phẩm làm tham chiếu, cắt 100% sản phẩm trong ảnh tham chiếu ra không thay đổi gì cả.

Prompt phải giữ nguyên sản phẩm, nhãn, logo và bao bì nhìn thấy trong ảnh; chỉ chuyển đổi bối cảnh, bố cục, ánh sáng và nội dung quảng cáo theo dữ liệu đã duyệt. Claim thiếu nguồn phải được bỏ hoặc dùng placeholder khi manifest cho phép.

## Đầu ra là gì?

Mỗi batch tạo cấu trúc:

```text
outputs/<batch-id>/
├── <product-id>/
│   └── prompts.txt
└── batch-summary.yaml
```

- `prompts.txt`: mỗi prompt là một dòng liên tục; không tiêu đề, số thứ tự, metadata, code fence hay dòng trống.
- `batch-summary.yaml`: nguồn đầu vào, số lượng prompt, claim bị bỏ, placeholder, cảnh báo và ngày tạo.

Output chỉ chứa prompt và báo cáo; không đặt ảnh gốc, catalog hay dữ liệu đầu vào trong `outputs/`.

## Sử dụng đầu ra ở đâu?

Mở `outputs/<batch-id>/<product-id>/prompts.txt`, chọn prompt phù hợp rồi dán vào công cụ tạo ảnh mà đội ngũ đang sử dụng. Tải **ảnh sản phẩm gốc** lên cùng công cụ làm ảnh tham chiếu để giữ nguyên bao bì và nhãn. Sau khi sinh ảnh:

1. Kiểm tra sản phẩm có bị vẽ lại, đổi nhãn, sai màu hoặc sai tỷ lệ không.
2. Kiểm tra headline, CTA, giá, khuyến mãi và claim có đúng bản được duyệt không.
3. Thực hiện typography và chỉnh sửa cuối trong công cụ thiết kế nếu mô hình tạo ảnh không render chữ chính xác.
4. Lưu ảnh cuối cùng và thông tin sử dụng ở hệ thống quản lý nội bộ; không đưa ảnh kết quả trở lại làm dữ liệu đầu vào nếu chưa được phê duyệt.

## Vị trí các tệp chính

| Nội dung | Vị trí |
|---|---|
| Hồ sơ và quy tắc thương hiệu | `brand/` |
| Logo gốc | `brand/assets/logos/original/` |
| Ảnh sản phẩm | `products/<product-id>/images/reference/` |
| USP và nguồn sản phẩm | `products/<product-id>/product.yaml` |
| Prompt tham khảo | `library/prompt-templates/` |
| Cấu hình chiến dịch | `jobs/<batch-id>/manifest.yaml` |
| Prompt đầu ra | `outputs/<batch-id>/<product-id>/prompts.txt` |
| Báo cáo batch | `outputs/<batch-id>/batch-summary.yaml` |

## Nguyên tắc an toàn dữ liệu

- Không đưa `.env` hoặc API key lên Git; chỉ dùng `.env.example` làm mẫu.
- Không tự nghĩ ra giá, khuyến mãi, chứng nhận, thành phần, nguồn gốc hoặc cam kết.
- Không ghi đè tài sản gốc, prompt nguồn hoặc output của batch cũ.
- Không xem lịch sử trò chuyện là nguồn dữ liệu lâu dài; mọi thông tin đã xác minh phải được lưu trong `brand/` hoặc `products/`.

Đọc [PROJECT.md](PROJECT.md) để biết quy tắc định tuyến chung, [instructions/ONBOARDING.md](instructions/ONBOARDING.md) để thiết lập thương hiệu, và các hướng dẫn tạo prompt trước mỗi lần chạy.
