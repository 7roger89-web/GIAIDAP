RUN_ID: 0000-pr1-verify
ROLE: B
LOẠI RUN: KIỂM LUẬT ĐỘC LẬP (không phải B RUN)
CONTAMINATED=YES
MODEL: Muse Spark 1.3
TOOL: GitHub MCP get_file_contents (call-read-tool) + local sed -n '<n>p' trên file notebook đã tải
REVIEWED_HEAD: 84ae8b3dfd8271d11af40c49fb34715634af1d0f
DATE: 2026-10-26
CONTENT_SHA256: UNKNOWN
CONTENT_STATUS: VERBATIM_RECEIVED
GHI CHÚ: MODEL và TOOL lấy từ chính header báo cáo của B bên dưới (B tự khai). CONTENT_SHA256=UNKNOWN vì B không tự khai SHA-256 cho chính báo cáo của mình; Writer không tính thay rồi ghi như B khai.
GHI CHÚ 2: Mọi lỗi chính tả của B giữ nguyên, không sửa (xem `DECISION.md` §4).

=== BẮT ĐẦU NGUYÊN VĂN B REPORT ===

# B.md — RUN PR1-VERIFY | ROLE=B | INPUT_REF | DATE | MODEL | TOOL | LAW_CHECK

```
RUN: PR1-VERIFY
ROLE: B — VERIFIER (không viết lại kiến trúc, không merge)
INPUT_REF:
  - https://github.com/7roger89-web/GIAIDAP/pull/1 — files fetched via refs/pull/1/head, head ref seen in tree listing: 84ae8b3dfd8271d11af40c49fb34715634af1d0f
    - LAW/00-PROVENANCE-MAP.md — blob 502a26ae19b5d2f50670d8472fb9a86ea2ff5fe1, 8085 bytes
    - LAW/00-SUPREME-LAW.md — blob 9163d9b98479024c1f80f5d49787a7743c78776f, 6408 bytes, SHA256 (file as fetched) 5eb22efb1f4f7bc9b4f9838c59b3c6aeea934ad9718b588192c037e02964d56a
    - PROTOCOL/multi-brain-loop.md — blob 60731bc21a6d4ae0bb0981df6fc413eca7ddc71e, 7845 bytes
    - Plus, for B5 only: AGENTS.md, README.md, KB/INDEX.md, PROTOCOL/arena-agent-mode.md, PROTOCOL/handoff-packet.md, RUNS/README.md (same PR head)
  - https://github.com/7roger89-web/P2P-upgrade-github-1/blob/main/docs/p2p-development/P2P-OPERATIONS-NOTEBOOK.md
DATE: 2026-10-26
MODEL: Muse Spark 1.3
TOOL: GitHub MCP get_file_contents (call-read-tool) + local sed -n '<n>p' on the fetched notebook file (literal sed run, not only Python)
LAW_CHECK: PASS | SOURCE=7roger89-web/P2P-upgrade-github-1@main:docs/p2p-development/P2P-OPERATIONS-NOTEBOOK.md | SOURCE_SHA256=11ce33bb9c514d32ad3aec3eb7d8b40f0d0290b1dbe79eaa15751ef34668bd4b | DATE=2026-10-26
LAW_CHECK_GIAIDAP_READ: PASS | SOURCE=GIAIDAP PR1 LAW/00-SUPREME-LAW.md (as fetched above) | SOURCE_SHA256=5eb22efb1f4f7bc9b4f9838c59b3c6aeea934ad9718b588192c037e02964d56a | DATE=2026-10-26
```

FACT: LAW_CHECK=PASS ở đây chỉ có nghĩa là các file nguồn đã được đọc và băm trong phiên này. FACT: Nó KHÔNG có nghĩa là LAW/00 đã VERIFIED. FACT: LAW/00 tự ghi `PROVENANCE_STATUS=PENDING_VERIFICATION` và §0.1 ghi biên lai PR1 là vòng tròn. INFERENCE: Chỉ sau khi các điều kiện ở B6 được sửa và Owner xác nhận, PENDING_VERIFICATION mới được gỡ.

## VERDICT

**VERDICT: PASS_WITH_FIXES**

- FACT: Blob nguồn khớp hoàn toàn (xem phần nguồn dưới đây), và mọi số dòng đã ghi trong bảng ánh xạ đều trỏ đúng mục nguồn (B1: 14/14 luật, 0 sai).
- FACT: Bảng đã tự khai nhiều phần tự chế (thang 7 bước LUẬT 05, thêm/bớt nhãn LUẬT 09, bỏ Control Tower LUẬT 10, DEPRECATED + 3 cột LUẬT 11, artifact KB/INDEX.md LUẬT 12) — nhưng vẫn kết luận `NEW=0`.
- INFERENCE: `NEW=0` là kết luận gây hiểu lầm, nhất là LUẬT 12: cơ chế tra cứu bằng KB/INDEX.md + khớp từ khóa + bỏ dấu không có mục nguồn tương ứng, dù cảm hứng có nguồn. Do đó NEW=0 không được giữ nguyên.
- INFERENCE: Các lỗi còn lại đều sửa được bằng văn bản (sửa map, sửa header LAW/00, ghi PHẦN_TỰ_CHẾ, đổi LOẠI LUẬT 12), không phải là bịa nguồn toàn bộ. Vì vậy verdict không phải FAIL toàn cục, nhưng cũng không phải PASS sạch.
- FACT: Điều kiện gỡ PENDING_VERIFICATION nằm ở B6 / ĐỀ_XUẤT_SỬA_TỐI_THIỂU. Chưa sửa xong thì PENDING_VERIFICATION vẫn đứng.

### Biên lai nguồn (đọc độc lập trong phiên này)

- FACT: Notebook tại main, dòng đầu file là `# P2P_OPERATIONS_NOTEBOOK`, blob SHA do GitHub trả về: `f3edbac375d4e1540011f0c12081938d05a77b4f` — KHỚP với chuỗi packet yêu cầu kiểm.
- FACT: Băm lại từ bytes đã tải: content SHA256 `11ce33bb9c514d32ad3aec3eb7d8b40f0d0290b1dbe79eaa15751ef34668bd4b`, git blob SHA1 tính lại `f3edbac375d4e1540011f0c12081938d05a77b4f` — KHỚP cả hai, kích thước file 138240 bytes — KHỚP `NGUỒN_SIZE_BYTES=138240` trong bảng.
- FACT: Các chuỗi packet yêu cầu đều tìm đúng, 1-indexed:
  - `## 2A. P2P_SUPREME_OPERATING_LAW_V1` — notebook dòng 90.
  - `### Supreme laws` — notebook dòng 426.
  - `### Bounded ACTIVE experience preflight invariant` — notebook dòng 249.
  - `### RULE 01 — EXPLICIT_DESTINATION` — notebook dòng 1218.
  - `### RULE 21 — BEGINNER_PLAIN_LANGUAGE_FIRST` — notebook dòng 2616.

## B1_BẢNG_XÁC_MINH_SỐ_DÒNG

FACT: Phương pháp: chạy literal `sed -n '<n>p'` trên file notebook đã tải (138240 bytes). FACT: Tất cả 25 số dòng phân biệt đã ghi trong bảng đều trả về đúng heading/câu nguồn. Đếm theo luật (không theo số dòng): **đúng 14 / sai 0 / không kiểm được 0** đối với các số dòng đã ghi.

FACT: Lưu ý phân biệt: một số nguồn phụ trong bảng không ghi số dòng (ví dụ LUẬT 03 ghi Supreme laws 3 nhưng chỉ ghi số 548 cho Supreme laws 8; LUẬT 04 ghi Supreme laws 8 nhưng chỉ ghi số 1306 cho RULE 08; LUẬT 06 ghi RULE 08 + Supreme laws 1 nhưng chỉ ghi số 1296 cho RULE 07; LUẬT 05 ghi Supreme laws 4 nhưng không ghi số dòng). INFERENCE: Những nguồn phụ đó không tính là "sai số dòng", vì chúng không ghi số; B đã kiểm riêng bằng tìm heading và thấy chúng tồn tại (Supreme laws 3 dòng 444, Supreme laws 8 dòng 548, RULE 08 dòng 1306, Supreme laws 1 dòng 428, Supreme laws 4 dòng 449). Chúng được ghi là "không ghi số dòng" ở cột ghi chú dưới đây, không phải "không kiểm được".

| LUẬT | Số dòng đã ghi trong bảng | sed -n trả về (rút gọn) | Kết luận |
|---|---|---|---|
| LUẬT 01 | 428 | FACT: dòng 428: `1. **OWNER_OUTCOME_AND_AUTHORITY_ARE_INVARIANTS** — Understand the outcome and` | ĐÚNG |
| LUẬT 02 | 444 | FACT: dòng 444: `3. **REAL_STATE_AND_EVIDENCE_OVERRIDE_ASSUMPTIONS** — Fresh-check relevant state` | ĐÚNG |
| LUẬT 03 | 548 (+ Supreme laws 3 không ghi số) | FACT: dòng 548: `8. **TASK_CONTRACT_AND_ACCEPTANCE_FIDELITY** — Before delegating or executing a`; FACT: Supreme laws 3 tồn tại ở dòng 444 (xem LUẬT 02) | ĐÚNG (số đã ghi); nguồn phụ không ghi số |
| LUẬT 04 | 1306 (+ Supreme laws 8 không ghi số) | FACT: dòng 1306: `### RULE 08 — INDEPENDENT_SUPERVISOR`; FACT: Supreme laws 8 ở dòng 548 | ĐÚNG (số đã ghi); nguồn phụ không ghi số |
| LUẬT 05 | 438, 1395, 1430, 1091 (+ Supreme laws 4 không ghi số) | FACT: dòng 438: `2. **SIMPLEST_USEFUL_PATH_TO_COMPLETION**`; dòng 1395: `### RULE 12 — MINIMUM_SUFFICIENT_WORK`; dòng 1430: `### RULE 14 — OVER_ENGINEERING_CHECK`; dòng 1091: `### Anti-overengineering decision`; FACT: Supreme laws 4 ở dòng 449 | ĐÚNG (số đã ghi); nguồn phụ không ghi số |
| LUẬT 06 | 1296 (+ RULE 08, Supreme laws 1 không ghi số) | FACT: dòng 1296: `### RULE 07 — WRITER_BOUNDARY`; FACT: RULE 08 dòng 1306, Supreme laws 1 dòng 428 | ĐÚNG (số đã ghi); nguồn phụ không ghi số |
| LUẬT 07 | 1507, 249 | FACT: dòng 1507: `### RULE 16 — CONTEXT_HYGIENE_AND_PLAN_LIFECYCLE`; dòng 249: `### Bounded ACTIVE experience preflight invariant` | ĐÚNG |
| LUẬT 08 | 1218, 1237, 1260, 468, 857 | FACT: dòng 1218: `### RULE 01 — EXPLICIT_DESTINATION`; dòng 1237: `### RULE 02 — CHAT_TITLE_REQUIRED`; dòng 1260: `### RULE 03 — SAME_CHAT_MUST_NAME_CHAT`; dòng 468: `6. **PROMPT_TITLE_DESTINATION_AND_PLAN_STATE_ARE_EXPLICIT**`; dòng 857: `### Prompt-alignment gate` | ĐÚNG |
| LUẬT 09 | 504 | FACT: dòng 504: `7. **ANALYTICAL_AUTONOMY_AND_DELEGATION_ALIGNMENT** — For non-trivial P2P` | ĐÚNG |
| LUẬT 10 | 1265, 1279 | FACT: dòng 1265: `### RULE 04 — GITHUB_IS_DURABLE_CHECKPOINT`; dòng 1279: `### RULE 05 — SESSION_OR_QUOTA_RECOVERY` | ĐÚNG |
| LUẬT 11 | 288, 307, 1525 | FACT: dòng 288: `### Task-end learning reconciliation invariant`; dòng 307: `- Preserved lifecycle: \`CANDIDATE -> VERIFIED -> ACTIVE -> SUPERSEDED \| QUARANTINED\`.`; dòng 1525: `NO_BLIND_DELETE_AFTER_MERGE = YES` (nằm trong RULE 16, bắt đầu dòng 1507) | ĐÚNG |
| LUẬT 12 | 249, 288 | FACT: dòng 249 và 288 như trên | ĐÚNG (số dòng); nội dung cơ chế thì xem B2 — số dòng đúng không có nghĩa là cơ chế có nguồn |
| LUẬT 13 | 95, 1206 | FACT: dòng 95: `Do not create a parallel supreme-law file or duplicate framework.`; dòng 1206: `### Canonical change rule` | ĐÚNG |
| LUẬT 14 | 1395, 461 | FACT: dòng 1395: `### RULE 12 — MINIMUM_SUFFICIENT_WORK`; dòng 461: `5. **PRESERVE_CONTINUITY_AND_STOP** — For long work, retain only the durable` | ĐÚNG |

**Tổng B1: đúng 14 / sai 0 / không kiểm được 0 (tính theo luật, cho các số dòng đã ghi).**

## B2_PHÁN_XỬ

### LUẬT 05 — ĐƯỜNG ĐƠN GIẢN NHẤT + THỨ TỰ CHỐNG OVER-ENGINEERING

- FACT: Nguồn có: Supreme laws 2 dòng 438-443 ("Choose the next action with the best practical contribution… Do not open speculative architecture… before the core capability shows a need"); OE Gate 5 câu hỏi dòng 1091-1116 (SIMPLER_PATH, MATERIAL_PROGRESS, NECESSITY, CORE_BEFORE_SUPPORT, SMALLER_VERIFIABLE_SLICE); RULE 12 dòng 1395; RULE 14 dòng 1430-1433 (áp OE Gate).
- FACT: Nguồn KHÔNG có: thang 7 bước có thứ tự (1) trả lời/không code → (2) cấu hình → (3) sửa quy trình → (4) sửa hẹp → (5) dùng lại component → (6) thay skill/tool → (7) trừu tượng mới. FACT: Bảng tự khai điều này: "Thang 7 bước (1..7) do GIAIDAP tự xếp — không tìm thấy trong nguồn".
- FACT: Câu "không biến một lỗi đơn lẻ thành luật/hạ tầng vĩnh viễn" CÓ nguồn: Supreme laws 4 dòng 449-455 ("Do not convert every isolated failure into a permanent rule or new infrastructure").
- INFERENCE: Nguyên tắc "đường đơn giản nhất + OE Gate" là DERIVED thật; thứ tự 7 bước là phần tự chế, không phải thứ tự nguồn.
- **Đề xuất — giữ LOẠI:** `DERIVED` cho nguyên tắc, nhưng bắt buộc ghi PHẦN_TỰ_CHẾ. Nếu chỉ giữ một LOẠI duy nhất mà không ghi PHẦN_TỰ_CHẾ, phải đổi thành `NEW` cho phần thứ tự.
- **PHẦN_TỰ_CHẾ đề xuất ghi:** "Thang 7 bước và thứ tự 1→7 do GIAIDAP tự xếp, KHÔNG có trong nguồn. Nguồn chỉ có Supreme laws 2 (dòng 438), OE Gate 5 câu hỏi (dòng 1091), RULE 12 (dòng 1395), RULE 14 (dòng 1430). Câu về lỗi đơn lẻ CÓ nguồn Supreme laws 4 (dòng 449)."

### LUẬT 09 — NHÃN NHẬN THỨC

- FACT: Nguồn, Supreme laws 7 dòng 504-510: "label or clearly separate verified fact, inference, hypothesis, judgment, and recommendation" (dòng 509-510).
- FACT: GIAIDAP dùng bộ 5 nhãn: FACT | INFERENCE | HYPOTHESIS | UNKNOWN | OWNER_CONFIRMATION_REQUIRED.
- FACT: Đối chiếu: verified fact → FACT (tương đương), inference → INFERENCE, hypothesis → HYPOTHESIS là có nguồn; judgment và recommendation bị BỎ; UNKNOWN và OWNER_CONFIRMATION_REQUIRED được THÊM và không có trong liệt kê dòng 509-510.
- FACT: Bảng đã khai "bỏ judgment và recommendation, thêm OWNER_CONFIRMATION_REQUIRED (không có ở nguồn)", nhưng chưa ghi rõ UNKNOWN cũng là nhãn thêm vào so với liệt kê dòng 509-510. INFERENCE: UNKNOWN với tư cách khái niệm có xuất hiện ở nơi khác trong notebook (ví dụ trạng thái UNKNOWN ở Supreme laws 3 dòng 444-448), nhưng đó không phải là nhãn trong liệt kê của Supreme laws 7 — không được dùng sự xuất hiện ở nơi khác để nói bộ nhãn 5 mục là nguyên văn nguồn.
- **Đề xuất — giữ LOẠI:** `DERIVED` cho 3 nhãn đầu, bắt buộc ghi PHẦN_TỰ_CHẾ.
- **PHẦN_TỰ_CHẾ đề xuất ghi:** "Bộ nhãn 5 mục KHÔNG phải bộ nhãn nguồn. Nguồn (dòng 509-510) liệt kê: verified fact, inference, hypothesis, judgment, recommendation. GIAIDAP bỏ judgment, recommendation; thêm UNKNOWN và OWNER_CONFIRMATION_REQUIRED — hai nhãn thêm này không có trong liệt kê dòng 509-510."

### LUẬT 10 — GITHUB LÀ CHECKPOINT BỀN VỮNG

- FACT: Nguồn RULE 04 dòng 1265-1277: work identity là `REPOSITORY + WORKSTREAM + PR_HEAD_SHA + PR_HEAD_TREE` (dòng 1271-1274); "Do not use chat position or PR number alone as authority" (dòng 1277).
- FACT: Nguồn RULE 05 dòng 1279-1287: mất context/quota thì "Do NOT restart the task blindly", "Return to Control Tower", "Inspect the current durable branch/PR/head", "Continue from the exact verified checkpoint".
- FACT: GIAIDAP ghi identity là `REPO + WORKSTREAM + PR_HEAD_SHA + TREE`. INFERENCE: TREE ở đây chỉ có nghĩa nếu hiểu là viết tắt của PR_HEAD_TREE; bảng ghi "BỎ PR_HEAD_TREE (GIAIDAP viết tắt 'TREE')" là tự mâu thuẫn về từ ngữ — bỏ và viết tắt là hai việc khác nhau, và LAW vẫn giữ trường TREE.
- FACT: Bảng đã khai bỏ bước "Return to Control Tower" vì GIAIDAP không có Control Tower. INFERENCE: Câu GIAIDAP "quay lại checkpoint bền, không khởi động lại mù" là chuyển thể của RULE 05 trừ bước Control Tower, không phải nguyên văn RULE 05.
- **Đề xuất — giữ LOẠI:** `DERIVED`.
- **PHẦN_TỰ_CHẾ đề xuất ghi:** "TREE là viết tắt của PR_HEAD_TREE (dòng 1271-1274), KHÔNG phải bỏ trường này — sửa lại ghi chú bảng từ 'BỎ' thành 'ĐỔI TÊN'. Bước 'Return to Control Tower' (dòng 1285) bị bỏ vì GIAIDAP không có Control Tower; phần còn lại của RULE 05 (dòng 1284, 1286-1287) được chuyển thể thành 'quay lại checkpoint bền, không khởi động lại mù'."

### LUẬT 11 — VÒNG ĐỜI TRI THỨC KB

- FACT: Nguồn Task-end dòng 307: lifecycle `CANDIDATE -> VERIFIED -> ACTIVE -> SUPERSEDED | QUARANTINED`, áp cho "experience" (dòng 288-309: learning reconciliation, experience candidate), không phải cho "mục KB".
- FACT: Nguồn RULE 16 dòng 1525: `NO_BLIND_DELETE_AFTER_MERGE = YES`, trong ngữ cảnh sau merge, không phải quy tắc "mọi cái mới thay cái cũ".
- FACT: GIAIDAP STATUS = `ACTIVE | SUPERSEDED | DEPRECATED | QUARANTINED`, kèm 3 cột NGÀY / NGUỒN / ĐỘ TIN CẬY, áp lên "mục KB". FACT: Bảng đã khai thêm DEPRECATED và 3 cột, và nguồn áp lifecycle cho experience.
- FACT: Phần KHÔNG có nguồn / chưa khai: (a) DEPRECATED không có trong dòng 307; (b) 3 cột NGÀY/NGUỒN/ĐỘ TIN CẬY không có trong dòng 288-309; (c) CANDIDATE và VERIFIED bị bỏ khỏi STATUS GIAIDAP mà bảng không ghi là bỏ; (d) quy tắc "dữ kiện dễ cũ (giá, luật, model, API) phải ghi ngày kiểm và hạn" — grep toàn notebook cho `expir` cho 0 hit, và không có quy tắc hạn (expiry) tương đương trong các dòng đã dẫn; (e) quy tắc chuyển đổi "mới thay cũ thì cũ thành SUPERSEDED" là khái quát hoá từ NO_BLIND_DELETE_AFTER_MERGE (merge-specific, dòng 1525), không phải câu nguyên văn nguồn.
- **Đề xuất — giữ LOẠI:** `DERIVED` CHỈ khi PHẦN_TỰ_CHẾ dưới đây được ghi đầy đủ. INFERENCE: Nếu Owner áp tiêu chuẩn "schema/artifact riêng thì là NEW", LUẬT 11 phải đổi thành `NEW` cho phần schema KB — B không tự quyết tiêu chuẩn đó, Owner quyết (xem UNKNOWN).
- **PHẦN_TỰ_CHẾ đề xuất ghi:** "DEPRECATED, 3 cột NGÀY/NGUỒN/ĐỘ TIN CẬY, và việc áp lifecycle lên 'mục KB' (thay vì 'experience') là của GIAIDAP, KHÔNG có ở nguồn. CANDIDATE và VERIFIED trong dòng 307 bị bỏ khỏi STATUS GIAIDAP. Quy tắc 'dữ kiện dễ cũ phải ghi ngày kiểm và hạn' không có nguồn tương đương trong các dòng đã dẫn. Chỉ phần ACTIVE/SUPERSEDED/QUARANTINED và nguyên tắc không xóa mù là DERIVED từ dòng 307 và dòng 1525."

### LUẬT 12 — TRA CỨU BẰNG TỪ KHÓA — MỤC QUAN TRỌNG NHẤT

- FACT: Nguồn Bounded preflight dòng 249-286: lookup là lookup experience ACTIVE đã promoted, bounded theo task-text, qua các đường: script `experience_evolution.py … retrieve --task-text` (dòng 278), đọc capsule `.p2p/portable/P2P-EXPERIENCE-CAPSULE.json` và khớp trigger tokens (dòng 279), hoặc Control Tower `activation_summary` (dòng 280); receipt `EXPERIENCE_CHECK=` (dòng 253, 266-275); tối đa mặc định <= 3 experience (dòng 283); experience chỉ là advisory, không widen permissions (dòng 284-286).
- FACT: Nguồn Task-end dòng 288-309: chỉ khi `REPEATED_OR_MATERIAL_FAILURE | CLEARLY_REUSABLE_CORRECTION` mới tạo experience candidate kèm evidence + trigger conditions (dòng 293, 300-304); `ROUTINE_SUCCESS => LEARNING_RECONCILIATION=NONE`, "Do not manufacture memory or candidates from routine success" (dòng 292, 298-299).
- FACT: GIAIDAP LUẬT 12: "Vào repo => tra KB/INDEX.md theo từ khóa. KHỚP và còn ACTIVE => dùng làm điểm xuất phát (vẫn kiểm nguồn nếu là dữ kiện dễ cũ). KHÔNG KHỚP => tự tìm + suy nghĩ, rồi GHI LẠI mục KB mới. Từ khóa không phân biệt hoa/thường, bỏ dấu."
- FACT: Phần KHÔNG có nguồn: (a) artifact `KB/INDEX.md` — grep toàn notebook cho `KB/INDEX` cho 0 hit; (b) khớp từ khóa trên bảng KB thay vì khớp task-text/trigger tokens trên experience ACTIVE; (c) quy tắc "không phân biệt hoa/thường, bỏ dấu" — grep `diacritic`, `case-insensitive`, `bỏ dấu` trong notebook đều 0 hit; (d) điều kiện vào "Vào repo => tra" thay vì preflight cho "every non-trivial P2P-managed task" (dòng 256); (e) "KHÔNG KHỚP => … rồi GHI LẠI mục KB mới" vô điều kiện — trái với nguồn dòng 292/298-299 (routine success thì NONE, không tạo candidate), và sai thời điểm (nguồn tạo candidate ở task-end reconciliation, kèm evidence + trigger, không phải ngay lúc lookup không khớp).
- FACT: Bảng đã khai: "GIAIDAP thay bằng bảng từ khóa KB/INDEX.md + bỏ dấu khi so khớp — artifact riêng của GIAIDAP, KHÔNG có ở nguồn. Phần 'ghi lại mục KB mới' lấy từ learning reconciliation." INFERENCE: Lời khai này là đúng về artifact, nhưng vẫn giữ LOẠI=DERIVED và tổng NEW=0, nên lời khai bị chìm. Theo chính định nghĩa LOẠI của bảng ("NEW = Không có mục nguồn tương ứng — luật riêng của GIAIDAP"), cơ chế tra cứu của LUẬT 12 không có mục nguồn tương ứng — cảm hứng có nguồn không bằng cơ chế có nguồn.
- **Đề xuất — giữ LOẠI:** Đổi LUẬT 12 thành `NEW` cho cơ chế tra cứu (KB/INDEX.md + khớp từ khóa + bỏ dấu + ghi mới khi không khớp). Phần cảm hứng (lookup ACTIVE trước khi làm; ghi lại bài học tái dùng ở cuối task) giữ là DERIVED, nhưng phải sửa điều kiện ghi lại cho đúng nguồn.
- **PHẦN_TỰ_CHẾ đề xuất ghi:** "Toàn bộ cơ chế tra cứu là của GIAIDAP, KHÔNG có ở nguồn: bảng KB/INDEX.md, khớp từ khóa, không phân biệt hoa/thường, bỏ dấu khi so khớp, và quy tắc 'KHÔNG KHỚP => ghi mục KB mới'. Nguồn chỉ có: lookup experience ACTIVE theo task-text qua script/capsule/Control Tower (dòng 249-286) và tạo experience candidate ở task-end khi có failure tái diễn hoặc correction tái dùng rõ ràng, kèm evidence + trigger (dòng 288-309). GIAIDAP phải sửa: chỉ ghi mục mới khi bài học tái dùng rõ ràng (không phải mọi lần không khớp), và ROUTINE_SUCCESS thì không tạo mục mới (dòng 292, 298-299)."

## B3_LỆCH_CHƯA_KHAI

INFERENCE: Theo packet, mỗi lệch chưa khai dưới đây là BLOCKER cho việc gỡ PENDING_VERIFICATION — tức là phải sửa văn bản map/LAW rồi mới gỡ, không phải là bằng chứng LAW không dùng được. Các lệch ĐÃ khai trong bảng (ví dụ bỏ PLAN_REFERENCE ở LUẬT 08, bỏ Control Tower ở LUẬT 10, DEPRECATED ở LUẬT 11, artifact KB ở LUẬT 12) không liệt kê lại ở đây, trừ khi ghi chú bảng tự mâu thuẫn.

1. FACT — LUẬT 01, map ghi "Giữ nguyên danh sách lý do phải hỏi Owner": nguồn dòng 430-432 liệt kê "genuine outcome, authority, material cost, security/privacy/business-impact, production, destructive, infrastructure-commitment, or hard-to-reverse decisions". FACT: GIAIDAP bỏ `business-impact`, bỏ `widen authority` (chỉ giữ "không hạ chuẩn nghiệm thu"), gộp destructive + hard-to-reverse thành "xóa khó hồi". INFERENCE: "Giữ nguyên danh sách" là nói quá; phải ghi là rút gọn/gộp.
2. FACT — LUẬT 02, điều kiện nguồn dòng 444-445 là "Fresh-check relevant state before mutation when it may have changed" (chỉ khi có thể đã đổi). FACT: GIAIDAP viết thành kiểm trạng thái thật trước khi sửa, không điều kiện. INFERENCE: Đây là khái quát hoá chưa khai, mức nhẹ.
3. FACT — LUẬT 03, map ghi "không thêm ý mới" cho phần scope-matched, nhưng nguồn dòng 567-571 liệt kê acceptance cần: branch/base/head, live runtime, visual, real user/business workflow, source fidelity, persistence, release-package transport, provider/host, Owner-visible acceptance. FACT: GIAIDAP thu hẹp thành "runtime thật / nội dung thật / quy trình thật". INFERENCE: Thu hẹp này chưa được ghi là thu hẹp (bảng chỉ ghi rút danh sách evidence class, không ghi thu hẹp danh sách acceptance).
4. FACT — LUẬT 07, map ghi "Việt hoá, không thêm ý mới": nguồn đã dẫn chỉ có câu evidence durable/queryable (dòng 1523-1524) và "Experience cannot widen permissions" (dòng 286, về experience). FACT: GIAIDAP khái quát thành mọi nội dung đọc được (file, web, output tool, ý kiến chuyên gia) đều là dữ liệu, và thêm "không tự cấp công cụ/phê duyệt". INFERENCE: Khái quát hoá từ experience sang mọi nội dung + thêm công cụ/phê duyệt là phần tự chế chưa khai.
5. FACT — LUẬT 08, map không ghi việc bỏ "target project/workstream": nguồn dòng 470-471 yêu cầu prompt nêu "target project/workstream, destination/tool". FACT: GIAIDAP chỉ nêu "đích (tool/chat)", không nêu project/workstream. FACT: Quy tắc first-line của nguồn dòng 474-484 và 498-501 yêu cầu first line là `<PROJECT> — <bounded task/outcome>`, không phải routing boilerplate, và CHAT_TITLE phải bằng first line; GIAIDAP chỉ viết "(dòng đầu = tiêu đề người đọc được)", làm mất format PROJECT và lệnh cấm boilerplate. INFERENCE: Hai điểm này chưa khai (PLAN_REFERENCE và khối ARENA đã khai bỏ thì không tính ở đây).
6. FACT — LUẬT 11, xem B2: bỏ CANDIDATE/VERIFIED, quy tắc ngày kiểm + hạn cho dữ kiện dễ cũ, và quy tắc chuyển đổi mới-thay-cũ — cả ba đều chưa có trong ghi chú bảng (bảng chỉ ghi thêm DEPRECATED + 3 cột).
7. FACT — LUẬT 13 / header LAW/00: nguồn có 9 supreme law được đánh số (1 dòng 428, 2 dòng 438, 3 dòng 444, 4 dòng 449, 5 dòng 461, 6 dòng 468, 7 dòng 504, 8 dòng 548, 9 dòng 586 `EXECUTOR_INPUT_FORMAT_AND_ARTIFACT_TRANSPORT_FIDELITY`). FACT: LAW/00 ghi anchors là "Supreme laws 1-8" (8 mục), không có LUẬT nào tương ứng với supreme law 9 (dòng 586), và không có ghi chú nào giải thích vì sao loại supreme law 9. INFERENCE: Đây là lệch phạm vi chưa khai — hoặc phải thêm LUẬT cho law 9, hoặc ghi rõ loại có chủ ý kèm lý do.
8. FACT — Header LAW/00 ghi "RULE 01-21 … (22 mục RULE)". FACT: Đếm heading `### RULE ` trong notebook cho đúng 21 mục (RULE 01 dòng 1218 đến RULE 21 dòng 2616). INFERENCE: Số 22 là sai đếm, phải sửa thành 21.
9. FACT — Header LAW/00 ghi anchors gồm RULE 01-21, nhưng nhiều RULE không được LUẬT nào dẫn (ví dụ RULE 06 dòng 1289, RULE 09 dòng 1318, RULE 10 dòng 1324, RULE 13 dòng 1416, RULE 15 dòng 1462, RULE 17 dòng 1660, RULE 18 dòng 1742, RULE 19 dòng 1816, RULE 20 dòng 2357). INFERENCE: Danh sách anchors nói quá phạm vi thực dùng; phải ghi anchors thực dùng, hoặc ghi rõ các RULE còn lại là ngoài phạm vi LUẬT 01-14.
10. FACT — LUẬT 14, map ghi "Không thêm ý mới": LAW ghi báo cáo khi có "ngoại lệ / blocker / quyết định cần Owner". FACT: Nguồn RULE 12 dòng 1403-1404 chỉ có `PROGRESS_REPORTING=EXCEPTIONS_ONLY`, và Supreme laws 5 dòng 461-467 chỉ nói dừng khi outcome đã proven. INFERENCE: "quyết định cần Owner" là trigger báo cáo thứ ba, chưa khai (mức nhẹ, có thể biện minh là một dạng ngoại lệ, nhưng phải ghi rõ).
11. FACT — LUẬT 10, ghi chú bảng tự mâu thuẫn: vừa ghi "BỎ PR_HEAD_TREE" vừa ghi "GIAIDAP viết tắt 'TREE'" trong khi LAW vẫn giữ TREE. Xem B2. INFERENCE: Phải sửa ghi chú thành "ĐỔI TÊN", không phải "BỎ".
12. INFERENCE — Mâu thuẫn nội bộ GIAIDAP (không phải lệch nguồn, nhưng ảnh hưởng LUẬT 12): KB/INDEX.md trong cùng PR ghi bước không khớp là "mở RUNS/<4 số>-<slug>/, tự tìm, ghi kết quả, rồi thêm dòng vào bảng", trong khi LUẬT 12 ghi không khớp là "tự tìm + suy nghĩ, rồi GHI LẠI mục KB mới" (không nhắc RUN). INFERENCE: Hai văn bản trong cùng PR mô tả hai quy trình khác nhau cho cùng trường hợp không khớp; phải thống nhất một quy trình.

## B4_RANH_GIỚI_B

- FACT: Trong PROTOCOL/multi-brain-loop.md §2, B chỉ nhận `QUESTION.md + A.md`, và "Không được xem" gồm: C, kết luận của Owner, chat của A, tài liệu ngoài 2 file. FACT: §3 ghi nếu một vai đã thấy tài liệu ngoài phạm vi thì ghi rõ trong INPUT_REF (ví dụ `+ extra: ...`) và đánh dấu `CONTAMINATED=YES`, Owner quyết định mở RUN mới.
- FACT: §0 ghi luật là meta: mọi vai đều phải đọc LAW/00 để phát biên lai, và "việc đọc luật không tính là nội dung bài toán và không được dùng để gợi ý kết quả". INFERENCE: Theo chính protocol, việc B đọc LAW/00 không tính là rò rỉ nội dung bài toán — nhưng đó là ngoại lệ do protocol tự đặt ra, không phải là B chỉ thấy đúng 2 file.
- FACT: §5 yêu cầu B.md có mục "NGUỒN ĐỐI LẬP — nguồn mâu thuẫn với A", trong khi §2 cấm B xem tài liệu ngoài 2 file. INFERENCE: Protocol tự mâu thuẫn ở điểm này: B không thể đưa nguồn đối lập ngoài QUESTION/A mà vẫn tuân thủ giới hạn input, trừ khi nguồn đối lập đã nằm trong QUESTION/A.
- INFERENCE — Kết luận B4: Bản thân protocol KHÔNG cho B thấy quá nhiều trong một RUN bình thường — giới hạn 2 file là chặt. Nhưng B trong task này KHÔNG phải là B của một RUN bình thường: B ở đây được packet giao xem PR1 (LAW + map + protocol) và notebook thượng nguồn, tức là vượt xa QUESTION+A. Do đó, nếu đánh giá B.md này bằng tiêu chuẩn RUN của protocol, nó phải được ghi là `CONTAMINATED=YES` (extra: LAW/00, provenance map, multi-brain-loop, P2P notebook, các file PR khác) và Owner phải quyết định xem B.md này là "kiểm độc lập luật" (phạm vi do packet định, tách khỏi RUN) hay là B của một RUN (khi đó không được dùng làm B RUN). INFERENCE: B không được giấu việc đã thấy các file này; header INPUT_REF ở đầu B.md này chính là bản khai extra đó.
- FACT: Protocol không cho B thấy kết luận của Owner hay C — và B.md này cũng không dùng kết luận Owner hay C nào, vì không có C nào trong INPUT. INFERENCE: Không có rò rỉ theo hướng C→B hay Owner→B trong task này; rò rỉ duy nhất là rò rỉ về phạm vi (B luật-verifier thấy nhiều hơn B RUN-challenger).

## B5_LAW_CHECK_SÓT

FACT: Phạm vi quét: toàn bộ cây PR head (9 file): AGENTS.md, README.md, LAW/00-PROVENANCE-MAP.md, LAW/00-SUPREME-LAW.md, PROTOCOL/multi-brain-loop.md, PROTOCOL/arena-agent-mode.md, PROTOCOL/handoff-packet.md, KB/INDEX.md, RUNS/README.md. FACT: Mọi lần xuất hiện `LAW_CHECK` trong 9 file đều là mẫu/instruction/checklist, không phải biên lai đã phát cho một vai cụ thể:

- FACT: AGENTS.md dòng 18: mẫu `LAW_CHECK=PASS | SOURCE=LAW/00-SUPREME-LAW.md | SOURCE_SHA256=<SHA256> | DATE=<YYYY-MM-DD>`; dòng 24: mẫu BLOCKED; dòng 29: nếu không tính được thì ghi `UNKNOWN`.
- FACT: LAW/00-SUPREME-LAW.md dòng 21: mẫu `LAW_CHECK=PASS | SOURCE=<nguồn thật> | SOURCE_SHA256=<sha nội dung> | DATE=<ngày>`.
- FACT: PROTOCOL/multi-brain-loop.md dòng 63: ví dụ header `LAW_CHECK: PASS | SOURCE=LAW/00-SUPREME-LAW.md | SOURCE_SHA256=<SHA256> | DATE=2026-10-26`; dòng 71: mẫu.
- FACT: Các file còn lại chỉ nhắc "phát LAW_CHECK" (AGENTS.md dòng 55, README.md dòng 22, PROTOCOL/arena-agent-mode.md dòng 157 checklist, PROTOCOL/handoff-packet.md dòng 30/48/67 điều kiện dừng) mà không chứa dòng LAW_CHECK nào.

INFERENCE: Vì vậy, trong cây PR, **không có biên lai LAW_CHECK cụ thể nào bị thiếu SOURCE_SHA256** — vì không có biên lai cụ thể nào cả; chỉ có mẫu. INFERENCE: Nhưng điều đó cũng có nghĩa là PR1 hiện không chứa một biên lai LAW_CHECK đã phát nào để kiểm; biên lai duy nhất có thể kiểm là biên lai của B trong B.md này (xem header) và biên lai của Writer nếu có trong PR description/comments — phần đó B chưa kiểm (xem UNKNOWN).

FACT — Lỗ hổng mẫu cần sửa (không phải là "sót" theo nghĩa thiếu sha trong một biên lai cụ thể, nhưng là sót về thiết kế mẫu): LAW/00 §0 và AGENTS.md dòng 29 cho phép `SOURCE_SHA256=UNKNOWN` khi không tính được. INFERENCE: Một biên lai PASS với SOURCE_SHA256=UNKNOWN sẽ vẫn đúng mẫu mà không chứng minh được đã đọc đúng file nào — mẫu này làm suy yếu chính mục đích của B5. Tương tự, ví dụ header trong multi-brain-loop.md dòng 63 dùng placeholder `<SHA256>` mà không ghi rõ là TEMPLATE; nếu một file A/B/C copy nguyên ví dụ đó thì sẽ có một "biên lai" placeholder trông như thật.

**Đề xuất B5:** (a) Sửa LAW/00 §0 và AGENTS.md: PASS chỉ được phát khi SOURCE_SHA256 là SHA256 thật đã tính; nếu không tính được thì phát BLOCKED, không phát PASS với UNKNOWN. (b) Ghi rõ mọi ví dụ LAW_CHECK trong repo là TEMPLATE, không phải biên lai đã phát.

## UNKNOWN

- UNKNOWN: Trạng thái PR #1 (open/draft/merged, tiêu đề, mô tả, comments) — B không kiểm qua pull_request_read vì tool cũ `get_pull_request`/`get_pull_request_files` không còn được server advertise, và `pull_request_read` là call-tool cần approval riêng; B chỉ fetch file qua `refs/pull/1/head`. INFERENCE: Head ref 84ae8b3… chỉ chứng minh nhánh PR tồn tại tại thời điểm fetch, không chứng minh PR đang open hay đã merge.
- UNKNOWN: Notebook thượng nguồn có đổi sau thời điểm fetch 2026-10-26 hay không — blob/SHA ở trên chỉ đúng tại thời điểm fetch.
- UNKNOWN: Owner có chấp nhận tiêu chuẩn "schema/artifact riêng = NEW" cho LUẬT 11 hay không, và có chấp nhận đổi LUẬT 12 thành NEW hay không — đây là OWNER_CONFIRMATION_REQUIRED, B không tự quyết thay Owner.
- UNKNOWN: Việc loại supreme law 9 (dòng 586) và các RULE không được dẫn khỏi LUẬT 01-14 là chủ ý hay sót — không có ghi chú nào trong map/LAW giải thích.
- UNKNOWN: Hành vi UI thực tế của Arena về tiêu đề first-line — nhưng theo ràng buộc của packet, B ghi rõ: NGUỒN cho quy tắc first-line là P2P notebook (Supreme laws 6 dòng 474-502 và RULE 02 dòng 1239-1258), KHÔNG phải tài liệu Arena. FACT: PROTOCOL/arena-agent-mode.md dòng 113 ghi không tìm thấy tài liệu chính thức của Arena nói Arena tự lấy dòng đầu làm tiêu đề — điều đó nói về sản phẩm Arena, không làm mất nguồn P2P của quy tắc vận hành GIAIDAP. INFERENCE: Không được đóng UNKNOWN này bằng cách viện dẫn "tài liệu Arena"; nếu đóng, phải viện dẫn notebook.
- UNKNOWN: Các lệch mức nhẹ ở B3 (LUẬT 02 điều kiện, LUẬT 03 thu hẹp acceptance, LUẬT 14 trigger Owner) là chủ ý rút gọn hay vô ý — B chỉ chứng minh được văn bản khác nguồn, không chứng minh được ý định của Writer.
- UNKNOWN: B chưa kiểm nội dung PR description/comments có chứa LAW_CHECK của Writer hay không (xem UNKNOWN đầu tiên) — do đó B không kết luận Writer đã phát hay chưa phát biên lai hợp lệ ngoài file.

## ĐỀ_XUẤT_SỬA_TỐI_THIỂU

INFERENCE: Chỉ sửa văn bản, không viết lại kiến trúc, không merge. Thứ tự sửa:

1. FACT — Sửa tổng kết bảng: đổi `NEW=0` thành `NEW=1 (LUẬT 12, cơ chế tra cứu)` và `DERIVED=13` (hoặc `DERIVED=12 + DERIVED_WITH_NEW_PARTS=2` nếu muốn giữ chi tiết cho LUẬT 05/11 — nhưng tối thiểu phải ghi NEW>=1). Sửa câu "0 dòng NEW: … chưa tìm ra luật nào hoàn toàn không có nguồn" vì LUẬT 12 đã tìm ra.
2. FACT — LUẬT 12: đổi LOẠI thành `NEW` (cơ chế), ghi PHẦN_TỰ_CHẾ như ở B2, và sửa điều kiện ghi mới cho đúng nguồn (chỉ khi bài học tái dùng rõ ràng; ROUTINE_SUCCESS thì NONE, dòng 292/298-299).
3. FACT — LUẬT 11, 09, 05, 10: giữ LOẠI DERIVED nhưng thêm PHẦN_TỰ_CHẾ đúng như văn bản đề xuất ở B2 vào bảng (và, nếu LAW/00 có ghi chú provenance theo luật, thêm vào đó luôn).
4. FACT — Sửa các ghi chú bảng ở B3: LUẬT 01 (ghi rút gọn/gộp danh sách, không phải giữ nguyên), LUẬT 02 (ghi bỏ điều kiện "when it may have changed"), LUẬT 03 (ghi thu hẹp acceptance), LUẬT 07 (ghi khái quát hoá từ experience sang mọi nội dung + thêm công cụ/phê duyệt), LUẬT 08 (ghi bỏ project/workstream và làm mất format PROJECT + cấm boilerplate), LUẬT 10 (đổi "BỎ PR_HEAD_TREE" thành "ĐỔI TÊN"), LUẬT 14 (ghi thêm trigger "quyết định cần Owner").
5. FACT — Sửa header LAW/00: (a) "Supreme laws 1-8" → ghi rõ supreme law 9 (dòng 586) bị loại có chủ ý kèm lý do, hoặc thêm LUẬT cho nó; (b) "(22 mục RULE)" → "(21 mục RULE)"; (c) danh sách anchors RULE 01-21 → chỉ liệt kê RULE thực dùng, hoặc ghi rõ các RULE còn lại ngoài phạm vi LUẬT 01-14.
6. FACT — Thống nhất LUẬT 12 với KB/INDEX.md: một quy trình duy nhất cho trường hợp không khớp (mở RUN rồi thêm dòng, hoặc tự ghi trực tiếp — Owner chọn một).
7. FACT — Sửa mẫu LAW_CHECK (B5): PASS chỉ khi SOURCE_SHA256 thật; không tính được thì BLOCKED, không PASS với UNKNOWN; ghi rõ mọi ví dụ LAW_CHECK là TEMPLATE.
8. FACT — B.md này phải được ghi INPUT_REF đầy đủ như header (extra files) và, nếu Owner muốn dùng nó như B của một RUN, phải ghi `CONTAMINATED=YES` theo §3 của multi-brain-loop.md và mở RUN mới cho B RUN thật; nếu Owner dùng nó như kiểm luật độc lập thì ghi rõ nó không phải B RUN.

INFERENCE: Sau khi 8 điểm trên được sửa trong cùng một commit trên nhánh PR1 (không force, không merge) và B kiểm lại diff đó, PENDING_VERIFICATION mới được gỡ thành VERIFIED cho phạm vi bảng ánh xạ + LAW/00. FACT: Cho đến lúc đó, trạng thái đúng vẫn là PENDING_VERIFICATION, và B.md này không tự nâng mình thành VERIFIED.

=== HẾT ===
