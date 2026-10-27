# STATE.md — Điểm hồi sinh GIAIDAP

TRẠNG THÁI: ACTIVE | CẬP NHẬT: 2026-10-27T07:23Z
SESSION_REF: arena/953af346-giaidap
SINH_TỪ_HEAD: 60d6cc0cccb0f1c21010c89b66d1c208390f12cd
PROVENANCE_STATUS: PENDING_VERIFICATION
POST_MERGE_RECONCILE: DONE | NEEDED→DONE ngày 2026-10-27 (phiên reconcile PR #6 lên main). Bằng chứng merge (`gh pr view <n> --json state,mergedAt,mergeCommit,baseRefName`): PR #4 MERGED 06:36:32Z → main @ 03639d4; PR #5 MERGED 06:36:46Z nhưng baseRefName=`arena/b960bf99-giaidap` (KHÔNG phải main) → nội dung #5 chưa vào main; PR #6 MERGED 06:37:18Z → main @ 60d6cc0. Hệ quả: PR reconcile (#7) đưa #5 lên main. Phiên arena/953af346 re-verify toàn bộ PR_STATE bằng `gh` lúc 2026-10-27T07:0xZ: khớp, không có merge mới → vẫn DONE.
MAIN_CONTENT_CHECK: PASS (kiểm 2026-10-27, phiên arena/953af346 — định nghĩa tại PROTOCOL/resume-protocol.md §2): (a) PR_STATE re-verify bằng `gh pr list --state all` khớp từng dòng; (b) khoản khai "đã có trên main": nội dung #6 (`PROTOCOL/kiem.md`, `PROTOCOL/cach-nghi.md`) CÓ trên origin/main (git ls-tree); khoản khai "#5 KHÔNG trên main": xác nhận đúng (origin/main:PROTOCOL/resume-protocol.md không chứa POST_MERGE_RECONCILE; origin/main:STATE.md không chứa PR_STATE).
MỐC: KHUNG (hợp lệ: KHUNG | ĐANG_VẬN_HÀNH; ĐANG_VẬN_HÀNH chỉ đạt khi T1–T6 tại PROTOCOL/resume-protocol.md §11 đạt bởi một PHIÊN MỚI thật, kèm ngày + bằng chứng PR/commit)
MỐC — QUY TẮC NÂNG MỐC: nâng MỐC cần Owner xác nhận, kèm trích nguyên văn (comment/quyết định gốc của Owner); không tự nâng MỐC bằng tự chấm T1–T6 của Writer (LUẬT 03, LUẬT 04).
QUY TẮC BẢO TRÌ: Mọi thay đổi trạng thái phải cập nhật STATE.md TRONG CÙNG COMMIT. STATE.md là file ghi CUỐI CÙNG của phiên; nếu sau khi ghi STATE.md còn sửa file khác (LAW/00, PROTOCOL/, SKILL.md) thì PHẢI tính lại MỌI hash ở khối HASH CHUẨN (`PROTOCOL/resume-protocol.md §5`).
Cổng kết phiên là kỷ luật TỰ NGUYỆN — không có CI cưỡng chế.

## HASH CHUẨN
Tính lại 2026-10-27T07:23Z. Phạm vi: LAW/00-SUPREME-LAW.md + LAW/00-PROVENANCE-MAP.md + 6 file PROTOCOL/*.md + scope-reality-check/SKILL.md = 9 hash. 8 hash (LAW_SHA256, PROTOCOL_HASHES, SKILL_HASH) tính bằng đúng một dòng lệnh tại `PROTOCOL/kiem.md` §5 (bản SAU mọi sửa file); MAP_SHA256 tính bằng `sha256sum LAW/00-PROVENANCE-MAP.md` (lệnh một dòng ở kiem.md §5 chưa in khóa MAP_SHA256 — đã báo MUI=b, KHÔNG tự sửa kiem.md vì ngoài phạm vi packet).
LAW_SHA256: 2cf47ae59380740b500402eb386ae3b63b06d28a4d1b90b1e58a9524784eee52
MAP_SHA256: c15b64d5cb89f6fd9af85290a50bf710b6c06943403b0f9a124df67a73ca2d18
PROTOCOL_HASHES:
- PROTOCOL/arena-agent-mode.md:d104dd4ccb297f1dde12a531631be7bc324944ab8e442acb36526b0beaaf977a
- PROTOCOL/cach-nghi.md:cd49bd3c0427bd842feac0b6f4d5de567cea9dcedac7f2bbc19be855dfc73c40
- PROTOCOL/handoff-packet.md:5215f30ec053b78861c2b11c38ed918b839e57aeb7779c938df37dcf9a850b1c
- PROTOCOL/kiem.md:a3dc66e995950638b19c9210e74bd5801d0ea62fa821626ead674535a71b1464
- PROTOCOL/multi-brain-loop.md:523d15cebb081c099bbfc65ec313591588589a015f63b987b8f6576cc8f6169f
- PROTOCOL/resume-protocol.md:d56f4583c5a774a089e0d7832c066353b2d45bb07f3bb9b41770d40522e6f902
SKILL_HASH: 941ca990c137a33f1f18fbee43411e2b35a3635944c531905f974cd276221268

## PR_STATE (đối chiếu GitHub thật, re-verify 2026-10-27 ~07:0xZ bởi phiên arena/953af346)
Mỗi dòng: `PR_STATE: <PR#> <OPEN|MERGED|CLOSED> <ngày kiểm>`. Nguồn: `gh pr list --state all` + `gh pr view`.
```text
PR_STATE: #1 MERGED 2026-10-27 (main @ 0a892a4; mergedAt 2026-10-26T10:32:04Z)
PR_STATE: #2 CLOSED 2026-10-27 (không merge)
PR_STATE: #3 CLOSED 2026-10-27 (không merge)
PR_STATE: #4 MERGED 2026-10-27 (main @ 03639d4; mergedAt 06:36:32Z)
PR_STATE: #5 MERGED 2026-10-27 (base arena/b960bf99-giaidap — KHÔNG vào main; nội dung đưa lên main bởi PR reconcile #7)
PR_STATE: #6 MERGED 2026-10-27 (main @ 60d6cc0; mergedAt 06:37:18Z — merge sau #4)
PR_STATE: #7 OPEN 2026-10-27 (reconcile: arena/ea8a6620-giaidap → main; base=main, MERGEABLE; B1–B8 đối chiếu chống mất nội dung đã dán vào mô tả; chờ Owner)
PR_STATE: #8 OPEN 2026-10-27 (L1–L4: arena/953af346-giaidap → main; base=main; STACK chứa trọn #7 + L1–L4; số điền bởi commit nối tiếp chỉ-sửa-STATE.md ngay sau khi mở PR — hash 9/9 không đổi)
```

## VIỆC ĐANG MỞ
- 0000-pr1-verify — OPEN (verdict gần nhất của B cho head 84ae8b3: PASS_WITH_FIXES; bản V4 chưa kiểm lại) — Giao vai B ở phiên mới kiểm lại diff 84ae8b3..HEAD (LUẬT 12, LUẬT 08, map V4, KB/INDEX.md §MỞ RỘNG, cặp hash B.md)
- PR #7 (arena/ea8a6620-giaidap → main) — OPEN, chờ Owner review; Writer không tự merge.
- PR #8 (arena/953af346-giaidap → main; L1–L4; STACK: chứa trọn nội dung #7) — OPEN, chờ Owner review; Writer không tự merge.

## NEXT_ONE_ACTION
Owner review và quyết định merge theo MỘT trong hai đường an toàn (luật BASE_PHAI_LA_MAIN, arena-agent-mode.md §4.1): (1) merge PR #8 (chứa trọn #7) rồi đóng #7; hoặc (2) merge #7 trước rồi merge PR #8 ngay sau. Sau khi merge: phiên đầu tiên đổi `POST_MERGE_RECONCILE=NEEDED` và chạy `PROTOCOL/resume-protocol.md` §13 + `MAIN_CONTENT_CHECK` TRƯỚC; rồi mới giao vai B (phiên mới, EVIDENCE_MODE=SEALED) kiểm lại diff 84ae8b3..HEAD trước khi xét gỡ PENDING_VERIFICATION.

## BLOCKER & UNKNOWN
- BLOCKER: Chưa được gỡ PROVENANCE_STATUS=PENDING_VERIFICATION vì vai B chưa kiểm độc lập bản map V4 sau vá lần 5–7 (kiểm ngày 2026-10-27).
- UNKNOWN: Cơ chế claim/lock chưa làm (để PR sau) vì lỗi thiết kế: STATE.md nằm trên nhánh riêng của từng phiên trước khi merge nên hai phiên chạy song song không thấy nhau (kiểm ngày 2026-10-27). PR này KHÔNG làm claim/lock.
- UNKNOWN: CONTENT_SHA256_B_DECLARED=UNKNOWN trong RUNS/0000-pr1-verify/B.md do B không tự khai (kiểm ngày 2026-10-26).
- UNKNOWN: Chưa có bằng chứng phiên mới độc lập chạy nghiệm thu T1–T6 để nâng MỐC từ KHUNG lên ĐANG_VẬN_HÀNH (kiểm ngày 2026-10-27); nâng MỐC cần Owner xác nhận kèm trích nguyên văn.
- ĐÃ GIẢI QUYẾT 2026-10-27 (thay dòng UNKNOWN cũ): LAW/00-PROVENANCE-MAP.md ĐÃ vào HASH CHUẨN với khóa `MAP_SHA256` theo packet L3 của Owner; lệnh một dòng kiem.md §5 chưa in khóa này (MUI=b, chờ Owner cấp việc sửa kiem.md).
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
- 2026-10-27 — Đối chiếu chống mất nội dung cho PR #7 (B1–B8: KHÔNG mất nội dung #5/#6; kết quả dán vào mô tả PR #7) + bịt L1–L4 (BASE_PHAI_LA_MAIN §4.1 arena-agent-mode; MAIN_CONTENT_CHECK vào RESUME_CHECK §2 resume-protocol; MAP_SHA256 vào HASH CHUẨN; 4 dòng sự cố PR #5 nối cuối LICH-SU.md) — nhánh arena/953af346-giaidap (sinh từ tip nhánh #7 @ 94162e3), PR mới base=main, STACK chứa trọn #7 — chờ Owner; số PR điền ở commit nối tiếp ngay sau khi mở PR (một commit chỉ sửa STATE.md, không đụng file có hash)
- 2026-10-27 — Reconcile PR #6 lên main sau khi #4 và #5 đã merge: PR mới từ nhánh arena/ea8a6620-giaidap; đưa nội dung #5 lên main; hợp nhất xung đột; RESTATE một nguồn (cach-nghi §1); lệnh hash một dòng (kiem §5); §13 POST_MERGE / §14 MAINTAIN — chờ Owner merge
- 2026-10-27 — Lắp lớp chứng minh verification-first: thêm PROTOCOL/kiem.md (khối CÁCH CHỨNG MINH 4 dòng, DRY_RUN, MÙI a–d, nhịp MAINTAIN, bản đồ workstream) + PROTOCOL/cach-nghi.md (8 bước nghĩ trước khi làm); packet A/B/C lên 10 trường, RETURN_PACKET thêm 3 trường chứng minh; cold-start thêm cach-nghi — PR #6 MERGED 06:37:18Z (main @ 60d6cc0)
- 2026-10-27 — Vá 4 lỗ tự mục của cơ chế hồi sinh (A: POST_MERGE_RECONCILE/PR_STATE/ghi-hash/LICH-SU.md; B: đồng bộ lệnh B/C/A; C: câu lệnh đọc skill + TỰ SOI; D: sửa seed BAC/MỐC/OWNER_QUYẾT) — PR #5 MERGED 06:36:46Z vào nhánh arena/b960bf99-giaidap (KHÔNG vào main; đưa lên main ở dòng trên)
- 2026-10-27 — Khởi tạo cơ chế hồi sinh + bind skill scope-reality-check + vá khuôn RUN 0000 — nhánh arena/b960bf99-giaidap (sinh từ d907435) — PR #4 MERGED 06:36:32Z (main @ 03639d4)
- 2026-10-27 — Đưa thư mục skill scope-reality-check lên main — commit d907435
- 2026-10-26 — Merge khung luật và giao thức V1 vào main — commit 0a892a4 (PR #1: https://github.com/7roger89-web/GIAIDAP/pull/1)
- 2026-10-26 — Vá lần 7: khôi phục LUẬT 08 theo D4, tách 2 trường hash B.md theo D5, nâng map lên V4 — commit 9c4b63a (PR #1)

Đẩy xuống REGISTER/LICH-SU.md (append-only) khi tràn 8 dòng: 2026-10-26 Vai B kiểm độc lập (84ae8b3); 2026-10-26 Vá lần 5 (db14795); 2026-10-26 Khởi tạo khung V1 (612a8e6, đã đẩy ở vá trước); 2026-10-27 đẩy thêm dòng "2026-10-26 Vá lần 6 (b1ba697)".

## CON TRỎ
- Luật & ánh xạ nguồn: LAW/00-SUPREME-LAW.md | LAW/00-PROVENANCE-MAP.md
- Giao thức & skill: PROTOCOL/resume-protocol.md | PROTOCOL/multi-brain-loop.md | PROTOCOL/kiem.md | PROTOCOL/cach-nghi.md | scope-reality-check/SKILL.md
- Sổ & mục lục: REGISTER/BAC.md | REGISTER/LICH-SU.md | RUNS/INDEX.md | KB/INDEX.md
