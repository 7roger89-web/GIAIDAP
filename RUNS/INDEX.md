# RUNS/INDEX.md — Mục lục nhật ký chạy

TRẠNG THÁI: ACTIVE | NGÀY: 2026-10-27

Bảng tra cứu toàn bộ các `RUN` trong `RUNS/`. Dùng đúng khuôn 6 cột như `KB/INDEX.md`.

| RUN_ID | CÂU HỎI (1 dòng) | TRẠNG THÁI | KẾT LUẬN (1 dòng) | NGÀY | FILE |
|---|---|---|---|---|---|
| 0000-pr1-verify | Kiểm chứng độc lập LAW/00-SUPREME-LAW.md và bảng ánh xạ LAW/00-PROVENANCE-MAP.md trên PR #1 so với P2P-OPERATIONS-NOTEBOOK.md thượng nguồn (LOẠI RUN: KIỂM LUẬT ĐỘC LẬP, không phải vòng A/B/C) | OPEN | B ra verdict PASS_WITH_FIXES cho head 84ae8b3 (map V1); đã vá tới V4 nhưng B chưa kiểm lại diff 84ae8b3..HEAD, PROVENANCE_STATUS=PENDING_VERIFICATION | 2026-10-26 | RUNS/0000-pr1-verify/DECISION.md |

## Quy ước 6 cột

- **RUN_ID**: mã thư mục dưới `RUNS/` (`<4 số>-<slug>`). `0000-pr1-verify` là run kiểm luật khởi tạo; các vòng A/B/C chuẩn bắt đầu từ `0001`.
- **CÂU HỎI (1 dòng)**: tóm tắt trung thực câu hỏi trong `QUESTION.md` trên một dòng; nếu không phải vòng A/B/C thường thì ghi kèm `LOẠI RUN`.
- **TRẠNG THÁI**: `OPEN` | `CLOSED` (khớp trường `STATUS` trong `DECISION.md` của RUN đó).
- **KẾT LUẬN (1 dòng)**:
  - Khi `OPEN`: ghi trạng thái kiểm hiện có và việc còn thiếu.
  - Khi `CLOSED`: ghi verdict của C (`C_VERDICT`) và quyết định của Owner (`OWNER_DECISION`). Không tự nâng thành `PASS` khi chưa có bằng chứng tương xứng.
- **NGÀY**: ngày mở hoặc cập nhật kết luận gần nhất của RUN, định dạng `YYYY-MM-DD`.
- **FILE**: đường dẫn tương đối tới `DECISION.md` của RUN (hoặc `QUESTION.md` nếu RUN mới mở chưa có `DECISION.md`).

## Quy tắc bảo trì

1. **Thêm dòng khi mở RUN**: mở thư mục `RUNS/<4 số>-<slug>/` mới => thêm ngay 1 dòng `OPEN` vào bảng này.
2. **Đổi trạng thái khi RUN đóng**: khi `DECISION.md` chuyển sang `STATUS: CLOSED` => cập nhật cột `TRẠNG THÁI` thành `CLOSED` và ghi cột `KẾT LUẬN (1 dòng)`.
3. **Không xóa**: không xóa dòng của RUN cũ, kể cả khi RUN bị `CONTAMINATED=YES` hoặc dừng ở `VERDICT=UNKNOWN`.
4. **Đồng bộ trong cùng commit**: mọi cập nhật `RUNS/INDEX.md` làm đổi việc đang mở phải đi kèm cập nhật `STATE.md` **trong cùng commit** (xem `PROTOCOL/resume-protocol.md` §5).
