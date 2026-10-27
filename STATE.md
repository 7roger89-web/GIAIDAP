# STATE.md — Điểm hồi sinh GIAIDAP

TRẠNG THÁI: ACTIVE | CẬP NHẬT: 2026-10-27T08:28Z
SESSION_REF: arena/6ceeb5d2-giaidap
SINH_TỪ_HEAD: 03ee7be327258ba0a3aa04f957138556104859bd
PROVENANCE_STATUS: PENDING_VERIFICATION
POST_MERGE_RECONCILE: DONE | NEEDED→DONE ngày 2026-10-27T08:28Z — LẦN RECONCILE SAU MERGE PR #7 + PR #8 (giá trị DONE ghi ở bản trước là của lần reconcile sau PR #6, KHÔNG phải lần này; phiên arena/6ceeb5d2 là PHIÊN ĐẦU TIÊN sau merge #7/#8 nên POST_MERGE_RECONCILE vào phiên là NEEDED). Bằng chứng merge, lệnh THẬT `gh pr list --state all --json number,state,baseRefName,mergedAt` + `gh pr view <n> --json state,baseRefName,mergedAt,mergeCommit` chạy 2026-10-27T08:2xZ: trả đủ 8 PR (đúng 8 PR tại THỜI ĐIỂM reconcile — trước khi phiên này mở PR #9; chạy lại sau khi mở #9 thì lệnh trả 9 PR, dòng thêm là `#9 OPEN base=main`, xem PR_STATE bên dưới); PR #8 state=MERGED, baseRefName=main, mergedAt 2026-10-27T07:57:21Z, mergeCommit 03ee7be (= tip main hiện tại); PR #7 state=MERGED, baseRefName=main, mergedAt 2026-10-27T07:57:23Z, mergeCommit gh=94162e3. Ghi chú trung thực (FACT): #8 merge TRƯỚC #7 2 giây, mà nhánh #8 vốn STACK chứa trọn #7, nên #7 vào main bằng rebase và KHÔNG sinh merge commit mới; `git merge-base --is-ancestor 94162e3 03ee7be` = YES và `git merge-base --is-ancestor 42b14e1 03ee7be` = YES (chạy sau `git fetch --unshallow` vì sandbox clone `--depth=1`). Hệ quả: nội dung #7 (reconcile #6 + đưa #5 lên main) và #8 (B1–B8 + L1–L4) ĐỀU đã nằm trên main @ 03ee7be. (Lần reconcile trước, sau PR #6: #4 MERGED 06:36:32Z → main @ 03639d4; #5 MERGED 06:36:46Z nhưng base=`arena/b960bf99-giaidap` nên không vào main; #6 MERGED 06:37:18Z → main @ 60d6cc0.)
MAIN_CONTENT_CHECK: PASS (kiểm 2026-10-27T08:2xZ, phiên arena/6ceeb5d2 — định nghĩa tại PROTOCOL/resume-protocol.md §2; chạy THẬT sau `git fetch origin main` + `git fetch --unshallow`, KHÔNG tin giá trị ghi sẵn): (a) re-verify PR_STATE bằng `gh pr list --state all --json number,state,baseRefName,mergedAt` → đủ 8 PR tại thời điểm reconcile (8 PR gốc; sau khi phiên này mở PR #9 thì lệnh trả 9 PR), #7 và #8 có state=MERGED và baseRefName="main" (khác bản STATE.md trước reconcile còn ghi OPEN → đúng là DRIFT do merge sau khi ghi); #5 MERGED nhưng base=`arena/b960bf99-giaidap`. (b) khoản khai "đã có trên main" — grep cây `origin/main` thật: `git show origin/main:STATE.md | grep -c 'PR_STATE:'` = 9; `git show origin/main:PROTOCOL/resume-protocol.md | grep -c 'POST_MERGE_RECONCILE'` = 5, `| grep -c 'MAIN_CONTENT_CHECK'` = 3; `git show origin/main:PROTOCOL/arena-agent-mode.md | grep -c 'BASE_PHAI_LA_MAIN'` = 1; `git show origin/main:PROTOCOL/kiem.md | grep -c 'PROTOCOL_HASHES:'` = 2; `git show origin/main:REGISTER/LICH-SU.md | grep -c 'PR #5'` = 1. => khoản khai "#5 KHÔNG trên main" của bản trước nay ĐÃ HẾT HIỆU LỰC (nội dung #5 đã lên main qua #7), các khoản còn lại xác nhận đúng. (c) HASH CHUẨN: `sha256sum` 9 file khớp 9/9 ĐÚNG từng ký tự → không có lệch nội dung; chỗ lệch duy nhất là PR_STATE/HEAD đã sửa ở lần reconcile này → PASS.
MỐC: KHUNG (hợp lệ: KHUNG | ĐANG_VẬN_HÀNH; ĐANG_VẬN_HÀNH chỉ đạt khi T1–T6 tại PROTOCOL/resume-protocol.md §11 đạt bởi một PHIÊN MỚI thật, kèm ngày + bằng chứng PR/commit)
MỐC — QUY TẮC NÂNG MỐC: nâng MỐC cần Owner xác nhận, kèm trích nguyên văn (comment/quyết định gốc của Owner); không tự nâng MỐC bằng tự chấm T1–T6 của Writer (LUẬT 03, LUẬT 04).
QUY TẮC BẢO TRÌ: Mọi thay đổi trạng thái phải cập nhật STATE.md TRONG CÙNG COMMIT. STATE.md là file ghi CUỐI CÙNG của phiên; nếu sau khi ghi STATE.md còn sửa file khác (LAW/00, PROTOCOL/, SKILL.md) thì PHẢI tính lại MỌI hash ở khối HASH CHUẨN (`PROTOCOL/resume-protocol.md §5`).
GHI NHẬN PHIÊN NÀY (2026-10-27T08:28Z→08:3xZ, arena/6ceeb5d2-giaidap): STATE.md là file ghi CUỐI CÙNG của phiên reconcile này — thứ tự ghi thật: STATE.md (reconcile) → REGISTER/LICH-SU.md (nhận 1 dòng đẩy) → RUNS/INDEX.md (1 dòng nhật ký bảo trì) → STATE.md (ghi lại/xác nhận cuối) → commit f4fd2fb → mở PR #9 → commit nối tiếp CHỈ sửa STATE.md để điền số PR #9 (theo đúng tiền lệ đã ghi ở dòng PR #8 và dòng LỊCH SỬ của phiên arena/953af346). Commit đầu đổi 3 file (`git diff --stat`: STATE.md, REGISTER/LICH-SU.md, RUNS/INDEX.md); commit nối tiếp đổi 1 file (STATE.md). KHÔNG file nào trong 9 hash bị sửa ở cả hai commit, nên 9 hash giữ nguyên và đã kiểm lại SAU khi sửa bằng `sha256sum` + lệnh một dòng `PROTOCOL/kiem.md` §5: khớp 9/9.
Cổng kết phiên là kỷ luật TỰ NGUYỆN — không có CI cưỡng chế.

## HASH CHUẨN
Kiểm lại 2026-10-27T08:2xZ (phiên arena/6ceeb5d2) bằng `sha256sum LAW/00-SUPREME-LAW.md LAW/00-PROVENANCE-MAP.md PROTOCOL/*.md scope-reality-check/SKILL.md`: in ra đúng 9 dòng, khớp ĐÚNG từng ký tự với LAW_SHA256 / MAP_SHA256 / 6 dòng PROTOCOL_HASHES / SKILL_HASH bên dưới → KHÔNG có DRIFT nội dung. Phiên reconcile này KHÔNG sửa file nào trong 9 hash nên 9 hash GIỮ NGUYÊN (nếu buộc phải sửa thì phải tính lại MỌI hash theo `PROTOCOL/resume-protocol.md` §5). Lần tính gần nhất trước đó: 2026-10-27T07:23Z. Phạm vi: LAW/00-SUPREME-LAW.md + LAW/00-PROVENANCE-MAP.md + 6 file PROTOCOL/*.md + scope-reality-check/SKILL.md = 9 hash. 8 hash (LAW_SHA256, PROTOCOL_HASHES, SKILL_HASH) tính bằng đúng một dòng lệnh tại `PROTOCOL/kiem.md` §5 (bản SAU mọi sửa file); MAP_SHA256 tính bằng `sha256sum LAW/00-PROVENANCE-MAP.md` (lệnh một dòng ở kiem.md §5 chưa in khóa MAP_SHA256 — đã báo MUI=b, KHÔNG tự sửa kiem.md vì ngoài phạm vi packet).
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

## PR_STATE (đối chiếu GitHub thật, re-verify 2026-10-27T08:3xZ bởi phiên arena/6ceeb5d2 — POST_MERGE_RECONCILE sau merge #7+#8; `gh pr list --state all` trả 9 PR: #1/#4/#5/#6/#7/#8 MERGED, #2/#3 CLOSED, #9 OPEN)
Mỗi dòng: `PR_STATE: <PR#> <OPEN|MERGED|CLOSED> <ngày kiểm>`. Nguồn: `gh pr list --state all` + `gh pr view`.
```text
PR_STATE: #1 MERGED 2026-10-27 (main @ 0a892a4; mergedAt 2026-10-26T10:32:04Z)
PR_STATE: #2 CLOSED 2026-10-27 (không merge; baseRefName=main, mergedAt=null)
PR_STATE: #3 CLOSED 2026-10-27 (không merge; baseRefName=main, mergedAt=null)
PR_STATE: #4 MERGED 2026-10-27 (main @ 03639d4; mergedAt 06:36:32Z)
PR_STATE: #5 MERGED 2026-10-27 (base arena/b960bf99-giaidap — KHÔNG vào main; nội dung đưa lên main bởi PR reconcile #7, #7 đã MERGED nên nội dung #5 NAY ĐÃ trên main)
PR_STATE: #6 MERGED 2026-10-27 (main @ 60d6cc0; mergedAt 06:37:18Z — merge sau #4)
PR_STATE: #7 MERGED 2026-10-27 (main @ 03ee7be; mergedAt 2026-10-27T07:57:23Z; baseRefName=main; mergeCommit gh=94162e3 — vào main bằng rebase vì #8 merge trước 2s và chứa trọn #7, không sinh merge commit mới)
PR_STATE: #8 MERGED 2026-10-27 (main @ 03ee7be; mergedAt 2026-10-27T07:57:21Z; baseRefName=main; mergeCommit gh=03ee7be = tip main hiện tại; L1–L4 + B1–B8)
PR_STATE: #9 OPEN 2026-10-27 (reconcile-sau-merge-7-8: arena/6ceeb5d2-giaidap → main; base=main, MERGEABLE; 3 file đổi STATE.md + REGISTER/LICH-SU.md + RUNS/INDEX.md; số điền bởi commit nối tiếp chỉ-sửa-STATE.md ngay sau khi mở PR — hash 9/9 không đổi)
```

## VIỆC ĐANG MỞ
- 0000-pr1-verify — OPEN (verdict gần nhất của B cho head 84ae8b3: PASS_WITH_FIXES; bản V4 chưa kiểm lại) — Giao vai B ở phiên mới kiểm lại diff 84ae8b3..HEAD (LUẬT 12, LUẬT 08, map V4, KB/INDEX.md §MỞ RỘNG, cặp hash B.md)
- PR #9 (arena/6ceeb5d2-giaidap → main; bản reconcile STATE.md sau merge #7+#8 này) — OPEN, chờ Owner review; Writer không tự merge. https://github.com/7roger89-web/GIAIDAP/pull/9
- (Đã đóng 2026-10-27T08:28Z: 2 dòng "PR #7 ... chờ Owner review" và "PR #8 ... chờ Owner review" — cả hai đã MERGED vào main theo bằng chứng `gh` ở POST_MERGE_RECONCILE. Sau khi mở PR #9, repo có ĐÚNG 1 PR đang OPEN là #9 — kiểm bằng `gh pr list --state all`: count=9, chỉ #9 state=OPEN.)

## NEXT_ONE_ACTION
Giao vai B (phiên mới, EVIDENCE_MODE=SEALED, INPUT cấp tường minh) kiểm lại diff 84ae8b3..HEAD để xét gỡ PROVENANCE_STATUS=PENDING_VERIFICATION.

## BLOCKER & UNKNOWN
- BLOCKER: Chưa được gỡ PROVENANCE_STATUS=PENDING_VERIFICATION vì vai B chưa kiểm độc lập bản map V4 sau vá lần 5–7 (kiểm ngày 2026-10-27). GIỮ NGUYÊN qua lần reconcile này — reconcile sau merge KHÔNG phải kiểm chứng độc lập, không đủ thẩm quyền gỡ (LUẬT 03, LUẬT 04).
- BLOCKER (đã hết hiệu lực 2026-10-27T08:28Z): "chờ Owner review/merge PR #7 và #8" — Owner ĐÃ merge cả hai (07:57:21Z / 07:57:23Z, base=main); việc kế tiếp chuyển sang NEXT_ONE_ACTION ở trên.
- UNKNOWN: Cơ chế claim/lock chưa làm (để PR sau) vì lỗi thiết kế: STATE.md nằm trên nhánh riêng của từng phiên trước khi merge nên hai phiên chạy song song không thấy nhau (kiểm ngày 2026-10-27). PR này KHÔNG làm claim/lock. Lần reconcile này tái xác nhận lỗ đó là THẬT: STATE.md trên main ghi #7/#8 OPEN trong khi GitHub đã MERGED — chỉ có `gh` + cây main là sự thật.
- UNKNOWN: PR #7 được GitHub ghi mergeCommit=94162e3 (không phải một merge commit riêng) vì #8 merge trước và chứa trọn #7; repo không có bản ghi nào giải thích cơ chế rebase/stack này ngoài suy luận từ `git log` + `gh`. Nhãn INFERENCE, chưa được bên độc lập xác nhận.
- UNKNOWN: CONTENT_SHA256_B_DECLARED=UNKNOWN trong RUNS/0000-pr1-verify/B.md do B không tự khai (kiểm ngày 2026-10-26).
- UNKNOWN: Chưa có bằng chứng phiên mới độc lập chạy nghiệm thu T1–T6 để nâng MỐC từ KHUNG lên ĐANG_VẬN_HÀNH (kiểm ngày 2026-10-27); nâng MỐC cần Owner xác nhận kèm trích nguyên văn. Phiên reconcile này KHÔNG nâng MỐC.
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
- 2026-10-27 — POST_MERGE_RECONCILE sau merge PR #7 + PR #8 (phiên ĐẦU TIÊN sau merge, `PROTOCOL/resume-protocol.md` §13): #8 MERGED 07:57:21Z → main @ 03ee7be, #7 MERGED 07:57:23Z (base=main, vào main bằng rebase, mergeCommit gh=94162e3); sửa `STATE.md` (PR_STATE #7/#8 OPEN→MERGED, `SINH_TỪ_HEAD`=03ee7be, POST_MERGE_RECONCILE NEEDED→DONE, MAIN_CONTENT_CHECK=PASS, VIỆC ĐANG MỞ bỏ 2 dòng #7/#8, NEXT_ONE_ACTION đổi sang giao vai B, BLOCKER/UNKNOWN cập nhật); hash 9/9 KHÔNG đổi (không sửa file nào trong 9 hash); GIỮ NGUYÊN PENDING_VERIFICATION, KHÔNG nâng MỐC, KHÔNG mở vòng A/B/C — nhánh arena/6ceeb5d2-giaidap (sinh từ 03ee7be), PR #9 base=main (https://github.com/7roger89-web/GIAIDAP/pull/9); số PR điền ở commit nối tiếp chỉ-sửa-STATE.md ngay sau khi mở PR
- 2026-10-27 — Đối chiếu chống mất nội dung cho PR #7 (B1–B8: KHÔNG mất nội dung #5/#6; kết quả dán vào mô tả PR #7) + bịt L1–L4 (BASE_PHAI_LA_MAIN §4.1 arena-agent-mode; MAIN_CONTENT_CHECK vào RESUME_CHECK §2 resume-protocol; MAP_SHA256 vào HASH CHUẨN; 4 dòng sự cố PR #5 nối cuối LICH-SU.md) — nhánh arena/953af346-giaidap (sinh từ tip nhánh #7 @ 94162e3), PR mới base=main, STACK chứa trọn #7 — PR #8 MERGED 07:57:21Z (main @ 03ee7be)
- 2026-10-27 — Reconcile PR #6 lên main sau khi #4 và #5 đã merge: PR mới từ nhánh arena/ea8a6620-giaidap; đưa nội dung #5 lên main; hợp nhất xung đột; RESTATE một nguồn (cach-nghi §1); lệnh hash một dòng (kiem §5); §13 POST_MERGE / §14 MAINTAIN — PR #7 MERGED 07:57:23Z (base=main, vào main bằng rebase)
- 2026-10-27 — Lắp lớp chứng minh verification-first: thêm PROTOCOL/kiem.md (khối CÁCH CHỨNG MINH 4 dòng, DRY_RUN, MÙI a–d, nhịp MAINTAIN, bản đồ workstream) + PROTOCOL/cach-nghi.md (8 bước nghĩ trước khi làm); packet A/B/C lên 10 trường, RETURN_PACKET thêm 3 trường chứng minh; cold-start thêm cach-nghi — PR #6 MERGED 06:37:18Z (main @ 60d6cc0)
- 2026-10-27 — Vá 4 lỗ tự mục của cơ chế hồi sinh (A: POST_MERGE_RECONCILE/PR_STATE/ghi-hash/LICH-SU.md; B: đồng bộ lệnh B/C/A; C: câu lệnh đọc skill + TỰ SOI; D: sửa seed BAC/MỐC/OWNER_QUYẾT) — PR #5 MERGED 06:36:46Z vào nhánh arena/b960bf99-giaidap (KHÔNG vào main; đưa lên main bởi PR #7 — nay đã MERGED nên nội dung #5 ĐÃ trên main)
- 2026-10-27 — Khởi tạo cơ chế hồi sinh + bind skill scope-reality-check + vá khuôn RUN 0000 — nhánh arena/b960bf99-giaidap (sinh từ d907435) — PR #4 MERGED 06:36:32Z (main @ 03639d4)
- 2026-10-27 — Đưa thư mục skill scope-reality-check lên main — commit d907435
- 2026-10-26 — Merge khung luật và giao thức V1 vào main — commit 0a892a4 (PR #1: https://github.com/7roger89-web/GIAIDAP/pull/1)

Đẩy xuống REGISTER/LICH-SU.md (append-only) khi tràn 8 dòng: 2026-10-26 Vai B kiểm độc lập (84ae8b3); 2026-10-26 Vá lần 5 (db14795); 2026-10-26 Khởi tạo khung V1 (612a8e6, đã đẩy ở vá trước); 2026-10-27 đẩy thêm dòng "2026-10-26 Vá lần 6 (b1ba697)"; 2026-10-27 (phiên reconcile sau merge #7+#8) đẩy thêm dòng "2026-10-26 Vá lần 7 (9c4b63a)".

## CON TRỎ
- Luật & ánh xạ nguồn: LAW/00-SUPREME-LAW.md | LAW/00-PROVENANCE-MAP.md
- Giao thức & skill: PROTOCOL/resume-protocol.md | PROTOCOL/multi-brain-loop.md | PROTOCOL/kiem.md | PROTOCOL/cach-nghi.md | scope-reality-check/SKILL.md
- Sổ & mục lục: REGISTER/BAC.md | REGISTER/LICH-SU.md | RUNS/INDEX.md | KB/INDEX.md
