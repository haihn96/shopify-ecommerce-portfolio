# Checklist nghiệm thu Home Page NOVA

Ngày lập: 2026-10-05. Trạng thái ban đầu: **Chưa thực hiện kiểm tra giao diện**.

Nguồn: [requirements.md](requirements.md), [plan.md](plan.md).

## 1. Cách đánh dấu

- Mỗi mục bắt đầu bằng `[ ]`. Chỉ chuyển sang `[x]` khi kết quả mong đợi đạt và có bằng chứng.
- Trạng thái hợp lệ: **Chưa chạy**, **Đạt**, **Không đạt**, **Chưa kiểm chứng**. Thiếu store, dữ liệu, quyền hoặc thiết bị kiểm tra dùng **Chưa kiểm chứng**, ghi rõ nguyên nhân.
- Checkbox là trạng thái đạt; mục chưa chạy, không đạt hoặc chưa kiểm chứng đều giữ `[ ]`.
- Mỗi lần kiểm tra ghi mã tiêu chí, ngày, theme preview/version, trình duyệt, viewport, kết quả và link bằng chứng. Nếu không đạt, ghi lỗi và task sửa; kiểm tra lại sau khi sửa.
- Bằng chứng có thể là screenshot, video ngắn, log Theme Check, phản hồi giỏ hàng đã loại bỏ thông tin nhạy cảm hoặc ghi nhận thao tác admin. Không lưu email khách hàng thật hoặc dữ liệu đăng nhập.
- Lưu bằng chứng triển khai tại `spec/001-homepage/evidence/` khi thực sự thực hiện; không tạo bằng chứng giả hoặc đánh dấu các mục dưới đây từ việc chỉ viết tài liệu.

Mẫu ghi nhận:

| Mã tiêu chí | Ngày / phiên bản preview | Trình duyệt / viewport | Trạng thái | Bằng chứng / lỗi / lý do chưa kiểm chứng |
|---|---|---|---|---|
| VAL-xx-yy | — | — | Chưa chạy | — |

## 2. Chuẩn bị môi trường

- Theme preview/development store với sản phẩm một biến thể, nhiều biến thể, biến thể khác ảnh/giá, sản phẩm hết hàng và sản phẩm bị gỡ/unpublish.
- Collection có sản phẩm và collection rỗng; menu và trang đích thật; ảnh desktop/mobile có quyền sử dụng.
- Tài khoản/localization bật khi cửa hàng hỗ trợ; nếu không hỗ trợ, kiểm tra hành vi ẩn thay vì giả lập chức năng.
- Test newsletter dùng địa chỉ thử do người kiểm tra kiểm soát. Chỉ kiểm tra đăng ký, không gửi chiến dịch.
- Desktop kiểm tra trình duyệt Chromium và Firefox; mobile kiểm tra Safari iOS hoặc thiết bị/browser tương ứng. Ghi rõ nếu chỉ mô phỏng viewport và chưa xác minh thiết bị thật.

## 3. Nghiệm thu component

### VAL-01 — Header

Liên kết: REQ-01 / TG01.

- [ ] **VAL-01-01:** Mở desktop/mobile, bật/tắt announcement và account trong cấu hình → logo/menu/actions đúng bố cục; mobile có tài khoản/wishlist trong drawer; tùy chọn tắt không để khoảng trống. Bằng chứng: ảnh hai viewport và cấu hình.
- [ ] **VAL-01-02:** Tìm từ có kết quả, từ không có kết quả và nhập rỗng → kết quả/trạng thái rỗng đúng, link sản phẩm hoạt động, không lỗi JavaScript. Bằng chứng: video hoặc ghi nhận cả ba trường hợp.
- [ ] **VAL-01-03:** Thêm sản phẩm rồi mở cart drawer → sản phẩm, số lượng và cart count đúng; đóng/mở bằng bàn phím, Escape, trả focus đúng. Bằng chứng: video thao tác.
- [ ] **VAL-01-04:** Thêm cùng sản phẩm từ hai card, tải lại, xóa rồi tải lại → không trùng, nút đồng bộ, dữ liệu tồn tại/xóa đúng. Bằng chứng: video và trạng thái wishlist.
- [ ] **VAL-01-05:** Chặn storage, dùng dữ liệu lưu bị hỏng và sản phẩm đã gỡ → trang không crash, có trạng thái phù hợp, sản phẩm không còn hợp lệ không có nút mua giả. Bằng chứng: ghi nhận từng trường hợp và console.

### VAL-02 — Hero

Liên kết: REQ-02 / TG02.

- [ ] **VAL-02-01:** Mở 390 và 1440 px → banner đọc rõ, một H1; card trên banner desktop và dưới banner mobile, không méo/cắt nội dung. Bằng chứng: screenshot.
- [ ] **VAL-02-02:** Chọn ảnh mobile riêng, bỏ ảnh mobile và đổi điểm lấy nét → ảnh mobile/fallback đúng, điểm lấy nét áp dụng. Bằng chứng: ảnh trước/sau và admin.
- [ ] **VAL-02-03:** Chọn sản phẩm, đổi swatch với biến thể khác ảnh/giá → dữ liệu card cập nhật đúng Shopify, CTA đúng product/collection. Bằng chứng: dữ liệu nguồn và video.
- [ ] **VAL-02-04:** Bỏ product hoặc CTA link → storefront không có hành động giả; Theme Editor vẫn cho phép cấu hình. Bằng chứng: screenshot hai chế độ.

### VAL-03 — Danh mục cuộn ngang

Liên kết: REQ-03 / TG03.

- [ ] **VAL-03-01:** Thêm/xóa/sắp xếp danh mục, đổi ảnh/nhãn → thứ tự và nội dung phản ánh admin, ảnh tròn không méo. Bằng chứng: admin và storefront.
- [ ] **VAL-03-02:** Vuốt, dùng bàn phím và nút tới hai đầu → mọi danh mục truy cập được, nút đầu/cuối đúng, không tràn ngang trang. Bằng chứng: video.
- [ ] **VAL-03-03:** Thử link riêng, collection fallback và thiếu cả hai → đích đúng, không link giả khi thiếu dữ liệu. Bằng chứng: ghi nhận ba cấu hình.

### VAL-04 — Shop by Mood

Liên kết: REQ-04 / TG04.

- [ ] **VAL-04-01:** Mở desktop/mobile → đủ sáu thẻ; mobile hai cột, tiêu đề dài không đè icon/mũi tên. Bằng chứng: screenshot có một tiêu đề dài.
- [ ] **VAL-04-02:** Đổi icon, màu và link; bấm/chọn bằng bàn phím toàn thẻ → thay đổi đúng và focus rõ, link đúng cấu hình. Bằng chứng: video/admin.
- [ ] **VAL-04-03:** Mở thẻ Under $50 → dùng đích admin đã chọn, không tự sinh bộ lọc hoặc tiền tệ khác. Bằng chứng: URL đích.

### VAL-05 — Editorial Grid

Liên kết: REQ-05 / TG05.

- [ ] **VAL-05-01:** Đối chiếu desktop và mobile → grid magazine có ảnh/nội dung/product card; mobile giữ toàn bộ block theo thứ tự. Bằng chứng: screenshot toàn section.
- [ ] **VAL-05-02:** Reorder, đổi ảnh, thêm nội dung dài và bỏ product → không cắt chữ, không ảnh méo, không hành động giả. Bằng chứng: admin và ảnh các trạng thái.
- [ ] **VAL-05-03:** Dùng swatches/wishlist trên card trong grid → hành vi đồng bộ với Hero/header; link đúng sản phẩm. Bằng chứng: video.

### VAL-06 — One Product, Five Stories

Liên kết: REQ-06 / TG06.

- [ ] **VAL-06-01:** Mở desktop/mobile và kiểm tra từng điểm → đủ Material, Comfort, Design, Sustainability, Delivery; nội dung truy cập bằng chạm/bàn phím. Bằng chứng: video cả năm điểm.
- [ ] **VAL-06-02:** Đổi icon, mô tả dài, ảnh và CTA → cập nhật đúng, không đè/cắt nội dung; CTA đúng đích. Bằng chứng: ảnh/admin.
- [ ] **VAL-06-03:** Resize qua 750/990 px → desktop bố trí quanh ảnh và cạnh Scene; mobile đứng trước Scene, thứ tự focus hợp lý. Bằng chứng: ảnh tại các breakpoint.

### VAL-07 — Shop the Scene

Liên kết: REQ-07 / TG07.

- [ ] **VAL-07-01:** Cấu hình ba hotspot rồi resize → hotspot vẫn bám đúng vật thể vì tọa độ theo toàn ảnh, không sai do crop. Bằng chứng: screenshot mobile/desktop.
- [ ] **VAL-07-02:** Mở từng hotspot bằng chuột/chạm/bàn phím → ảnh/tên/giá/link đúng product; panel không tràn màn hình; Escape/đóng trả focus đúng. Bằng chứng: video.
- [ ] **VAL-07-03:** Gỡ product khỏi hotspot, thay scene và tọa độ → không có hành động mua giả, admin cập nhật được. Bằng chứng: admin và storefront.

### VAL-08 — Horizontal Showcase

Liên kết: REQ-08 / TG08.

- [ ] **VAL-08-01:** Kiểm tra thứ tự trang → component riêng sau Scene, trước Brand Story, có đủ Work/Relax/Travel/Outdoor/Gift Ideas mặc định. Bằng chứng: screenshot.
- [ ] **VAL-08-02:** Đổi số thẻ hiển thị, reorder và cuộn bằng các phương thức → scroll snap hoạt động, mọi thẻ truy cập được, đầu/cuối đúng. Bằng chứng: video/admin.
- [ ] **VAL-08-03:** Cuộn Showcase khi danh mục/gợi ý cũng hiện diện → chỉ dải tương ứng thay đổi, không tràn ngang toàn trang. Bằng chứng: video.

### VAL-09 — Brand Story

Liên kết: REQ-09 / TG09.

- [ ] **VAL-09-01:** Mở mobile/desktop → heading, toàn bộ mô tả, ảnh và CTA đều hiện; desktop ghép với So sánh, mobile đứng trước So sánh. Bằng chứng: screenshot.
- [ ] **VAL-09-02:** Đổi ảnh, màu, nội dung dài và trang đích → nội dung không cắt, tương phản đạt, Our story tới đúng trang. Bằng chứng: admin, ảnh và URL.

### VAL-10 — So sánh sản phẩm

Liên kết: REQ-10 / TG10.

- [ ] **VAL-10-01:** Chọn ba product và badge → Essential/Plus/Pro là nhãn phân hạng, tên/ảnh/giá lấy đúng product; Most popular theo cấu hình. Bằng chứng: screenshot/admin.
- [ ] **VAL-10-02:** Desktop/mobile → ba cột desktop, dải cuộn mobile, cả ba thẻ truy cập được. Bằng chứng: ảnh/video.
- [ ] **VAL-10-03:** Thêm sản phẩm một/nhiều biến thể và hết hàng → dùng đúng luồng chung, không tự thêm biến thể chưa chọn, trạng thái hết hàng đúng. Bằng chứng: video và cart.

### VAL-11 — Social Proof

Liên kết: REQ-11 / TG11.

- [ ] **VAL-11-01:** Nhập/sửa testimonial, số sao, tên, ảnh và link → hiển thị đúng, text dài không cắt, thiếu ảnh không phá bố cục. Bằng chứng: admin và screenshot.
- [ ] **VAL-11-02:** Thay đổi số block rồi nhập điểm/số đánh giá tổng hợp → tổng hợp chỉ theo trường riêng; demo có nhãn, dữ liệu mẫu không thành tuyên bố đánh giá thật. Bằng chứng: ảnh trước/sau.
- [ ] **VAL-11-03:** Cuộn trên mobile → mọi testimonial đều truy cập được bằng chạm/bàn phím. Bằng chứng: video.

### VAL-12 — Sản phẩm gợi ý

Liên kết: REQ-12 / TG12.

- [ ] **VAL-12-01:** Có cả product list và collection → chỉ dùng product list đúng thứ tự. Bằng chứng: admin và storefront.
- [ ] **VAL-12-02:** Xóa product list, có collection → dùng collection; xóa cả hai hoặc collection rỗng → storefront ẩn dải, editor có hướng dẫn, không nút mua giả. Bằng chứng: từng trạng thái.
- [ ] **VAL-12-03:** Cuộn, đổi biến thể và wishlist → card hoạt động đồng bộ, giá/link đúng Shopify; không gọi recommendations API với nguồn thiếu. Bằng chứng: video và Network.

### VAL-13 — Newsletter

Liên kết: REQ-13 / TG13.

- [ ] **VAL-13-01:** Gửi email rỗng/sai → báo lỗi rõ, label/focus hợp lý, không ghi nhận đăng ký thành công. Bằng chứng: ảnh/video.
- [ ] **VAL-13-02:** Gửi email thử hợp lệ → nhận kết quả form Shopify; khi được phép, đối chiếu customer/email trong admin. Bằng chứng: phản hồi đã che email.
- [ ] **VAL-13-03:** Kiểm tra phản hồi lỗi Shopify và thành công → thông báo truy cập được bằng công nghệ hỗ trợ, không hiển thị trạng thái của form khác. Bằng chứng: ghi nhận screen reader và ảnh.
- [ ] **VAL-13-04:** Mở desktop/mobile → vùng nền tối nối Footer, desktop heading/email gọn và mobile xếp dọc; nội dung chỉnh được. Bằng chứng: screenshot/admin.

### VAL-14 — Footer

Liên kết: REQ-14 / TG14.

- [ ] **VAL-14-01:** Mở từng menu/social → đúng đích admin, không link placeholder; copyright đúng cấu hình. Bằng chứng: danh sách link và ảnh.
- [ ] **VAL-14-02:** Với localization bật/tắt → chỉ hiện tùy chọn hợp lệ, thay ngôn ngữ/quốc gia đúng nền tảng, không selector giả. Bằng chứng: hai cấu hình và thao tác.
- [ ] **VAL-14-03:** Đổi color scheme và font theme → Footer/Newsletter đồng bộ, mobile đọc rõ, không lỗi hồi quy. Bằng chứng: ảnh trước/sau.

## 4. Checklist toàn trang

- [ ] **VAL-G01 — Responsive và thiết kế:** Chụp toàn trang tại 375, 390, 768, 1024, 1440 px; kiểm tra đủ 14 nhóm, thứ tự mobile, bố cục ghép desktop, crop ảnh, typography, màu và khoảng cách. Không tràn ngang trang hoặc CTA bị che. Ghi khác biệt do ảnh/font thay thế; không yêu cầu trùng từng pixel.
- [ ] **VAL-G02 — Theme Editor:** Đổi ảnh/màu/font/nội dung, thêm/xóa/reorder block; reload từng section và tạo hai instance carousel → cập nhật đúng, không listener/UI trùng, trạng thái riêng, Header/Footer không lặp.
- [ ] **VAL-G03 — Luồng thương mại chung:** Thử một biến thể, nhiều biến thể, swatch khác giá/ảnh, hết hàng, bấm liên tiếp và lỗi phản hồi giỏ → biến thể đúng, chỉ số lần thêm dự kiến, thông báo chính xác, cart count/drawer đúng; giá theo tiền tệ cửa hàng.
- [ ] **VAL-G04 — Accessibility:** Kiểm tra một H1, heading, alt, tên nút icon, focus, bàn phím cho toàn bộ chức năng, Escape và focus của dialog, thông báo form, tương phản WCAG AA. Dùng kiểm tra tự động kết hợp thao tác bàn phím/screen reader; lưu báo cáo và kết quả thủ công.
- [ ] **VAL-G05 — Hiệu năng và chất lượng:** Chạy Theme Check, đối chiếu baseline trước/sau → không lỗi mới; kiểm tra console/network không lỗi mới, Hero ưu tiên tải, ảnh dưới fold lazy-load, ảnh có kích thước và script không nạp trùng. Lưu log/báo cáo; không dùng điểm Lighthouse duy nhất để kết luận đạt.
- [ ] **VAL-G06 — Hồi quy:** Mở trang product, collection, cart; thử search, Header/Footer và thêm giỏ → các chức năng dùng chung vẫn hoạt động, style Home Page không làm hỏng trang khác. Lưu screenshot và kết quả thao tác.
- [ ] **VAL-G07 — Trình duyệt và dữ liệu thiếu:** Kiểm tra browser nêu ở phần chuẩn bị, sản phẩm gỡ, collection rỗng, ảnh/link thiếu và storage chặn → không crash, có fallback phù hợp, không hành động giả. Ghi rõ phần chỉ mô phỏng hoặc chưa có thiết bị/môi trường để xác minh.

## 5. Definition of Done

### Task group

- Tất cả task details của group được thực hiện.
- Tất cả tiêu chí VAL tương ứng đạt, có bằng chứng.
- Không còn lỗi ngăn sử dụng component; tiêu chí chưa kiểm chứng không được đánh dấu hoàn thành.

### Home Page

- Đủ 14 group đạt; toàn bộ VAL-G01 → VAL-G07 đạt.
- Có theme preview/version và ảnh desktop/mobile để đối chiếu.
- Nội dung/ảnh/font/màu chỉnh được trong admin; dữ liệu thương mại lấy từ Shopify.
- Không có lỗi Theme Check/JavaScript mới hoặc lỗi hồi quy dùng chung.
- Báo cáo ghi rõ tài nguyên thay thế và kết quả kiểm tra, không còn mục bắt buộc chưa kiểm chứng.
- Nghiệm thu dừng ở preview; publish lên cửa hàng là hành động riêng.
