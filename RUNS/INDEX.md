# RUNS/INDEX.md — Bảng tra lịch sử chạy

TRẠNG THÁI: ACTIVE | NGÀY: 2026-10-27

Dùng đúng khuôn 6 cột của `KB/INDEX.md`.

| RUN_ID | CÂU HỎI (1 dòng) | TRẠNG THÁI | KẾT LUẬN (1 dòng) | NGÀY | FILE |
|---|---|---|---|---|---|
| 0000-pr1-verify | Kiểm luật độc lập cho PR1 (không phải vòng A/B/C) | OPEN | B kết luận `PASS_WITH_FIXES` cho bản V1 tại head `84ae8b3`; bản V4 chưa qua kiểm lại | 2026-10-26 | RUNS/0000-pr1-verify/DECISION.md |

## Quy ước

- Thêm dòng mới ngay khi mở RUN.
- Đổi trạng thái khi RUN đóng (`OPEN` -> `CLOSED`).
- Không xóa RUN cũ.
- Cột `FILE` ghi đường dẫn tới `DECISION.md` của RUN.
- Cập nhật bảng này trong cùng commit với thay đổi trạng thái của RUN (xem `STATE.md` và `PROTOCOL/resume-protocol.md`).
