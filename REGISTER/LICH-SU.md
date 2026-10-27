# REGISTER/LICH-SU.md — Lịch sử dài hạn (append-only)

TRẠNG THÁI: ACTIVE | NGÀY: 2026-10-27
SESSION_REF: arena/81c32a7d-giaidap

Kho chứa các dòng bị đẩy ra khỏi `STATE.md > LỊCH SỬ GẦN NHẤT` khi khối đó đạt trần **8 dòng**
(quy tắc ghi tại `PROTOCOL/resume-protocol.md §5`). Đây là file **append-only**: CHỈ ghi thêm xuống
cuối, KHÔNG sửa / xóa / sắp xếp lại dòng đã lưu. Mỗi dòng ghi rõ ngày bị đẩy kèm NGUYÊN VĂN dòng lịch sử.

## Quy tắc vận hành

1. **Append-only:** đẩy dòng cũ nhất từ `STATE.md` xuống đây bằng cách ghi thêm một dòng mới ở CUỐI
   danh sách bên dưới; không xóa, không sửa dòng cũ. Muốn đính chính thì ghi thêm một dòng mới ở cuối,
   nêu rõ đang đính chính dòng nào.
2. **Không thay `STATE.md`:** `STATE.md` vẫn là điểm hồi sinh; file này chỉ là kho lưu lịch sử dài hạn.
   Khi cần đối chiếu xa hơn 8 dòng, đọc tiếp file này (con trỏ tại `STATE.md > CON TRỎ`).
3. **Cùng commit:** mọi lần đẩy dòng phải đi trong CÙNG COMMIT với lần cập nhật `STATE.md` làm tràn
   lịch sử (`PROTOCOL/resume-protocol.md §5`), để hai file không bao giờ lệch nhau.
4. **POST_MERGE_RECONCILE:** phiên đầu sau một merge ghi PR đã merge vào `LỊCH SỬ GẦN NHẤT`; nếu việc
   đó làm tràn 8 dòng thì đẩy dòng cũ nhất xuống đây (`PROTOCOL/resume-protocol.md §13`).

## CÁC DÒNG ĐÃ ĐẨY (append-only — dòng cũ hơn nằm TRÊN, dòng bị đẩy sau nằm dưới)

- [đẩy 2026-10-27] 2026-10-26 — Khởi tạo khung luật và giao thức GIAIDAP V1 — commit 612a8e6 (PR #1)
- [đẩy 2026-10-27] 2026-10-26 — Vai B kiểm độc lập PR #1 tại head 84ae8b3, ra verdict PASS_WITH_FIXES — RUNS/0000-pr1-verify/B.md (commit 84ae8b3)
- [đẩy 2026-10-27] 2026-10-26 — Vá lần 5: áp sửa theo báo cáo B (thêm LUẬT 15, bắt buộc SHA thật cho LAW_CHECK, map V2) — commit db14795 (PR #1)
- [ghi 2026-10-27] ngày 2026-10-27 — bản ghi sự cố PR #5 (4 dòng liền nhau, cũ→mới)
- [ghi 2026-10-27] #5 merge vào nhánh #4 nên không vào main
- [ghi 2026-10-27] nguyên nhân: base là nhánh, không phải main
- [ghi 2026-10-27] luật chống: BASE_PHAI_LA_MAIN (PROTOCOL/arena-agent-mode.md §4.1) + MAIN_CONTENT_CHECK (PROTOCOL/resume-protocol.md §2)
- [đẩy 2026-10-27] 2026-10-26 — Vá lần 6: lưu nguyên văn B.md, sửa LUẬT 12 theo D1, nâng map lên V3 — commit b1ba697 (PR #1)
- [đẩy 2026-10-27] 2026-10-26 — Vá lần 7: khôi phục LUẬT 08 theo D4, tách 2 trường hash B.md theo D5, nâng map lên V4 — commit 9c4b63a (PR #1)
- [đẩy 2026-10-27] 2026-10-26 — Merge khung luật và giao thức V1 vào main — commit 0a892a4 (PR #1: https://github.com/7roger89-web/GIAIDAP/pull/1)
