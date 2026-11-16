# CLAUDE.md
<!-- Hướng dẫn cho AI khi làm việc với dự án Hệ thống quản lý cửa hàng Thành Phát.
     Điền từ phần phân tích Use Case (docs/usecase/). Chỗ ghi [chưa quyết định] cần bổ sung sau. -->

## 1. Dự án là gì
- **Tên dự án:** Hệ thống quản lý cửa hàng Thành Phát
- **Mô tả:** Web quản lý bán hàng, công nợ khách thầu, nhập hàng theo lô và kiểm kho cho cửa hàng cơ khí – vật tư xây dựng.
- **Người dùng chính:** 1 chủ, 2 nhân viên bán hàng, 1 thủ kho; ~40–60 lượt khách/ngày.
- **Mục tiêu chính:** Lập phiếu bán nhanh, biết tồn kho chính xác, biết ai nợ bao nhiêu, cuối tháng xem lãi và doanh số nhân viên.

## 2. Phạm vi
- **Phải có (MVP):**
  - Landing page giới thiệu cửa hàng (`frontend/index.html`), bố cục tham khảo ecount.com/vn – chỉ lấy bố cục, không sao chép logo/nội dung
  - Lập phiếu bán (khách lẻ trả ngay / khách thầu ghi nợ), trừ tồn theo FIFO
  - Lập phiếu nhập theo lô (giá nhập riêng từng lô)
  - Tra cứu tồn kho + cảnh báo sắp hết (≤ 10) / tồn lâu (180 ngày)
  - Xem và thu công nợ khách thầu
  - Báo cáo lãi gộp và doanh số theo nhân viên
- **Chưa làm ở giai đoạn này (AI không tự làm khi chưa được yêu cầu):** đặt hàng online, hóa đơn điện tử, kết nối ngân hàng, tính lương thưởng, công nợ phải trả NCC, backend/đồng bộ nhiều máy.
- **Tham khảo:** `docs/usecase/quan-ly-cua-hang-thanh-phat.md` (đặc tả + sơ đồ Use Case)

## 3. Tiêu chí "xong"
- [ ] Mở `frontend/index.html` không có lỗi trong Console
- [ ] Lập phiếu bán vượt tồn bị chặn; lưu phiếu thì tồn giảm đúng
- [ ] Khách thầu mua → công nợ tăng; thu tiền → công nợ giảm đúng
- [ ] Báo cáo lãi tính giá vốn đúng theo FIFO với ví dụ 2 lô giá khác nhau
- [ ] Tải lại trang (F5) dữ liệu vẫn còn

## 4. Công nghệ
- **Giao diện:** HTML + CSS + JavaScript thuần
- **Backend:** không có ở MVP. **Giai đoạn sau sẽ thêm backend** để nhiều máy dùng chung dữ liệu.
- **Cơ sở dữ liệu:** localStorage của trình duyệt; dữ liệu mẫu trong `data/`
- **Lưu ý:** localStorage chỉ nằm trên 1 trình duyệt của 1 máy → ở MVP cả cửa hàng dùng chung 1 máy ở quầy, mỗi người đăng nhập tài khoản riêng. Nên tách phần đọc/ghi dữ liệu ra một tệp riêng để sau này thay bằng backend dễ dàng.
- **Thư viện được phép dùng:** Google Fonts (Be Vietnam Pro). Ngoài ra không dùng thư viện ngoài.

## 5. Cấu trúc thư mục
```
homework_1/
├── frontend/   giao diện (HTML, CSS, JS)
├── data/       dữ liệu mẫu
├── docs/       tài liệu; docs/usecase/ chứa sơ đồ + đặc tả
├── .claude/    cấu hình Claude Code (settings.json, skills/, agents/)
├── .env.example
├── .gitignore
└── CLAUDE.md
```

## 6. Quy ước
- **Ngôn ngữ giao diện:** Tiếng Việt
- **Ngôn ngữ trong code & comment:** tên biến tiếng Anh, comment tiếng Việt
- **Đặt tên:** [chưa quyết định]
- **Định dạng dữ liệu hiển thị:** [chưa quyết định – vd: tiền "1.250.000 đ", ngày dd/mm/yyyy]
- **Thương hiệu/giao diện:** xanh dương đậm `#0b3c7d` + trắng, màu nhấn `#1e6fd9`, font Be Vietnam Pro, giọng thân thiện. Thông tin liên hệ hiện là demo.
- **Commit:** tiếng Việt, ngắn gọn, mỗi commit một việc

## 7. Lệnh hay dùng
- **Chạy dự án:** mở `frontend/index.html` bằng Live Server
- **Chạy test:** chưa có
- **Dựng lại dữ liệu:** không áp dụng

## 8. Cách làm việc với tôi
- Luôn theo 4 bước: **Explore → Plan → Code → Verify**.
- Trước khi sửa code: đưa kế hoạch từng bước (bước nào sửa tệp nào, kiểm chứng bằng cách nào) và **chờ tôi duyệt**.
- Làm **từng bước một**, xong một bước thì dừng lại báo cáo đã đụng vào tệp nào.
- Báo "xong" phải kèm **bằng chứng chạy thật** (kết quả test, lỗi Console, ảnh chụp), không chỉ nói "đã sửa xong".
- Chưa rõ yêu cầu thì **hỏi lại**, không tự đoán.
- Giải thích cho tôi bằng tiếng Việt, ngôn ngữ đơn giản. Trình độ của tôi: mới học code, có nền marketing/phân tích dữ liệu.

## 9. Không được làm
- Không xóa dữ liệu hoặc tệp khi chưa hỏi.
- Không cài thêm package khi chưa hỏi.
- Không sửa tệp ngoài phạm vi việc đang làm.
- Không đưa mật khẩu, API key vào code (dùng `.env`, đã có trong `.gitignore`).
- Không đổi quy tắc nghiệp vụ BR01–BR08 trong đặc tả khi chưa hỏi.

## 10. Trạng thái hiện tại
- **Đã xong:** phân tích + sơ đồ + đặc tả Use Case; cấu trúc thư mục; bản đầu landing page `frontend/index.html` (đã kiểm ở 375px và 1280px, không lỗi Console).
- **Đang làm:** chờ chủ dự án feedback landing page.
- **Việc tiếp theo:** sửa landing theo feedback; trả lời 7 câu hỏi mở trong đặc tả; dựng màn hình đăng nhập + quản lý.
