# STATE.md — Điểm hồi sinh GIAIDAP

TRẠNG THÁI: ACTIVE | CẬP NHẬT: 2026-10-27T04:24
SESSION_REF: arena/81c32a7d-giaidap (base: arena/b960bf99-giaidap — nối tiếp PR #4)
SINH_TỪ_HEAD: d9074354bc735241c5faf03bc06efd24b72117f1
PROVENANCE_STATUS: PENDING_VERIFICATION
POST_MERGE_RECONCILE: DONE | đối chiếu 2026-10-27 (main = d907435; PR #1 MERGED đã có trong LỊCH SỬ; PR #2/#3/#4/#5 OPEN — xem PR_STATE). Sau bất kỳ merge MỚI, phiên ĐẦU TIÊN phải đổi sang NEEDED rồi chạy `PROTOCOL/resume-protocol.md §13` (đối chiếu STATE.md với main thật, sửa STATE.md TRƯỚC, ghi PR đã merge vào LỊCH SỬ) rồi đổi DONE.
MỐC: KHUNG (hợp lệ: KHUNG | ĐANG_VẬN_HÀNH; ĐANG_VẬN_HÀNH chỉ đạt khi T1–T6 tại PROTOCOL/resume-protocol.md §11 đạt bởi một PHIÊN MỚI thật, kèm ngày + bằng chứng PR/commit)
MỐC — QUY TẮC NÂNG MỐC: nâng MỐC cần Owner xác nhận, kèm trích nguyên văn (comment/quyết định gốc của Owner); không tự nâng MỐC bằng tự chấm T1–T6 của Writer (LUẬT 03, LUẬT 04).
QUY TẮC BẢO TRÌ: Mọi thay đổi trạng thái phải cập nhật STATE.md TRONG CÙNG COMMIT. STATE.md là file ghi CUỐI CÙNG của phiên; nếu sau khi ghi STATE.md còn sửa file khác (LAW/00, PROTOCOL/, SKILL.md) thì PHẢI tính lại MỌI hash ở khối HASH CHUẨN (`PROTOCOL/resume-protocol.md §5`).
Cổng kết phiên là kỷ luật TỰ NGUYỆN — không có CI cưỡng chế.

## HASH CHUẨN
LAW_SHA256: 2cf47ae59380740b500402eb386ae3b63b06d28a4d1b90b1e58a9524784eee52
PROTOCOL_HASHES:
- PROTOCOL/arena-agent-mode.md:ddd30c90e5839e8986f2c2b13bed0e52c5da1a0916c0894171fc8df70ab28fc6
- PROTOCOL/handoff-packet.md:2581949e815044d859722d644623243460a9686883d60cada959c95cf6dccc8d
- PROTOCOL/multi-brain-loop.md:523d15cebb081c099bbfc65ec313591588589a015f63b987b8f6576cc8f6169f
- PROTOCOL/resume-protocol.md:cada9c472487ea75fd084984b6cff0eb5306ce6cbaec0d93439241d7202923b1
SKILL_HASH: 941ca990c137a33f1f18fbee43411e2b35a3635944c531905f974cd276221268
Ghi chú: 6 hash trên là `sha256sum` THẬT của bản SAU vá (tính lại 2026-10-27). LAW/00-SUPREME-LAW.md, PROTOCOL/multi-brain-loop.md, scope-reality-check/SKILL.md không đổi trong vá này; 3 file PROTOCOL còn lại đổi nên đã tính lại và ghi đè.

## PR_STATE (đối chiếu thực tế GitHub, kiểm ngày 2026-10-27)
Mỗi dòng: `PR_STATE: <PR#> <OPEN|MERGED|CLOSED> <ngày kiểm>`. Cập nhật ở bước POST_MERGE_RECONCILE (`PROTOCOL/resume-protocol.md §13`). Nguồn: `gh pr list --state all` + `gh pr view`.
```text
PR_STATE: #1 MERGED 2026-10-27
PR_STATE: #2 OPEN 2026-10-27
PR_STATE: #3 OPEN 2026-10-27
PR_STATE: #4 OPEN 2026-10-27
PR_STATE: #5 OPEN 2026-10-27
```
- #5 là PR của phiên này (vá 4 lỗ tự mục; base `arena/b960bf99-giaidap`, head `arena/81c32a7d-giaidap`); số #5 xác nhận khi mở PR.
- PR #2/#3/#4/#5 đều OPEN; quyết định xử lý (merge/đóng) thuộc Owner, chưa ghi trong main.

## VIỆC ĐANG MỞ
- 0000-pr1-verify — OPEN (verdict gần nhất của B cho head 84ae8b3: PASS_WITH_FIXES; bản V4 chưa kiểm lại) — Giao vai B ở phiên mới kiểm lại diff 84ae8b3..HEAD (LUẬT 12, LUẬT 08, map V4, KB/INDEX.md §MỞ RỘNG, cặp hash B.md)

## NEXT_ONE_ACTION
Nếu là phiên đầu tiên sau một merge: chạy POST_MERGE_RECONCILE (`PROTOCOL/resume-protocol.md §13`) TRƯỚC. Nếu không: giao vai B (ở một phiên mới độc lập, EVIDENCE_MODE=SEALED theo packet kiểm luật) kiểm lại phần thay đổi của vá lần 5–7 từ commit 84ae8b3dfd8271d11af40c49fb34715634af1d0f tới HEAD (LUẬT 12, LUẬT 08, LAW/00-PROVENANCE-MAP.md bản V4, KB/INDEX.md §MỞ RỘNG, cặp field hash trong RUNS/0000-pr1-verify/B.md) trước khi xét gỡ PENDING_VERIFICATION.

## BLOCKER & UNKNOWN
- BLOCKER: Chưa được gỡ PROVENANCE_STATUS=PENDING_VERIFICATION vì vai B chưa kiểm độc lập bản map V4 sau vá lần 5–7 (kiểm ngày 2026-10-27).
- UNKNOWN: Cơ chế claim/lock chưa làm (để PR sau) vì lỗi thiết kế: STATE.md nằm trên nhánh riêng của từng phiên trước khi merge nên hai phiên chạy song song không thấy nhau (kiểm ngày 2026-10-27). Vá này KHÔNG làm claim/lock.
- UNKNOWN: CONTENT_SHA256_B_DECLARED=UNKNOWN trong RUNS/0000-pr1-verify/B.md do B không tự khai (kiểm ngày 2026-10-26).
- UNKNOWN: Chưa có bằng chứng phiên mới độc lập chạy nghiệm thu T1–T6 để nâng MỐC từ KHUNG lên ĐANG_VẬN_HÀNH (kiểm ngày 2026-10-27); nâng MỐC cần Owner xác nhận kèm trích nguyên văn.
- UNKNOWN: PR #2, #3, #4, #5 đang OPEN (đã ghi rõ trong khối PR_STATE ở trên); quyết định xử lý của Owner chưa ghi trong main (kiểm ngày 2026-10-27).

## OWNER_QUYẾT
Bất biến: đủ **5 dòng riêng biệt D1–D5, KHÔNG gộp**; mỗi dòng giữ nhãn `OWNER_SAID=PARAPHRASE` (chưa có comment nguyên văn của Owner trên PR #1).
- D1 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: cho phép sửa riêng LUẬT 12) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap
- D2 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: giữ bảng 15 dòng NEW=1/DERIVED=14, không bỏ LUẬT 15) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap
- D3 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: B.md ghi nguyên văn, CONTENT_SHA256 lấy theo B tự khai, không khai => UNKNOWN) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap
- D4 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: cho phép sửa riêng LUẬT 08, các LUẬT khác không đổi) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap
- D5 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: tách hash B.md thành 2 field riêng, không gộp) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap

## LỊCH SỬ GẦN NHẤT (tối đa 8 dòng; dòng cũ hơn nằm ở REGISTER/LICH-SU.md — append-only)
- 2026-10-27 — Vá 4 lỗ tự mục của cơ chế hồi sinh (A: POST_MERGE_RECONCILE/PR_STATE/ghi-hash/LICH-SU.md; B: đồng bộ lệnh B/C/A; C: câu lệnh đọc skill + TỰ SOI; D: sửa seed BAC/MỐC/OWNER_QUYẾT) — PR #5 (base arena/b960bf99-giaidap, nối tiếp PR #4)
- 2026-10-27 — Khởi tạo cơ chế hồi sinh + bind skill scope-reality-check + vá khuôn RUN 0000 — nhánh arena/b960bf99-giaidap (sinh từ d907435) — PR #4
- 2026-10-27 — Đưa thư mục skill scope-reality-check lên main — commit d907435
- 2026-10-26 — Merge khung luật và giao thức V1 vào main — commit 0a892a4 (PR #1: https://github.com/7roger89-web/GIAIDAP/pull/1)
- 2026-10-26 — Vá lần 7: khôi phục LUẬT 08 theo D4, tách 2 trường hash B.md theo D5, nâng map lên V4 — commit 9c4b63a (PR #1)
- 2026-10-26 — Vá lần 6: lưu nguyên văn B.md, sửa LUẬT 12 theo D1, nâng map lên V3 — commit b1ba697 (PR #1)
- 2026-10-26 — Vá lần 5: áp sửa theo báo cáo B (thêm LUẬT 15, bắt buộc SHA thật cho LAW_CHECK, map V2) — commit db14795 (PR #1)
- 2026-10-26 — Vai B kiểm độc lập PR #1 tại head 84ae8b3, ra verdict PASS_WITH_FIXES — RUNS/0000-pr1-verify/B.md (commit 84ae8b3)

Quy tắc: khi khối này đầy 8 dòng, đẩy đúng 1 dòng CŨ NHẤT xuống `REGISTER/LICH-SU.md` (append-only, KHÔNG xóa), rồi mới thêm dòng mới lên đầu (`PROTOCOL/resume-protocol.md §5`). Dòng "2026-10-26 — Khởi tạo khung luật và giao thức GIAIDAP V1 — commit 612a8e6 (PR #1)" đã được đẩy xuống LICH-SU.md trong vá này.

## CON TRỎ
- Luật & ánh xạ nguồn: LAW/00-SUPREME-LAW.md | LAW/00-PROVENANCE-MAP.md
- Giao thức & skill: PROTOCOL/resume-protocol.md | PROTOCOL/multi-brain-loop.md | scope-reality-check/SKILL.md
- Sổ & mục lục: REGISTER/BAC.md | REGISTER/LICH-SU.md | RUNS/INDEX.md | KB/INDEX.md
