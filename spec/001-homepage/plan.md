# Kế hoạch triển khai Home Page NOVA

Ngày lập: 2026-10-05. Trạng thái: **Chưa triển khai giao diện**.

Yêu cầu nguồn: [requirements.md](requirements.md). Nghiệm thu: [validations.md](validations.md).

## 1. Cách sử dụng

- Mỗi task group tương ứng một component. Task chưa hoàn thành dùng `[ ]`; chỉ đổi sang `[x]` khi có kết quả thực hiện.
- Kết thúc group khi mọi task đạt và validation tương ứng có bằng chứng. Không coi việc tạo tài liệu là hoàn thành component.
- Tái sử dụng Horizon trước, bổ sung section/block riêng khi cần; không thay toàn bộ theme hoặc cài ứng dụng bên thứ ba.
- Header/Footer ở section groups; nội dung còn lại cấu hình trong `templates/index.json`. Font theo typography toàn theme; từng section dùng color scheme và ảnh chọn trong admin.
- Desktop ghép Five Stories/Scene và Brand Story/So sánh qua wrapper bố cục Home Page dùng các theme block của component; nếu cần wrapper mới, chỉ đảm nhiệm bố cục. Mobile xếp theo thứ tự REQ-01 → REQ-14; component vẫn cấu hình độc lập.

## 2. Task groups

### TG01 — Header

Yêu cầu: [REQ-01](requirements.md#req-01--header). Nghiệm thu: [VAL-01](validations.md#val-01--header). Phụ thuộc: không có.

- [ ] **TG01-01:** Điều chỉnh header Horizon theo thiết kế; cấu hình logo NOVA, menu, tìm kiếm, tài khoản, giỏ hàng và announcement bật/tắt.
- [ ] **TG01-02:** Thiết lập desktop với ô tìm kiếm/menu; mobile với tìm kiếm, cart, menu drawer và lối vào tài khoản/wishlist trong drawer.
- [ ] **TG01-03:** Giữ predictive search/cart drawer hiện có; tài khoản chỉ hiển thị khi cửa hàng hỗ trợ; kiểm tra focus và Escape.
- [ ] **TG01-04:** Xây wishlist drawer, lưu ID/handle theo thiết bị, thêm/xóa/chống trùng, xử lý dữ liệu cũ, danh sách rỗng và storage bị chặn.
- [ ] **TG01-05:** Xây nút wishlist dùng chung trên product card; đồng bộ các card cùng sản phẩm, cập nhật drawer sau thay đổi, hỗ trợ reload section.
- [ ] **TG01-06:** Xác minh Header trên Home Page, sản phẩm, collection và giỏ hàng; ghi bằng chứng VAL-01.

### TG02 — Hero

Yêu cầu: [REQ-02](requirements.md#req-02--hero). Nghiệm thu: [VAL-02](validations.md#val-02--hero). Phụ thuộc: TG01-05 cho wishlist trên product card.

- [ ] **TG02-01:** Dựng banner với ảnh desktop/mobile, điểm lấy nét, H1, mô tả và CTA; ưu tiên tải ảnh Hero, dự phòng ảnh desktop khi thiếu ảnh mobile.
- [ ] **TG02-02:** Tạo product card dùng chung từ primitive Horizon: sản phẩm, giá, ảnh, swatches, link và nút wishlist.
- [ ] **TG02-03:** Tái sử dụng quick-add/cart: một biến thể thêm trực tiếp, nhiều biến thể mở lựa chọn; trạng thái loading, thành công, lỗi, hết hàng và chống gửi trùng.
- [ ] **TG02-04:** Đặt card trên banner ở desktop, dưới banner ở mobile; admin chọn sản phẩm và nhãn giới thiệu.
- [ ] **TG02-05:** Kiểm tra cập nhật ảnh/giá theo swatch, ảnh responsive và luồng thêm giỏ chung; ghi VAL-02 và VAL-G03.

### TG03 — Danh mục cuộn ngang

Yêu cầu: [REQ-03](requirements.md#req-03--danh-mục-cuộn-ngang). Nghiệm thu: [VAL-03](validations.md#val-03--danh-mục-cuộn-ngang). Phụ thuộc: không có.

- [ ] **TG03-01:** Tạo block ảnh tròn, nhãn, collection/link; preset chín danh mục theo requirements.
- [ ] **TG03-02:** Dùng scroll container/carousel hiện có để hỗ trợ vuốt, bàn phím và nút điều hướng khi overflow.
- [ ] **TG03-03:** Ưu tiên link nhập riêng, nếu trống dùng collection URL; thiếu cả hai thì không tạo liên kết giả.
- [ ] **TG03-04:** Kiểm tra thêm/xóa/sắp xếp, trạng thái đầu/cuối, không overflow toàn trang; ghi VAL-03.

### TG04 — Shop by Mood

Yêu cầu: [REQ-04](requirements.md#req-04--shop-by-mood). Nghiệm thu: [VAL-04](validations.md#val-04--shop-by-mood). Phụ thuộc: không có.

- [ ] **TG04-01:** Tạo heading và block thẻ gồm icon/ảnh, tiêu đề, màu nhấn và link; preset sáu thẻ.
- [ ] **TG04-02:** Desktop sáu thẻ khi đủ rộng, tablet xuống hàng, mobile hai cột và giữ đủ sáu thẻ.
- [ ] **TG04-03:** Làm toàn thẻ thành link, xử lý tiêu đề dài và focus; “Under $50” dẫn tới link admin cấu hình.
- [ ] **TG04-04:** Kiểm tra đổi màu/icon, tất cả CTA và nhãn dài; ghi VAL-04.

### TG05 — Editorial Grid

Yêu cầu: [REQ-05](requirements.md#req-05--editorial-grid). Nghiệm thu: [VAL-05](validations.md#val-05--editorial-grid). Phụ thuộc: TG02-02/03 và TG01-05.

- [ ] **TG05-01:** Tạo block ảnh, nội dung/CTA và product card; preset magazine theo ảnh tham chiếu.
- [ ] **TG05-02:** Dựng tỷ lệ grid desktop; mobile xếp toàn bộ block theo thứ tự admin, không ẩn phần còn lại.
- [ ] **TG05-03:** Gắn product card chung, chọn ảnh/product/link qua admin; xử lý block thiếu dữ liệu.
- [ ] **TG05-04:** Kiểm tra reorder, text dài, swatches/wishlist, crop ảnh và CTA; ghi VAL-05.

### TG06 — One Product, Five Stories

Yêu cầu: [REQ-06](requirements.md#req-06--one-product-five-stories). Nghiệm thu: [VAL-06](validations.md#val-06--one-product-five-stories). Phụ thuộc: không có.

- [ ] **TG06-01:** Dựng heading, mô tả, ảnh trung tâm và CTA chi tiết; chọn ảnh/sản phẩm hoặc trang đích trong admin.
- [ ] **TG06-02:** Tạo năm điểm icon, tiêu đề, mô tả với preset Material, Comfort, Design, Sustainability, Delivery.
- [ ] **TG06-03:** Desktop đặt điểm quanh ảnh; mobile dùng điểm mở nội dung qua chạm/bàn phím, hỗ trợ đóng và focus rõ ràng.
- [ ] **TG06-04:** Cung cấp block component cho wrapper ghép TG06/TG07 trên desktop; mobile vẫn theo thứ tự đọc.
- [ ] **TG06-05:** Kiểm tra cả năm nội dung, CTA, text dài và ảnh resize; ghi VAL-06.

### TG07 — Shop the Scene

Yêu cầu: [REQ-07](requirements.md#req-07--shop-the-scene). Nghiệm thu: [VAL-07](validations.md#val-07--shop-the-scene). Phụ thuộc: TG06-04 cho bố cục ghép và product primitive TG02-02.

- [ ] **TG07-01:** Tái sử dụng cơ chế product hotspots Horizon; thêm ảnh scene, heading và CTA “Shop the room”.
- [ ] **TG07-02:** Preset ba hotspot chọn sản phẩm, tọa độ X/Y theo phần trăm; giữ tỷ lệ toàn ảnh để vị trí không sai do crop.
- [ ] **TG07-03:** Mở thông tin tên/ảnh/giá/link; mobile dùng panel không tràn màn hình; không render hotspot mua hàng khi thiếu product.
- [ ] **TG07-04:** Hoàn thiện wrapper desktop TG06/TG07, stacking mobile và reload trong Theme Editor.
- [ ] **TG07-05:** Kiểm tra tọa độ khi resize, nhiều hotspot, Escape/focus và giá/link; ghi VAL-07.

### TG08 — Horizontal Showcase

Yêu cầu: [REQ-08](requirements.md#req-08--horizontal-showcase). Nghiệm thu: [VAL-08](validations.md#val-08--horizontal-showcase). Phụ thuộc: primitive cuộn của TG03-02.

- [ ] **TG08-01:** Tạo component riêng “Curated for every moment”, đặt sau TG07 và trước TG09.
- [ ] **TG08-02:** Tạo block ảnh, tiêu đề, link; preset Work, Relax, Travel, Outdoor, Gift Ideas.
- [ ] **TG08-03:** Thêm scroll snap, vuốt, bàn phím, nút điều hướng và số thẻ hiển thị theo màn hình; không chia sẻ trạng thái cuộn giữa các instance.
- [ ] **TG08-04:** Kiểm tra đủ thẻ, đầu/cuối, reorder và overflow; ghi VAL-08.

### TG09 — Brand Story

Yêu cầu: [REQ-09](requirements.md#req-09--brand-story). Nghiệm thu: [VAL-09](validations.md#val-09--brand-story). Phụ thuộc: wrapper layout từ TG06-04/TG07-04.

- [ ] **TG09-01:** Tạo heading, mô tả, ảnh lifestyle và CTA “Our story” theo thiết kế.
- [ ] **TG09-02:** Desktop bố trí nội dung/ảnh; mobile giữ đủ mô tả và CTA. Admin chỉnh ảnh, color scheme, nội dung, trang đích.
- [ ] **TG09-03:** Cung cấp component cho wrapper ghép TG09/TG10; giữ thứ tự đọc/focus.
- [ ] **TG09-04:** Kiểm tra link thật, ảnh crop, tương phản và nội dung dài; ghi VAL-09.

### TG10 — So sánh sản phẩm

Yêu cầu: [REQ-10](requirements.md#req-10--so-sánh-sản-phẩm). Nghiệm thu: [VAL-10](validations.md#val-10--so-sánh-sản-phẩm). Phụ thuộc: TG02-02/03, TG01-05 và TG09-03.

- [ ] **TG10-01:** Tạo heading/mô tả và ba block Essential, Plus, Pro; chọn product cho mỗi block.
- [ ] **TG10-02:** Lấy tên/giá/ảnh từ product; nhập nhãn phân hạng, mô tả và badge riêng; preset “Most popular” ở Plus.
- [ ] **TG10-03:** Gắn product card/luồng thêm giỏ chung; desktop ba cột, mobile cuộn ngang.
- [ ] **TG10-04:** Hoàn thiện wrapper TG09/TG10; kiểm tra giá/biến thể/hết hàng và truy cập cả ba thẻ; ghi VAL-10.

### TG11 — Social Proof

Yêu cầu: [REQ-11](requirements.md#req-11--social-proof). Nghiệm thu: [VAL-11](validations.md#val-11--social-proof). Phụ thuộc: primitive cuộn TG03-02.

- [ ] **TG11-01:** Tạo testimonial/UGC block với ảnh, tên, trích dẫn, số sao và link tùy chọn; nhập thủ công trong admin.
- [ ] **TG11-02:** Cấu hình riêng điểm tổng hợp/số đánh giá; bổ sung trạng thái demo và nhãn hiển thị cho dữ liệu mẫu.
- [ ] **TG11-03:** Desktop bố trí grid/dải theo ảnh; mobile cuộn và giữ tất cả testimonial.
- [ ] **TG11-04:** Kiểm tra text dài, thiếu ảnh, nhãn demo và số liệu tổng hợp không tự tính từ block; ghi VAL-11.

### TG12 — Sản phẩm gợi ý

Yêu cầu: [REQ-12](requirements.md#req-12--sản-phẩm-gợi-ý). Nghiệm thu: [VAL-12](validations.md#val-12--sản-phẩm-gợi-ý). Phụ thuộc: TG02-02/03, TG01-05 và primitive cuộn TG03-02.

- [ ] **TG12-01:** Tạo dải “You might also like these” với product list chọn thủ công và collection fallback.
- [ ] **TG12-02:** Thực hiện ưu tiên product list → collection → ẩn dải khi rỗng; Theme Editor có hướng dẫn cấu hình. Không gọi recommendations API khi không có sản phẩm nguồn.
- [ ] **TG12-03:** Gắn product card chung và điều hướng carousel, kiểm tra wishlist/giá/biến thể.
- [ ] **TG12-04:** Kiểm tra ba trạng thái nguồn dữ liệu, sản phẩm bị gỡ và overflow; ghi VAL-12.

### TG13 — Newsletter

Yêu cầu: [REQ-13](requirements.md#req-13--newsletter). Nghiệm thu: [VAL-13](validations.md#val-13--newsletter). Phụ thuộc: không có; phối hợp TG14 về bố cục cuối trang.

- [ ] **TG13-01:** Tái sử dụng form customer/email signup Shopify, label email và thông báo hiện có.
- [ ] **TG13-02:** Dựng “STAY CURIOUS.”, mô tả, trường email và nút gửi; cấu hình nội dung/color scheme trong admin.
- [ ] **TG13-03:** Xử lý email sai/rỗng, phản hồi lỗi và thành công; thông báo được công nghệ hỗ trợ nhận biết.
- [ ] **TG13-04:** Phối hợp Footer thành vùng nền tối: desktop heading/email cùng vùng, mobile xếp dọc; ghi VAL-13 bằng dữ liệu thử có quyền sử dụng.

### TG14 — Footer

Yêu cầu: [REQ-14](requirements.md#req-14--footer). Nghiệm thu: [VAL-14](validations.md#val-14--footer). Phụ thuộc: TG13-02/04 cho giao diện cuối trang.

- [ ] **TG14-01:** Cấu hình menu, social, copyright; chỉ hiển thị liên kết có đích hợp lệ.
- [ ] **TG14-02:** Tái sử dụng localization, chỉ hiện tùy chọn khi cửa hàng có ngôn ngữ/quốc gia tương ứng.
- [ ] **TG14-03:** Đồng bộ nền, typography và khoảng cách với Newsletter; mobile chia nhóm dễ đọc.
- [ ] **TG14-04:** Ghép toàn bộ Home Page theo thứ tự và presets, không ghi đè cấu hình theme không liên quan; xác minh Header/Footer chỉ xuất hiện một lần.
- [ ] **TG14-05:** Chạy Theme Check, kiểm tra responsive, Theme Editor, accessibility và hồi quy; hoàn thiện VAL-14 cùng VAL-G01 → VAL-G07.

## 3. Thứ tự và đầu ra

1. TG01 → TG02: thiết lập Header, wishlist, product card và luồng thêm giỏ chung.
2. TG03 → TG04 → TG05: danh mục, mood, editorial.
3. TG06 → TG07 → TG08: câu chuyện sản phẩm, scene và showcase độc lập.
4. TG09 → TG10 → TG11 → TG12: thương hiệu, so sánh, đánh giá và gợi ý.
5. TG13 → TG14: newsletter/footer, ghép trang và nghiệm thu toàn bộ.

Đầu ra triển khai: Home Page cấu hình được trong admin, preset gần thiết kế, các tương tác dùng dữ liệu Shopify và báo cáo validation có bằng chứng. Không publish theme tự động.

## 4. Điều kiện và rủi ro cần theo dõi

- Cần development store/theme preview và dữ liệu mẫu để kiểm tra giá, biến thể, giỏ hàng, newsletter, account và localization thực tế.
- Thiếu ảnh gốc: dùng ảnh tương đương có quyền sử dụng; ghi tài nguyên thay thế trong báo cáo đối chiếu, không coi khác nội dung ảnh là lỗi pixel.
- Header/Footer và primitive sản phẩm có tác động dùng chung: mọi thay đổi phải qua kiểm tra hồi quy.
- Chức năng chưa kiểm tra được phải ghi **Chưa kiểm chứng**. Không đóng task hoặc group chỉ bằng kiểm tra tĩnh.
