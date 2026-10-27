# STATE.md — Điểm hồi sinh GIAIDAP

TRẠNG THÁI: ACTIVE | CẬP NHẬT: 2026-10-27T10:20:33Z
SESSION_REF: arena/97dd9264-giaidap
SINH_TỪ_HEAD: bdf9d1615a9e7343871eb17a3e8ca554a3df3687
PROVENANCE_STATUS: PENDING_VERIFICATION
POST_MERGE_RECONCILE: DONE | NEEDED→DONE ngày 2026-10-27T10:16:48Z — LẦN RECONCILE SAU MERGE PR #9, không dùng lại DONE của #7/#8. Phiên arena/97dd9264-giaidap là PHIÊN ĐẦU TIÊN sau #9; đã sửa STATE.md TRƯỚC mọi file khác lúc 2026-10-27T10:16:09Z, rồi đẩy đúng 1 dòng lịch sử/ghi nhật ký và hoàn tất §13 trước việc MERGE_OK. Bằng chứng thật: `gh pr list --state all --limit 100 --json number,state,baseRefName,mergedAt` trả 9 PR, 0 OPEN TRƯỚC khi mở PR phiên này; `gh pr view 9 --json state,baseRefName,mergedAt,mergeCommit` trả state=MERGED, baseRefName=main, mergedAt=2026-10-27T10:11:59Z, mergeCommit=bdf9d1615a9e7343871eb17a3e8ca554a3df3687 (= origin/main đã fetch).
MAIN_CONTENT_CHECK: PASS (đối chiếu nguồn thật 2026-10-27T10:14:19Z; phạm vi main @ bdf9d1615a9e7343871eb17a3e8ca554a3df3687). Vào phiên: FAIL + STATE_TRUST=DRIFT vì #9 còn OPEN, SINH_TỪ_HEAD=03ee7be và DONE thuộc lần cũ; PR_STATE/HEAD nay đã sửa theo `gh`. (a) Danh sách GitHub trước khi mở PR phiên này: 9 PR; #1/#4/#5/#6/#7/#8/#9 MERGED, #2/#3 CLOSED; #5 có base=arena/b960bf99-giaidap, các PR còn lại base=main. (b) `git show origin/main:<file> | grep -n <chuỗi>` xác nhận các khoản đã trên main: nội dung #5/#6/#7/#8 qua POST_MERGE_RECONCILE + MAIN_CONTENT_CHECK + §14 MAINTAIN (resume-protocol), BASE_PHAI_LA_MAIN (arena-agent-mode), PROTOCOL_HASHES (kiem), MAP_SHA256 (STATE), bản ghi sự cố #5 (LICH-SU); nội dung #9 qua dòng reconcile #7/#8 (RUNS/INDEX) và dòng đẩy Vá lần 7 (LICH-SU). (c) ĐẦU phiên HEAD=origin/main và khối hash cũ được kiểm bằng `sha256sum LAW/00-SUPREME-LAW.md LAW/00-PROVENANCE-MAP.md PROTOCOL/*.md scope-reality-check/SKILL.md` + so khối HASH CHUẨN lúc vào phiên: 9/9 OK. Khối HASH CHUẨN bên dưới nay mô tả bản SAU sửa trên nhánh PR: chỉ hash arena-agent-mode.md đổi; không khai quy tắc MERGE_OK đã ở main. `git merge-base --is-ancestor 03ee7be327258ba0a3aa04f957138556104859bd HEAD` exit=0. MERGE_OK CHƯA có trên main (kiểm AGENTS.md và arena-agent-mode.md bằng awk: mỗi file count=0); việc ghi quy tắc theo packet là thay đổi của nhánh phiên này, không phải nội dung đã merge.
STATE_TRUST: OK (sau reconcile; đầu phiên DRIFT đã báo). RUN 0000-pr1-verify vẫn OPEN, NEXT của RUN vẫn giao B kiểm độc lập, khớp RUNS/INDEX.md:9 và RUNS/0000-pr1-verify/DECISION.md:2,149. NEXT_ONE_ACTION của PHIÊN này theo packet bounded được cấp, không thay NEXT của RUN; số PR sẽ lấy từ gh sau khi mở, không đoán.
MỐC: KHUNG (hợp lệ: KHUNG | ĐANG_VẬN_HÀNH; ĐANG_VẬN_HÀNH chỉ đạt khi T1–T6 tại PROTOCOL/resume-protocol.md §11 đạt bởi một PHIÊN MỚI thật, kèm ngày + bằng chứng PR/commit)
MỐC — QUY TẮC NÂNG MỐC: nâng MỐC cần Owner xác nhận, kèm trích nguyên văn (comment/quyết định gốc của Owner); không tự nâng MỐC bằng tự chấm T1–T6 của Writer (LUẬT 03, LUẬT 04).
QUY TẮC BẢO TRÌ: Mọi thay đổi trạng thái phải cập nhật STATE.md TRONG CÙNG COMMIT. STATE.md là file ghi CUỐI CÙNG của phiên; nếu sau khi ghi STATE.md còn sửa file khác (LAW/00, PROTOCOL/, SKILL.md) thì PHẢI tính lại MỌI hash ở khối HASH CHUẨN (`PROTOCOL/resume-protocol.md §5`).
GHI NHẬN PHIÊN NÀY (2026-10-27T10:20:33Z, arena/97dd9264-giaidap, ROLE=R — Resumer/ghi file, MODEL=UNKNOWN): thứ tự ghi thật: STATE.md (reconcile đầu tiên 10:16:09Z) → REGISTER/LICH-SU.md (append đúng 1 dòng) → RUNS/INDEX.md (append đúng 1 dòng) → STATE.md (hoàn tất §13 lúc 10:16:48Z) → AGENTS.md §3 + arena-agent-mode.md §7 (nguyên văn câu MERGE_OK của packet Owner ngày 2026-10-27) → MAINTAIN/kiểm literal → RUNS/INDEX.md (cập nhật CHÍNH dòng vừa thêm, không thêm dòng thứ hai) → sha256sum toàn bộ 9 file → STATE.md (ghi cuối trước commit). Chưa mở PR tại checkpoint này; khi có số PR thật sẽ cập nhật CHÍNH dòng bảo trì + STATE.md trong cùng commit nối tiếp, tính lại 9 hash và giữ STATE.md là file ghi cuối. Không tự merge/không tự chứng nhận độc lập.
MAINTAIN: 2026-10-27T10:20:33Z — HASH: tính lại 9/9 bằng sha256sum; lệnh nguyên văn kiem.md §5 in 8 hash + MAP kiểm riêng. CON TRỎ: test -f 18 file thật, test -d 5 thư mục, PROTOCOL/*.md=6; tất cả tồn tại. Tên A.md/B.md/C.md và RUNS/0001-... trong packet là mẫu, BAN-DO.md là tên bị cấm tạo, không giả là artifact có sẵn. LỆNH MẪU: A exit=1 (kiem.md:31/handoff-packet.md:29), B exit=1 (handoff-packet.md:55), C exit=2 (handoff-packet.md:83; No such file or directory); không tuyên bố MAINTAIN toàn bộ PASS. Các lệnh chứng minh của TASK hiện tại được kiểm riêng trong log; mẫu hỏng ghi MUI=c, không tạo file/RUN mới.
Cổng kết phiên là kỷ luật TỰ NGUYỆN — không có CI cưỡng chế.

## HASH CHUẨN
Tính lại MỌI hash lúc 2026-10-27T10:20:33Z bằng `sha256sum LAW/00-SUPREME-LAW.md LAW/00-PROVENANCE-MAP.md PROTOCOL/*.md scope-reality-check/SKILL.md`, SAU các sửa file; ghi STATE.md cuối. Đã chạy nguyên văn lệnh một dòng PROTOCOL/kiem.md §5 (8 hash có khóa) + `sha256sum LAW/00-PROVENANCE-MAP.md` (MAP_SHA256). Tổng đúng 9 hash: LAW + MAP + 6 PROTOCOL + SKILL. So đầu phiên: chỉ arena-agent-mode.md đổi từ d104dd4ccb297f1dde12a531631be7bc324944ab8e442acb36526b0beaaf977a sang 702a467bf047e84e7bb1d6323fb72f6dd6b440b4b43f5cbbb61588bfc7241c35; 8 hash còn lại vẫn được TÍNH LẠI, không chép tin theo bản cũ. Đây là hash của nhánh PR; MERGE_OK CHƯA có trên main @ bdf9d161.
LAW_SHA256: 2cf47ae59380740b500402eb386ae3b63b06d28a4d1b90b1e58a9524784eee52
MAP_SHA256: c15b64d5cb89f6fd9af85290a50bf710b6c06943403b0f9a124df67a73ca2d18
PROTOCOL_HASHES:
- PROTOCOL/arena-agent-mode.md:702a467bf047e84e7bb1d6323fb72f6dd6b440b4b43f5cbbb61588bfc7241c35
- PROTOCOL/cach-nghi.md:cd49bd3c0427bd842feac0b6f4d5de567cea9dcedac7f2bbc19be855dfc73c40
- PROTOCOL/handoff-packet.md:5215f30ec053b78861c2b11c38ed918b839e57aeb7779c938df37dcf9a850b1c
- PROTOCOL/kiem.md:a3dc66e995950638b19c9210e74bd5801d0ea62fa821626ead674535a71b1464
- PROTOCOL/multi-brain-loop.md:523d15cebb081c099bbfc65ec313591588589a015f63b987b8f6576cc8f6169f
- PROTOCOL/resume-protocol.md:d56f4583c5a774a089e0d7832c066353b2d45bb07f3bb9b41770d40522e6f902
SKILL_HASH: 941ca990c137a33f1f18fbee43411e2b35a3635944c531905f974cd276221268

## PR_STATE (đối chiếu GitHub thật 2026-10-27T10:14:19Z — reconcile sau merge #9; TRƯỚC khi mở PR phiên arena/97dd9264: 9 PR, 0 OPEN)
Mỗi dòng: `PR_STATE: <PR#> <OPEN|MERGED|CLOSED> <ngày kiểm>`. Nguồn: `gh pr list --state all` + `gh pr view`.
```text
PR_STATE: #1 MERGED 2026-10-27 (main @ 0a892a4; mergedAt 2026-10-26T10:32:04Z)
PR_STATE: #2 CLOSED 2026-10-27 (không merge; baseRefName=main, mergedAt=null)
PR_STATE: #3 CLOSED 2026-10-27 (không merge; baseRefName=main, mergedAt=null)
PR_STATE: #4 MERGED 2026-10-27 (main @ 03639d4; mergedAt 06:36:32Z)
PR_STATE: #5 MERGED 2026-10-27 (base arena/b960bf99-giaidap — KHÔNG vào main; nội dung đưa lên main bởi PR reconcile #7, #7 đã MERGED nên nội dung #5 NAY ĐÃ trên main)
PR_STATE: #6 MERGED 2026-10-27 (main @ 60d6cc0; mergedAt 06:37:18Z — merge sau #4)
PR_STATE: #7 MERGED 2026-10-27 (mergedAt=2026-10-27T07:57:23Z, baseRefName=main; mergeCommit gh=94162e3 theo hồ sơ trước; cơ chế rebase/stack là INFERENCE, không phải xác nhận độc lập)
PR_STATE: #8 MERGED 2026-10-27 (mergedAt=2026-10-27T07:57:21Z, baseRefName=main; mergeCommit=03ee7be theo hồ sơ trước, là tip main SAU #8, không phải tip hiện tại; L1–L4 + B1–B8)
PR_STATE: #9 MERGED 2026-10-27 (arena/6ceeb5d2-giaidap → main; baseRefName=main, mergedAt=2026-10-27T10:11:59Z, mergeCommit=bdf9d1615a9e7343871eb17a3e8ca554a3df3687; gh pr view 9 xác nhận 3 file STATE.md + REGISTER/LICH-SU.md + RUNS/INDEX.md đã vào main)
```

## VIỆC ĐANG MỞ
- 0000-pr1-verify — OPEN (verdict gần nhất của B cho head 84ae8b3: PASS_WITH_FIXES; bản V4 chưa kiểm lại). NEXT của RUN giữ nguyên: giao vai B ở PHIÊN KHÁC, EVIDENCE_MODE=SEALED, INPUT cấp tường minh, kiểm diff 84ae8b3..HEAD (LUẬT 12, LUẬT 08, map V4, KB/INDEX.md §MỞ RỘNG, cặp hash B.md); phiên R này KHÔNG làm B.
- Packet hiện tại — đã reconcile #9 và ghi nguyên văn MERGE_OK tại AGENTS.md §3 + PROTOCOL/arena-agent-mode.md §7 trên arena/97dd9264-giaidap; chưa mở PR tại checkpoint trước commit, base sẽ là main. Nội dung mới CHƯA merge, chờ Owner review/merge thủ công; phiên này không merge dù có comment MERGE_OK.
- Đã đóng việc chờ review/merge PR #9: MERGED vào main lúc 2026-10-27T10:11:59Z theo gh thật. Kiểm trước khi mở PR phiên này: tổng 9 PR, 0 OPEN; không mang dòng chờ #9 sang việc đang mở.

## NEXT_ONE_ACTION
Mở đúng 1 PR base=main từ arena/97dd9264-giaidap, trả RETURN_PACKET->OWNER đủ 11 trường rồi dừng; sau khi có số PR thật, NEXT chuyển sang Owner review/merge thủ công PR đó. Không tự merge và không chuyển sang vai B của RUN 0000.

## BLOCKER & UNKNOWN
- BLOCKER: Chưa được gỡ PROVENANCE_STATUS=PENDING_VERIFICATION vì vai B chưa kiểm độc lập bản map V4 sau vá lần 5–7 (kiểm ngày 2026-10-27). GIỮ NGUYÊN qua lần reconcile này — reconcile sau merge KHÔNG phải kiểm chứng độc lập, không đủ thẩm quyền gỡ (LUẬT 03, LUẬT 04).
- BLOCKER (đã hết hiệu lực 2026-10-27T10:14:19Z): chờ Owner review/merge PR #9 — GitHub xác nhận #9 ĐÃ MERGED 10:11:59Z, base=main. PR của phiên này chưa mở; không tự merge vì quy tắc MERGE_OK chưa được đưa lên main và packet cấm tường minh.
- UNKNOWN: Cơ chế claim/lock chưa làm; STATE.md nằm trên nhánh từng phiên, không phải khóa dùng chung. Quan sát thực tế lần này: main còn ghi #9 OPEN trong khi gh trả MERGED. Đây là drift sau merge, không phải bằng chứng đã có cơ chế khóa; packet này KHÔNG làm claim/lock.
- UNKNOWN: Cơ chế rebase/stack của #7/#8 trong hồ sơ trước chỉ là INFERENCE từ git log/gh, chưa được bên độc lập xác nhận. Không nâng giải thích cơ chế đó thành FACT trong lần reconcile #9.
- UNKNOWN: CONTENT_SHA256_B_DECLARED=UNKNOWN trong RUNS/0000-pr1-verify/B.md do B không tự khai (kiểm ngày 2026-10-26).
- UNKNOWN: Chưa có bằng chứng phiên mới độc lập chạy nghiệm thu T1–T6 để nâng MỐC từ KHUNG lên ĐANG_VẬN_HÀNH (kiểm ngày 2026-10-27); nâng MỐC cần Owner xác nhận kèm trích nguyên văn. Phiên reconcile này KHÔNG nâng MỐC.
- ĐÃ GIẢI QUYẾT 2026-10-27 (thay dòng UNKNOWN cũ): LAW/00-PROVENANCE-MAP.md ĐÃ vào HASH CHUẨN với khóa `MAP_SHA256` theo packet L3 của Owner; lệnh một dòng kiem.md §5 chưa in khóa này (MUI=b, chờ Owner cấp việc sửa kiem.md).
- UNKNOWN: Repo không chứa bản ghi nào về "2 dòng DRIFT giả của phiên trước" (tìm `DRIFT` trong repo: chỉ là thuật ngữ giao thức); cách chữa ở `PROTOCOL/kiem.md` §5 làm theo yêu cầu và chưa được kiểm độc lập.
- UNKNOWN: Lý do đóng PR #2 và #3 (CLOSED, không merge) chưa được ghi trong main; quyết định đó thuộc Owner.

- MUI=a | CONFLICT=YES (phần áp dụng merge DỪNG): AGENTS.md:77/arena-agent-mode.md:154 thêm ngoại lệ MERGE_OK đúng packet, nhưng multi-brain-loop.md:148,177 và arena-agent-mode.md:173 vẫn ghi cấm merge tuyệt đối. Các quy tắc vai/binding còn lặp ở multi-brain-loop.md §11, handoff-packet.md:14 và SKILL.md §GIAIDAP binding. Không tự sửa các vị trí ngoài §3/§7; Owner quyết việc đồng bộ sau. Packet phiên này cấm merge nên KHÔNG áp dụng ngoại lệ.
- MUI=a | CONFLICT=YES (không dùng skill để vượt giao thức): cach-nghi.md:19 nói skill thắng khi va nhau, còn scope-reality-check/SKILL.md:251–252 đặt PROTOCOL trên skill. T5 ở resume-protocol.md:140 ghi ROLE_BOUND chung, trong khi vai R dùng USER_EXPLICIT ở :130; khả năng áp T5 cho R còn UNKNOWN, không dùng để tự chấm/nâng MỐC. Không sửa các file đó ngoài phạm vi.
- MUI=b: các trường LAW_CHECK/SOURCE_SHA256 lặp ở AGENTS.md:45 và multi-brain-loop.md:65,77 (khác nguồn biên lai phải giữ tách); khuôn hash trong resume-protocol.md:83 vẫn nói 4 PROTOCOL/6 hash trong khi thực tế 6 PROTOCOL/9 hash, lệnh kiem.md:72 chưa in MAP_SHA256. Đã tính MAP riêng, không tự sửa khuôn ngoài phạm vi.
- MUI=c: các lệnh mẫu chưa chạy thành công nguyên văn trên checkout vì RUN 0001 không tồn tại (A/B exit=1, C exit=2; xem MAINTAIN và log). Chúng KHÔNG phải bằng chứng chạy A/B/C; không tạo file để né giới hạn packet. Kiểm grep MERGE_OK chỉ chứng minh có chuỗi, không tự chứng minh tác giả là Owner; không thử merge để kiểm quyền.
- MUI=d: cùng câu "Ghi header chuẩn 6 trường; MODEL=UNKNOWN nếu không xác minh được." phải chép vào ba packet tại handoff-packet.md:38,67,94; chỉ báo, không tự refactor template.

## OWNER_QUYẾT
Bất biến: đủ **5 dòng riêng biệt D1–D5, KHÔNG gộp**; mỗi dòng giữ nhãn `OWNER_SAID=PARAPHRASE` (chưa có comment nguyên văn của Owner trên PR #1).
- D1 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: cho phép sửa riêng LUẬT 12) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap
- D2 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: giữ bảng 15 dòng NEW=1/DERIVED=14, không bỏ LUẬT 15) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap
- D3 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: B.md ghi nguyên văn, CONTENT_SHA256 lấy theo B tự khai, không khai => UNKNOWN) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap
- D4 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: cho phép sửa riêng LUẬT 08, các LUẬT khác không đổi) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap
- D5 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: tách hash B.md thành 2 field riêng, không gộp) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap

## LỊCH SỬ GẦN NHẤT (tối đa 8 dòng; dòng cũ hơn nằm ở REGISTER/LICH-SU.md — append-only)
- 2026-10-27 — POST_MERGE_RECONCILE sau merge PR #9 (phiên ĐẦU TIÊN, §13): MERGED 2026-10-27T10:11:59Z, base=main, mergeCommit=bdf9d1615a9e7343871eb17a3e8ca554a3df3687. Sửa STATE.md TRƯỚC (#9 OPEN→MERGED; SINH_TỪ_HEAD=bdf9d161; MAIN_CONTENT_CHECK FAIL→PASS; VIỆC ĐANG MỞ/NEXT/BLOCKER cập nhật), rồi ghi lịch sử và POST_MERGE_RECONCILE NEEDED→DONE; đẩy đúng 1 dòng Merge khung V1 (0a892a4/PR #1) xuống cuối REGISTER/LICH-SU.md. Cùng packet: ghi nguyên văn MERGE_OK tại AGENTS.md §3 + arena-agent-mode.md §7; tính lại đủ 9 hash, chỉ hash arena-agent-mode.md đổi; MAINTAIN và MUI=a,b,c,d ghi ở trên. Nhánh arena/97dd9264-giaidap, PR base=main chưa mở tại checkpoint này; không merge. Giữ PENDING_VERIFICATION và MỐC=KHUNG; không mở A/B/C.
- 2026-10-27 — POST_MERGE_RECONCILE sau merge PR #7 + PR #8 (phiên ĐẦU TIÊN sau merge, `PROTOCOL/resume-protocol.md` §13): #8 MERGED 07:57:21Z → main @ 03ee7be, #7 MERGED 07:57:23Z (base=main, vào main bằng rebase, mergeCommit gh=94162e3); sửa `STATE.md` (PR_STATE #7/#8 OPEN→MERGED, `SINH_TỪ_HEAD`=03ee7be, POST_MERGE_RECONCILE NEEDED→DONE, MAIN_CONTENT_CHECK=PASS, VIỆC ĐANG MỞ bỏ 2 dòng #7/#8, NEXT_ONE_ACTION đổi sang giao vai B, BLOCKER/UNKNOWN cập nhật); hash 9/9 KHÔNG đổi (không sửa file nào trong 9 hash); GIỮ NGUYÊN PENDING_VERIFICATION, KHÔNG nâng MỐC, KHÔNG mở vòng A/B/C — nhánh arena/6ceeb5d2-giaidap (sinh từ 03ee7be), PR #9 base=main (https://github.com/7roger89-web/GIAIDAP/pull/9); số PR điền ở commit nối tiếp chỉ-sửa-STATE.md ngay sau khi mở PR
- 2026-10-27 — Đối chiếu chống mất nội dung cho PR #7 (B1–B8: KHÔNG mất nội dung #5/#6; kết quả dán vào mô tả PR #7) + bịt L1–L4 (BASE_PHAI_LA_MAIN §4.1 arena-agent-mode; MAIN_CONTENT_CHECK vào RESUME_CHECK §2 resume-protocol; MAP_SHA256 vào HASH CHUẨN; 4 dòng sự cố PR #5 nối cuối LICH-SU.md) — nhánh arena/953af346-giaidap (sinh từ tip nhánh #7 @ 94162e3), PR mới base=main, STACK chứa trọn #7 — PR #8 MERGED 07:57:21Z (main @ 03ee7be)
- 2026-10-27 — Reconcile PR #6 lên main sau khi #4 và #5 đã merge: PR mới từ nhánh arena/ea8a6620-giaidap; đưa nội dung #5 lên main; hợp nhất xung đột; RESTATE một nguồn (cach-nghi §1); lệnh hash một dòng (kiem §5); §13 POST_MERGE / §14 MAINTAIN — PR #7 MERGED 07:57:23Z (base=main, vào main bằng rebase)
- 2026-10-27 — Lắp lớp chứng minh verification-first: thêm PROTOCOL/kiem.md (khối CÁCH CHỨNG MINH 4 dòng, DRY_RUN, MÙI a–d, nhịp MAINTAIN, bản đồ workstream) + PROTOCOL/cach-nghi.md (8 bước nghĩ trước khi làm); packet A/B/C lên 10 trường, RETURN_PACKET thêm 3 trường chứng minh; cold-start thêm cach-nghi — PR #6 MERGED 06:37:18Z (main @ 60d6cc0)
- 2026-10-27 — Vá 4 lỗ tự mục của cơ chế hồi sinh (A: POST_MERGE_RECONCILE/PR_STATE/ghi-hash/LICH-SU.md; B: đồng bộ lệnh B/C/A; C: câu lệnh đọc skill + TỰ SOI; D: sửa seed BAC/MỐC/OWNER_QUYẾT) — PR #5 MERGED 06:36:46Z vào nhánh arena/b960bf99-giaidap (KHÔNG vào main; đưa lên main bởi PR #7 — nay đã MERGED nên nội dung #5 ĐÃ trên main)
- 2026-10-27 — Khởi tạo cơ chế hồi sinh + bind skill scope-reality-check + vá khuôn RUN 0000 — nhánh arena/b960bf99-giaidap (sinh từ d907435) — PR #4 MERGED 06:36:32Z (main @ 03639d4)
- 2026-10-27 — Đưa thư mục skill scope-reality-check lên main — commit d907435

Đẩy xuống REGISTER/LICH-SU.md (append-only) khi tràn 8 dòng: 2026-10-26 Vai B kiểm độc lập (84ae8b3); 2026-10-26 Vá lần 5 (db14795); 2026-10-26 Khởi tạo khung V1 (612a8e6, đã đẩy ở vá trước); 2026-10-27 đẩy thêm dòng "2026-10-26 Vá lần 6 (b1ba697)"; 2026-10-27 (phiên reconcile sau merge #7+#8) đẩy thêm dòng "2026-10-26 Vá lần 7 (9c4b63a)". 2026-10-27 (phiên reconcile sau merge #9) đẩy thêm đúng dòng "2026-10-26 Merge khung V1 — 0a892a4/PR #1".

## CON TRỎ
- Luật & ánh xạ nguồn: LAW/00-SUPREME-LAW.md | LAW/00-PROVENANCE-MAP.md
- Giao thức & skill: PROTOCOL/resume-protocol.md | PROTOCOL/multi-brain-loop.md | PROTOCOL/kiem.md | PROTOCOL/cach-nghi.md | scope-reality-check/SKILL.md
- Sổ & mục lục: REGISTER/BAC.md | REGISTER/LICH-SU.md | RUNS/INDEX.md | KB/INDEX.md
