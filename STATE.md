# STATE.md — Điểm hồi sinh GIAIDAP

TRẠNG THÁI: ACTIVE | CẬP NHẬT: 2026-10-27T06:50Z
SESSION_REF: arena/ea8a6620-giaidap
SINH_TỪ_HEAD: 60d6cc0cccb0f1c21010c89b66d1c208390f12cd
PROVENANCE_STATUS: PENDING_VERIFICATION
POST_MERGE_RECONCILE: DONE | NEEDED→DONE ngày 2026-10-27 (phiên reconcile PR #6 lên main). Bằng chứng merge (`gh pr view <n> --json state,mergedAt,mergeCommit,baseRefName`): PR #4 MERGED 06:36:32Z → main @ 03639d4; PR #5 MERGED 06:36:46Z nhưng baseRefName=`arena/b960bf99-giaidap` (KHÔNG phải main) → nội dung #5 chưa vào main; PR #6 MERGED 06:37:18Z → main @ 60d6cc0. Hệ quả: PR reconcile này đưa #5 lên main.
MỐC: KHUNG (hợp lệ: KHUNG | ĐANG_VẬN_HÀNH; ĐANG_VẬN_HÀNH chỉ đạt khi T1–T6 tại PROTOCOL/resume-protocol.md §11 đạt bởi một PHIÊN MỚI thật, kèm ngày + bằng chứng PR/commit)
MỐC — QUY TẮC NÂNG MỐC: nâng MỐC cần Owner xác nhận, kèm trích nguyên văn (comment/quyết định gốc của Owner); không tự nâng MỐC bằng tự chấm T1–T6 của Writer (LUẬT 03, LUẬT 04).
QUY TẮC BẢO TRÌ: Mọi thay đổi trạng thái phải cập nhật STATE.md TRONG CÙNG COMMIT. STATE.md là file ghi CUỐI CÙNG của phiên; nếu sau khi ghi STATE.md còn sửa file khác (LAW/00, PROTOCOL/, SKILL.md) thì PHẢI tính lại MỌI hash ở khối HASH CHUẨN (`PROTOCOL/resume-protocol.md §5`).
Cổng kết phiên là kỷ luật TỰ NGUYỆN — không có CI cưỡng chế.

## HASH CHUẨN
Tính lại 2026-10-27T06:50Z bằng đúng một dòng lệnh tại `PROTOCOL/kiem.md` §5 (bản SAU mọi sửa file). Phạm vi: LAW/00-SUPREME-LAW.md + 6 file PROTOCOL/*.md + scope-reality-check/SKILL.md = 8 hash.
LAW_SHA256: 2cf47ae59380740b500402eb386ae3b63b06d28a4d1b90b1e58a9524784eee52
PROTOCOL_HASHES:
- PROTOCOL/arena-agent-mode.md:ddd30c90e5839e8986f2c2b13bed0e52c5da1a0916c0894171fc8df70ab28fc6
- PROTOCOL/cach-nghi.md:cd49bd3c0427bd842feac0b6f4d5de567cea9dcedac7f2bbc19be855dfc73c40
- PROTOCOL/handoff-packet.md:5215f30ec053b78861c2b11c38ed918b839e57aeb7779c938df37dcf9a850b1c
- PROTOCOL/kiem.md:a3dc66e995950638b19c9210e74bd5801d0ea62fa821626ead674535a71b1464
- PROTOCOL/multi-brain-loop.md:523d15cebb081c099bbfc65ec313591588589a015f63b987b8f6576cc8f6169f
- PROTOCOL/resume-protocol.md:79926433e9ffb94fb74389741eeaad519889af3f9bf7d60641087d8c5dfa4dd1
SKILL_HASH: 941ca990c137a33f1f18fbee43411e2b35a3635944c531905f974cd276221268

## PR_STATE (đối chiếu GitHub thật, kiểm 2026-10-27 06:41Z)
Mỗi dòng: `PR_STATE: <PR#> <OPEN|MERGED|CLOSED> <ngày kiểm>`. Nguồn: `gh pr list --state all` + `gh pr view`.
```text
PR_STATE: #1 MERGED 2026-10-26 (main @ 0a892a4)
PR_STATE: #2 CLOSED 2026-10-27 (không merge)
PR_STATE: #3 CLOSED 2026-10-27 (không merge)
PR_STATE: #4 MERGED 2026-10-27 (main @ 03639d4)
PR_STATE: #5 MERGED 2026-10-27 (base arena/b960bf99-giaidap — KHÔNG vào main; nội dung đưa lên main bởi PR reconcile)
PR_STATE: #6 MERGED 2026-10-27 (main @ 60d6cc0 — merge sau #4)
PR_STATE: PR-RECONCILE (nhánh arena/ea8a6620-giaidap → main) OPEN 2026-10-27 — số PR xác nhận khi mở
```

## VIỆC ĐANG MỞ
- 0000-pr1-verify — OPEN (verdict gần nhất của B cho head 84ae8b3: PASS_WITH_FIXES; bản V4 chưa kiểm lại) — Giao vai B ở phiên mới kiểm lại diff 84ae8b3..HEAD (LUẬT 12, LUẬT 08, map V4, KB/INDEX.md §MỞ RỘNG, cặp hash B.md)
- PR reconcile (nhánh arena/ea8a6620-giaidap → main) — OPEN, chờ Owner review; Writer không tự merge.

## NEXT_ONE_ACTION
Owner review và quyết định merge PR reconcile (nhánh arena/ea8a6620-giaidap → main). Sau khi Owner merge: phiên đầu tiên đổi `POST_MERGE_RECONCILE=NEEDED` và chạy `PROTOCOL/resume-protocol.md` §13 TRƯỚC; rồi mới giao vai B (phiên mới, EVIDENCE_MODE=SEALED) kiểm lại diff 84ae8b3..HEAD trước khi xét gỡ PENDING_VERIFICATION.

## BLOCKER & UNKNOWN
- BLOCKER: Chưa được gỡ PROVENANCE_STATUS=PENDING_VERIFICATION vì vai B chưa kiểm độc lập bản map V4 sau vá lần 5–7 (kiểm ngày 2026-10-27).
- UNKNOWN: Cơ chế claim/lock chưa làm (để PR sau) vì lỗi thiết kế: STATE.md nằm trên nhánh riêng của từng phiên trước khi merge nên hai phiên chạy song song không thấy nhau (kiểm ngày 2026-10-27). PR này KHÔNG làm claim/lock.
- UNKNOWN: CONTENT_SHA256_B_DECLARED=UNKNOWN trong RUNS/0000-pr1-verify/B.md do B không tự khai (kiểm ngày 2026-10-26).
- UNKNOWN: Chưa có bằng chứng phiên mới độc lập chạy nghiệm thu T1–T6 để nâng MỐC từ KHUNG lên ĐANG_VẬN_HÀNH (kiểm ngày 2026-10-27); nâng MỐC cần Owner xác nhận kèm trích nguyên văn.
- UNKNOWN: LAW/00-PROVENANCE-MAP.md KHÔNG nằm trong HASH CHUẨN (STATE chỉ hash LAW/00-SUPREME-LAW.md); chưa có quyết định nào về việc có hash-hóa nó hay không (kiểm 2026-10-27).
- UNKNOWN: Repo không chứa bản ghi nào về "2 dòng DRIFT giả của phiên trước" (tìm `DRIFT` trong repo: chỉ là thuật ngữ giao thức); cách chữa ở `PROTOCOL/kiem.md` §5 làm theo yêu cầu và chưa được kiểm độc lập.
- UNKNOWN: Lý do đóng PR #2 và #3 (CLOSED, không merge) chưa được ghi trong main; quyết định đó thuộc Owner.

## OWNER_QUYẾT
Bất biến: đủ **5 dòng riêng biệt D1–D5, KHÔNG gộp**; mỗi dòng giữ nhãn `OWNER_SAID=PARAPHRASE` (chưa có comment nguyên văn của Owner trên PR #1).
- D1 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: cho phép sửa riêng LUẬT 12) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap
- D2 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: giữ bảng 15 dòng NEW=1/DERIVED=14, không bỏ LUẬT 15) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap
- D3 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: B.md ghi nguyên văn, CONTENT_SHA256 lấy theo B tự khai, không khai => UNKNOWN) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap
- D4 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: cho phép sửa riêng LUẬT 08, các LUẬT khác không đổi) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap
- D5 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: tách hash B.md thành 2 field riêng, không gộp) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap

## LỊCH SỬ GẦN NHẤT (tối đa 8 dòng; dòng cũ hơn nằm ở REGISTER/LICH-SU.md — append-only)
- 2026-10-27 — Reconcile PR #6 lên main sau khi #4 và #5 đã merge: PR mới từ nhánh arena/ea8a6620-giaidap; đưa nội dung #5 lên main; hợp nhất xung đột; RESTATE một nguồn (cach-nghi §1); lệnh hash một dòng (kiem §5); §13 POST_MERGE / §14 MAINTAIN — chờ Owner merge
- 2026-10-27 — Lắp lớp chứng minh verification-first: thêm PROTOCOL/kiem.md (khối CÁCH CHỨNG MINH 4 dòng, DRY_RUN, MÙI a–d, nhịp MAINTAIN, bản đồ workstream) + PROTOCOL/cach-nghi.md (8 bước nghĩ trước khi làm); packet A/B/C lên 10 trường, RETURN_PACKET thêm 3 trường chứng minh; cold-start thêm cach-nghi — PR #6 MERGED 06:37:18Z (main @ 60d6cc0)
- 2026-10-27 — Vá 4 lỗ tự mục của cơ chế hồi sinh (A: POST_MERGE_RECONCILE/PR_STATE/ghi-hash/LICH-SU.md; B: đồng bộ lệnh B/C/A; C: câu lệnh đọc skill + TỰ SOI; D: sửa seed BAC/MỐC/OWNER_QUYẾT) — PR #5 MERGED 06:36:46Z vào nhánh arena/b960bf99-giaidap (KHÔNG vào main; đưa lên main ở dòng trên)
- 2026-10-27 — Khởi tạo cơ chế hồi sinh + bind skill scope-reality-check + vá khuôn RUN 0000 — nhánh arena/b960bf99-giaidap (sinh từ d907435) — PR #4 MERGED 06:36:32Z (main @ 03639d4)
- 2026-10-27 — Đưa thư mục skill scope-reality-check lên main — commit d907435
- 2026-10-26 — Merge khung luật và giao thức V1 vào main — commit 0a892a4 (PR #1: https://github.com/7roger89-web/GIAIDAP/pull/1)
- 2026-10-26 — Vá lần 7: khôi phục LUẬT 08 theo D4, tách 2 trường hash B.md theo D5, nâng map lên V4 — commit 9c4b63a (PR #1)
- 2026-10-26 — Vá lần 6: lưu nguyên văn B.md, sửa LUẬT 12 theo D1, nâng map lên V3 — commit b1ba697 (PR #1)

Đẩy xuống REGISTER/LICH-SU.md (append-only) khi tràn 8 dòng: 2026-10-26 Vai B kiểm độc lập (84ae8b3); 2026-10-26 Vá lần 5 (db14795); 2026-10-26 Khởi tạo khung V1 (612a8e6, đã đẩy ở vá trước).

## CON TRỎ
- Luật & ánh xạ nguồn: LAW/00-SUPREME-LAW.md | LAW/00-PROVENANCE-MAP.md
- Giao thức & skill: PROTOCOL/resume-protocol.md | PROTOCOL/multi-brain-loop.md | PROTOCOL/kiem.md | PROTOCOL/cach-nghi.md | scope-reality-check/SKILL.md
- Sổ & mục lục: REGISTER/BAC.md | REGISTER/LICH-SU.md | RUNS/INDEX.md | KB/INDEX.md
