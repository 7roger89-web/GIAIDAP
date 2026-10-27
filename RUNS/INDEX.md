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

## Nhật ký bảo trì giao thức (vá tài liệu — KHÔNG mở RUN mới)

Bản vá có thể là vá giao thức/điểm hồi sinh (không phải một câu hỏi A/B/C). Khi đó KHÔNG mở
`RUNS/<id>/` mới và KHÔNG tạo `DECISION.md` mới; thay vào đó ghi 1 dòng vào nhật ký này trong
CÙNG COMMIT với `STATE.md` + `REGISTER` (`PROTOCOL/resume-protocol.md §5`). Bảng RUN ở trên chỉ
liệt kê các RUN thật sự (vòng A/B/C hoặc kiểm luật độc lập).

- 2026-10-27 — Vá 4 lỗ tự mục của cơ chế hồi sinh (A1–A4 chống tự mục, B1–B3 khớp lệnh, C1–C3 dùng được ngay, D1–D3 seed) — PR nối tiếp PR #4, base = nhánh `arena/b960bf99-giaidap`, head = `arena/81c32a7d-giaidap`; file mới duy nhất `REGISTER/LICH-SU.md`. RUN `0000-pr1-verify` vẫn `OPEN`, `NEXT_ONE_ACTION` không đổi. Chi tiết: `STATE.md > LỊCH SỬ GẦN NHẤT`.
- 2026-10-27 — Reconcile PR #6 lên main sau khi #4 và #5 đã merge — PR MỚI từ nhánh `arena/ea8a6620-giaidap` (#6 đã MERGED vào main lúc 06:37:18Z, sau #4 (06:36:32Z), nên không cập nhật được; #5 MERGED 06:36:46Z nhưng có base là nhánh `arena/b960bf99-giaidap` nên nội dung của #5 chưa vào main — PR này đưa lên). Hợp nhất 5 file xung đột; `resume-protocol` §13 POST_MERGE_RECONCILE, §14 MAINTAIN; RESTATE một nguồn (`cach-nghi.md` §1); lệnh hash một dòng trong `kiem.md` §5. RUN `0000-pr1-verify` vẫn `OPEN`, `NEXT_ONE_ACTION` không đổi. Chi tiết: `STATE.md > LỊCH SỬ GẦN NHẤT`.
- 2026-10-27 — Đối chiếu chống mất nội dung cho PR #7 (B1–B8: không mất nội dung #5/#6; kết quả dán vào mô tả PR #7) + bịt 4 luật L1–L4 (`BASE_PHAI_LA_MAIN` ở `arena-agent-mode.md` §4.1; `MAIN_CONTENT_CHECK` vào `RESUME_CHECK` ở `resume-protocol.md` §2; `MAP_SHA256` vào HASH CHUẨN của `STATE.md`; 4 dòng bản ghi sự cố PR #5 nối cuối `REGISTER/LICH-SU.md`) — nhánh `arena/953af346-giaidap` (sinh từ tip nhánh PR #7). RUN `0000-pr1-verify` vẫn `OPEN`, `NEXT_ONE_ACTION` không đổi (Owner merge). Chi tiết: `STATE.md > LỊCH SỬ GẦN NHẤT`.
- 2026-10-27 — `POST_MERGE_RECONCILE` sau merge PR #7 + PR #8 (phiên ĐẦU TIÊN sau merge, `PROTOCOL/resume-protocol.md` §13; nhánh `arena/6ceeb5d2-giaidap` sinh từ `main @ 03ee7be`). Đối chiếu `STATE.md` với `main` thật bằng 2 lệnh chạy THẬT: `gh pr list --state all --json number,state,baseRefName,mergedAt` (đủ 8 PR; #8 MERGED 07:57:21Z và #7 MERGED 07:57:23Z, cả hai `baseRefName=main`) và `sha256sum LAW/00-SUPREME-LAW.md LAW/00-PROVENANCE-MAP.md PROTOCOL/*.md scope-reality-check/SKILL.md` (9 dòng, khớp 9/9 đúng từng ký tự → không DRIFT nội dung). Sửa `STATE.md`: PR_STATE #7/#8 `OPEN`→`MERGED`, `SINH_TỪ_HEAD=03ee7be`, `POST_MERGE_RECONCILE` NEEDED→DONE, `MAIN_CONTENT_CHECK=PASS`, VIỆC ĐANG MỞ bỏ 2 dòng #7/#8, `NEXT_ONE_ACTION` đổi sang giao vai B kiểm diff `84ae8b3..HEAD`, BLOCKER/UNKNOWN cập nhật; đẩy 1 dòng cũ nhất ("2026-10-26 Vá lần 7 — 9c4b63a") xuống `REGISTER/LICH-SU.md` vì LỊCH SỬ GẦN NHẤT đã đủ 8 dòng. KHÔNG sửa file nào trong 9 hash; KHÔNG gỡ `PENDING_VERIFICATION`; KHÔNG nâng MỐC; KHÔNG mở vòng A/B/C; KHÔNG tạo file mới. RUN `0000-pr1-verify` vẫn `OPEN`. Chi tiết: `STATE.md > LỊCH SỬ GẦN NHẤT`.
- 2026-10-27 — POST_MERGE_RECONCILE sau merge PR #9 (phiên ĐẦU TIÊN; SESSION_REF=arena/97dd9264-giaidap, PR_HEAD_SHA=bdf9d1615a9e7343871eb17a3e8ca554a3df3687). `gh pr list --state all --limit 100 --json number,state,baseRefName,mergedAt` + `gh pr view 9 --json state,baseRefName,mergedAt,mergeCommit` chạy thật: #9 MERGED 2026-10-27T10:11:59Z, base=main, mergeCommit=bdf9d161; trước khi mở PR phiên này có 9 PR, 0 OPEN. STATE.md ghi TRƯỚC: #9 OPEN→MERGED, SINH_TỪ_HEAD=bdf9d161, MAIN_CONTENT_CHECK FAIL→PASS; NEEDED→DONE sau ghi lịch sử. Hash đầu phiên khớp 9/9. Đẩy ĐÚNG 1 dòng cũ nhất (Merge khung V1 — 0a892a4/PR #1) xuống CUỐI REGISTER/LICH-SU.md, giữ 8 dòng gần nhất. Đã ghi nguyên văn câu MERGE_OK tại AGENTS.md §3 + arena-agent-mode.md §7 (grep trả đúng 2 dòng); chỉ arena-agent-mode.md đổi trong 9 file hash. MAINTAIN: chạy nguyên văn lệnh hash kiem.md §5 + sha256sum MAP riêng, rà 18 con trỏ file thật/5 thư mục (đều tồn tại); lệnh mẫu A/B/C chưa có RUN 0001 trả exit=1/1/2, báo MUI=c, không tạo RUN để làm xanh. MUI=a,b,c,d và CONFLICT=YES (các câu cấm merge cũ; thứ tự ưu tiên skill) đã báo, không sửa ngoài phạm vi. Tính lại đủ 9 hash sau mọi sửa và ghi STATE.md cuối. PR #10 OPEN, base=main, head=arena/97dd9264-giaidap (https://github.com/7roger89-web/GIAIDAP/pull/10); gh kiểm 2026-10-27T10:24:08Z: tổng 10 PR, đúng 1 OPEN là #10. Commit đầu 582fa615 ghi đủ 5 file; cập nhật số PR thật vào chính dòng này + STATE.md trong commit nối tiếp, không thêm dòng bảo trì thứ hai; tính lại đủ 9 hash và ghi STATE.md cuối. Không merge. RUN 0000-pr1-verify vẫn OPEN; giữ PENDING_VERIFICATION/MỐC=KHUNG, không mở A/B/C, không tạo file mới, không sửa LAW/00, không merge PR phiên này.
