# Yêu cầu Home Page NOVA

Ngày lập: 2026-10-05. Nền tảng hiện tại: Shopify Horizon 4.2.0.

## 1. Mục tiêu và phạm vi

Xây dựng Home Page theo ảnh tham chiếu NOVA do người dùng cung cấp, dành cho khách mua sắm trên desktop và mobile. Bản desktop là cơ sở về bố cục và phong cách; bản mobile là cơ sở về cách thu gọn. Giữ đủ 14 nhóm trên mobile, kể cả các nhóm không xuất hiện trong ảnh mobile.

Bộ tài liệu gồm [plan.md](plan.md) và [validations.md](validations.md). Tài liệu này mô tả yêu cầu triển khai, không xác nhận giao diện đã được xây dựng hoặc nghiệm thu.

Phạm vi gồm Home Page, điều chỉnh Header/Footer dùng chung, wishlist trên thiết bị và các product card sử dụng tại Home Page. Trang sản phẩm, collection và checkout dùng hành vi hiện có của Shopify/theme. Không xây ứng dụng bên thứ ba, backend wishlist hoặc đồng bộ tài khoản; không publish theme trong bước nghiệm thu.

## 2. Quy tắc chung

### Kiến trúc và cấu hình

- Dùng Liquid, sections, theme blocks, CSS và JavaScript theo kiến trúc Horizon; tái sử dụng tìm kiếm, giỏ hàng, carousel, hotspots và email signup hiện có khi phù hợp.
- Cấu hình nội dung trang qua `templates/index.json`; Header/Footer qua section groups hiện có.
- Nội dung từng section chỉnh được trong Theme Editor: tiêu đề, mô tả, nhãn CTA, link, ảnh, sản phẩm/collection và color scheme. Các danh sách block hỗ trợ thêm, xóa và sắp xếp.
- Font dùng typography toàn theme với Shopify font picker; không yêu cầu tải font tùy ý. Màu mặc định theo phong cách ảnh, nhưng thay đổi được trong admin.
- Không thay toàn bộ cấu hình theme. CSS/JavaScript mới phải giới hạn phạm vi, hỗ trợ nhiều instance và vòng đời tải lại section trong Theme Editor.
- Dùng các thiết lập và primitive hiện có trước; section/block mới chỉ bổ sung cho bố cục hoặc chức năng chưa đáp ứng.

### Thiết kế và responsive

- Phong cách mặc định: nền trắng/kem, ảnh lifestyle tông ấm, heading serif, nội dung sans-serif, nút bo tròn, thẻ có khoảng cách rõ ràng.
- Dùng ảnh/font tương đương có quyền sử dụng khi thiếu tài nguyên gốc. Không dùng ảnh chụp toàn thiết kế làm giao diện hoặc nguồn ảnh sản phẩm.
- Nội dung storefront mặc định bằng tiếng Anh như ảnh; chuỗi chức năng đi qua hệ thống bản dịch của theme.
- Kiểm tra 375, 390, 768, 1024 và 1440 px. Theo breakpoint Horizon: dưới 750 px là mobile, 750–989 px là tablet, từ 990 px là desktop.
- Thứ tự mobile: REQ-01 → REQ-14. Desktop có thể đặt REQ-06/07 và REQ-09/10 cạnh nhau, nhưng giữ thứ tự đọc và focus.
- Cuộn ngang chỉ nằm trong các dải thẻ; toàn trang không tràn ngang. Không chỉ dùng hover để truy cập nội dung.
- Newsletter và Footer là hai component riêng, nhưng cùng vùng nền tối ở cuối trang; desktop tạo bố cục heading/email/menu như ảnh, mobile xếp dọc.

### Dữ liệu và thương mại

- Tên, giá, ảnh, URL, biến thể và tồn kho lấy từ Shopify. Định dạng giá theo tiền tệ cửa hàng, không hardcode giá trong ảnh.
- Product card dùng chung hỗ trợ ảnh, tên, giá, swatches nếu phù hợp và wishlist. Chọn swatch cập nhật biến thể, ảnh và giá tương ứng.
- Thêm giỏ trực tiếp chỉ khi xác định được biến thể hợp lệ. Sản phẩm nhiều biến thể mở lựa chọn trước khi thêm; không tự chọn một biến thể thay khách hàng.
- Hiển thị trạng thái đang xử lý, thành công, lỗi và hết hàng. Không thêm trùng do bấm liên tiếp; cart drawer/count phản ánh phản hồi Shopify.
- Thiếu sản phẩm hoặc liên kết: không xuất hiện nút mua/CTA giả. Placeholder chỉ phục vụ cấu hình/preview; storefront xử lý bằng cách ẩn hành động không hợp lệ.
- Wishlist lưu product ID/handle trong trình duyệt; chống trùng, xóa được, đồng bộ trạng thái nút giữa các card cùng sản phẩm. Dữ liệu cũ hoặc bị hỏng không làm hỏng trang. Nếu lưu trữ bị chặn, cho phép dùng trong phiên và thông báo không lưu lâu dài.
- Đánh giá/UGC nhập thủ công, không tích hợp ứng dụng. Dữ liệu demo phải được ghi rõ; số liệu tổng hợp không tự suy ra từ các testimonial.
- Danh sách sản phẩm gợi ý do admin chọn; fallback về collection cấu hình. Không cần recommendations API theo hành vi khách hàng.

### Chất lượng

- Một H1 chính tại Hero; heading các section theo thứ bậc. Ảnh có alt phù hợp; ảnh trang trí không tạo mô tả thừa.
- Nút icon có tên truy cập, focus rõ ràng, vùng chạm đủ dùng; tương phản đạt WCAG AA. Drawer/dialog hỗ trợ Escape, giữ focus và trả focus về nút mở.
- Hero ưu tiên tải; ảnh bên dưới lazy-load và có kích thước để hạn chế dịch chuyển bố cục. Không nạp script trùng khi reload section.
- Không phát sinh lỗi Theme Check hoặc lỗi JavaScript mới. Header/Footer/product card dùng chung cần kiểm tra hồi quy trang sản phẩm, collection và giỏ hàng.

## 3. Yêu cầu theo component

### REQ-01 — Header

- Desktop: logo NOVA, menu Shop/Collections/Stories/About, ô tìm kiếm, tài khoản nếu cửa hàng bật, wishlist và giỏ hàng.
- Mobile: logo, nút tìm kiếm, giỏ hàng và menu drawer; tài khoản/wishlist nằm trong drawer.
- Logo và menu lấy từ cấu hình admin. Announcement là tùy chọn bật/tắt, không bắt buộc hiển thị mặc định.
- Tái sử dụng predictive search và cart drawer Horizon. Wishlist mở danh sách trên thiết bị, gồm link sản phẩm, nút xóa và trạng thái rỗng.

### REQ-02 — Hero

- Banner có ảnh, H1 “Objects worth living with.”, mô tả “Thoughtfully designed for everyday life.” và CTA “Explore collection”.
- Thẻ sản phẩm nổi bật có nhãn giới thiệu, ảnh, tên, giá, swatches và liên kết sản phẩm; chọn sản phẩm qua admin.
- Desktop đặt thẻ trên banner; mobile chuyển thẻ xuống dưới banner. Có ảnh mobile và điểm lấy nét riêng, fallback ảnh desktop khi chưa chọn.

### REQ-03 — Danh mục cuộn ngang

- Block gồm ảnh tròn, nhãn và collection/link. Mẫu: Fashion, Beauty, Home, Tech, Kids, Food, Lifestyle, Outdoor, Accessories.
- Nếu không nhập link riêng, dùng URL collection đã chọn. Chỉnh được ảnh và nhãn độc lập.
- Cuộn bằng vuốt, bàn phím và nút khi overflow; nút phản ánh đầu/cuối dải.

### REQ-04 — Shop by Mood

- Heading “What are you looking for?”; sáu thẻ: Something New, Everyday Essentials, A Gift, Under $50, Best Sellers, Something Unexpected.
- Mỗi thẻ có icon/ảnh, màu nhấn, tiêu đề và link; cả thẻ là vùng liên kết.
- Desktop sáu thẻ một hàng khi đủ rộng; tablet tự xuống hàng; mobile hai cột và giữ đủ sáu thẻ.
- “Under $50” là nhãn và link cấu hình, không tự chuyển thành bộ lọc giá hay quy đổi tiền tệ.

### REQ-05 — Editorial Grid

- Grid magazine gồm block ảnh, block nội dung/CTA và product card; mẫu kết hợp câu chuyện ghế, ảnh bàn, giày, lifestyle và tai nghe.
- Desktop dùng tỷ lệ thẻ và hình ảnh theo thiết kế; mobile xếp toàn bộ block theo thứ tự admin, không chỉ giữ thẻ đầu tiên.
- Product card dùng dữ liệu Shopify và chức năng chung, không nhân bản logic biến thể/wishlist.

### REQ-06 — One Product, Five Stories

- Heading, mô tả, CTA chi tiết và ảnh sản phẩm trung tâm.
- Năm điểm mặc định: Material, Comfort, Design, Sustainability, Delivery. Mỗi điểm có icon, tiêu đề và mô tả chỉnh được.
- Desktop bố trí các điểm quanh ảnh; mobile chạm/focus để mở nội dung. Cả năm điểm phải truy cập được, không phụ thuộc hover.

### REQ-07 — Shop the Scene

- Ảnh căn phòng, heading, CTA “Shop the room” và ba hotspot mặc định.
- Mỗi hotspot chọn sản phẩm Shopify, tọa độ X/Y theo phần trăm ảnh; mở ảnh, tên, giá và link sản phẩm.
- Giữ ảnh scene không crop làm sai vị trí hotspot; mobile dùng panel thông tin phù hợp để tránh tràn hoặc che các điểm.
- Tái sử dụng cơ chế hotspot Horizon và kiểm tra hoạt động khi resize.

### REQ-08 — Horizontal Showcase

- Component riêng “Curated for every moment”, đặt sau Shop the Scene và trước Brand Story.
- Mẫu gồm Work, Relax, Travel, Outdoor, Gift Ideas; mỗi thẻ có ảnh, tiêu đề và link.
- Dải cuộn ngang có scroll snap, vuốt, bàn phím, nút điều hướng và số thẻ hiển thị cấu hình theo màn hình.

### REQ-09 — Brand Story

- Heading “Designed for a brighter everyday.”, mô tả, ảnh lifestyle và CTA “Our story”.
- Desktop có vùng nội dung/ảnh; mobile giữ đầy đủ mô tả và CTA trong bố cục gọn.
- Chỉnh được ảnh, màu, nội dung và trang đích. Link tới trang hiện có, không xây thêm trang About trong phạm vi này.

### REQ-10 — So sánh sản phẩm

- Heading “Pick your match.” và ba thẻ mặc định Essential, Plus, Pro.
- Mỗi thẻ chọn một sản phẩm; tên/giá/ảnh từ Shopify, nhãn phân hạng và mô tả đối tượng sử dụng nhập riêng.
- Badge “Most popular” bật theo thẻ; mặc định ở thẻ Plus. Dùng luồng thêm giỏ chung.
- Desktop ba cột, mobile cuộn ngang, truy cập được cả ba lựa chọn.

### REQ-11 — Social Proof

- Heading “People are talking.”, mô tả và các block ảnh/UGC, tên, trích dẫn, số sao, link tùy chọn.
- Điểm tổng hợp và số lượng đánh giá là cấu hình riêng; không dùng số liệu trong ảnh làm dữ liệu thật.
- Có nhãn demo cho nội dung mẫu. Khi không có số liệu thật, không hiển thị tuyên bố tổng hợp như đã được xác thực.
- Desktop grid/dải theo mẫu; mobile giữ toàn bộ nội dung bằng dải cuộn.

### REQ-12 — Sản phẩm gợi ý

- Heading “You might also like these”, danh sách sản phẩm chọn thủ công hoặc collection fallback.
- Thứ tự ưu tiên: danh sách thủ công có sản phẩm → collection đã chọn → ẩn dải sản phẩm nếu không có dữ liệu; Theme Editor hiển thị hướng dẫn cấu hình.
- Product card và điều hướng dùng chức năng chung. Không hứa cá nhân hóa khi dữ liệu là danh sách tuyển chọn.

### REQ-13 — Newsletter

- Heading “STAY CURIOUS.”, mô tả, ô email, label và nút gửi; dùng form customer/email signup Shopify.
- Có kiểm tra email, lỗi phía Shopify, thông báo thành công và trạng thái truy cập được bằng công nghệ hỗ trợ.
- Không tạo dịch vụ gửi email riêng hoặc cam kết tự động gửi chiến dịch. Kết quả đăng ký theo hành vi form Shopify của cửa hàng.

### REQ-14 — Footer

- Menu Shop, About, Help, Track Order; social links, copyright và localization khi cửa hàng hỗ trợ.
- Menu/link và social lấy từ admin. Không hiển thị link giả hoặc chọn ngôn ngữ/quốc gia không hoạt động.
- Đồng bộ màu, typography và khoảng cách với Newsletter; mobile chia nhóm dễ đọc.

## 4. Điều kiện đầu vào và hoàn thành

- Cần theme preview/development store có sản phẩm một/nhiều biến thể, sản phẩm hết hàng, collection, menu và trang đích để nghiệm thu thực tế.
- Cần ảnh thay thế có quyền sử dụng; có thể thay sau trong admin. Không phụ thuộc đường dẫn ảnh tạm trên máy người lập kế hoạch.
- Không cần quyền cửa hàng để viết bộ tài liệu. Thiếu môi trường kiểm tra phải ghi **Chưa kiểm chứng**, không đánh dấu đạt.
- Hoàn thành Home Page khi toàn bộ task và validation đạt, có bằng chứng trên desktop/mobile và không có lỗi hồi quy mới. Xem [validations.md](validations.md) để biết cách đánh dấu.
