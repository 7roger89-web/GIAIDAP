# STATE.md — Điểm hồi sinh

TRẠNG THÁI: ACTIVE
CẬP NHẬT: 2026-10-27
SINH_TỪ_HEAD: 0a892a40c5daebe7cde963383f0582c83665313b
LAW_SHA256: 2cf47ae59380740b500402eb386ae3b63b06d28a4d1b90b1e58a9524784eee52
PROVENANCE_STATUS: PENDING_VERIFICATION
SESSION_REF: arena/02c3a44e-giaidap
MODEL: UNKNOWN

File này chỉ ghi trạng thái và con trỏ. Không chứa kết luận mới, không chứa nội dung luật.

## VIỆC ĐANG MỞ

- 0000-pr1-verify — OPEN — giao B kiểm lại diff `84ae8b3..head`

## NEXT_ONE_ACTION

Giao B kiểm lại diff `84ae8b3..head`: LUẬT 12, LUẬT 08, dòng PHẦN_TỰ_CHẾ trong map V4, KB/INDEX §MỞ RỘNG, cặp hash trong B.md

## BLOCKER

Luật nền chưa qua kiểm độc lập (bản V4 chưa được B kiểm; B mới kiểm bản V1 tại head `84ae8b3`).

## UNKNOWN

- B chưa kiểm bản map V2/V3/V4, chưa kiểm LUẬT 12 và LUẬT 08 sau khi sửa; không có kết luận độc lập cho các bản này.
- `CONTENT_SHA256_B_DECLARED` của `RUNS/0000-pr1-verify/B.md`: B không khai, giá trị là `UNKNOWN`.
- Việc B có chấp nhận cách viết mới của LUẬT 12 và LUẬT 08 hay không: chưa có.
- RUN `0000-pr1-verify` thiếu `QUESTION.md`/`A.md`/`C.md` (đây là kiểm luật độc lập, không phải vòng A/B/C).

## LỊCH SỬ GẦN NHẤT

- 2026-10-27 — Thêm cơ chế hồi sinh (`STATE.md`, `RUNS/INDEX.md`, `PROTOCOL/resume-protocol.md`) — nhánh `arena/02c3a44e-giaidap`, PR của phiên này (xem mô tả PR)
- 2026-10-26 — Merge PR #1 (V1 + vá lần 5/6/7, map V4) — commit `0a892a4`

## CON TRỎ

- `LAW/00-SUPREME-LAW.md`
- `PROTOCOL/resume-protocol.md`
- `RUNS/INDEX.md`
- `KB/INDEX.md`

## QUY TẮC BẢO TRÌ

Mọi thay đổi trạng thái phải cập nhật `STATE.md` TRONG CÙNG COMMIT với thay đổi đó. Push xong trước khi merge PR. Không cập nhật thì việc đó coi như không tồn tại với model sau.
