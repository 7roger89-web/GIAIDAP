# LAW/00-PROVENANCE-MAP.md — Bảng ánh xạ LUẬT 01–15 → nguồn thượng nguồn

```text
PROVENANCE_MAP_VERSION=V4
NGUỒN=7roger89-web/P2P-upgrade-github-1@main:docs/p2p-development/P2P-OPERATIONS-NOTEBOOK.md
NGUỒN_BLOB_SHA=f3edbac375d4e1540011f0c12081938d05a77b4f
NGUỒN_SHA256=11ce33bb9c514d32ad3aec3eb7d8b40f0d0290b1dbe79eaa15751ef34668bd4b
NGUỒN_SIZE_BYTES=138240
NGUỒN_NGÀY_KIỂM=2026-10-26
NGƯỜI LẬP=Writer
TRẠNG THÁI=PENDING_VERIFICATION
SỬA_LẦN_CUỐI=2026-10-26 — V4: chỉ sửa dòng LUẬT 08 (theo D4: Owner cho phép sửa riêng LUẬT 08); 14 dòng còn lại giữ nguyên như V3.
LỊCH_SỬ_BẢN=V1 (14 dòng) → V2 (thêm LUẬT 15 theo Q2) → V3 (sửa dòng LUẬT 12 theo D1) → V4 (sửa dòng LUẬT 08 theo D4).
```

> **bảng này do Writer lập, CHƯA được vai B xác nhận cho bản V4.**
> B mới kiểm bản V1 (head `84ae8b3`) và kết luận `PASS_WITH_FIXES`; bản V2/V3/V4 chưa qua kiểm lại. Xem `RUNS/0000-pr1-verify/B.md`.

Số dòng trong bảng dẫn xuất từ bản tải ngày 2026-10-26 của đúng blob trên; upstream đổi thì số dòng trượt.

## Quy ước cột LOẠI

`LOẠI` mô tả **cái LÕI** của luật, không mô tả phần thêm.

| LOẠI | Nghĩa |
|---|---|
| `VERBATIM` | Lõi giữ nguyên từng câu, chỉ đổi ngôn ngữ, không thêm/bớt ý. |
| `DERIVED` | Lõi có mục nguồn tương ứng nhưng đã Việt hoá + rút gọn/tái cấu trúc; phần thêm nằm ở cột `PHẦN_TỰ_CHẾ`. |
| `NEW` | Lõi **không** có mục nguồn tương ứng — luật riêng của GIAIDAP. |

Cột `PHẦN_TỰ_CHẾ` liệt kê phần GIAIDAP tự thêm/đổi so với nguồn. Không có phần tự chế thì ghi `KHÔNG`.

## Bảng ánh xạ

| LUẬT | MỤC NGUỒN THƯỢNG NGUỒN | LOẠI | PHẦN_TỰ_CHẾ | GHI CHÚ |
|---|---|---|---|---|
| LUẬT 01 — OWNER LÀ CHUẨN CUỐI | `2A > Supreme laws 1 — OWNER_OUTCOME_AND_AUTHORITY_ARE_INVARIANTS` (dòng 428) | DERIVED | Danh sách lý do phải hỏi Owner bị **rút gọn và gộp** (nguồn tách "outcome, authority, material cost, security/privacy/business-impact, production, destructive, infrastructure-commitment, hard-to-reverse" thành 6 nhóm của GIAIDAP). Bỏ `VALIDATED_PR_AUTO_MERGE_AUTHORITY` và phần promotion/release/deployment. | Lõi giữ ("Owner là chuẩn cuối", "không hạ chuẩn nghiệm thu để cho xanh"), nhưng câu chữ **không** nguyên văn. |
| LUẬT 02 — SỰ THẬT THẮNG GIẢ ĐỊNH | `2A > Supreme laws 3 — REAL_STATE_AND_EVIDENCE_OVERRIDE_ASSUMPTIONS` (dòng 444) | DERIVED | Bỏ điều kiện **"when it may have changed"** của nguồn, nên GIAIDAP yêu cầu fresh-check **mọi** lần trước mutation (rộng hơn nguồn). | Lõi giữ: kiểm trước khi sửa, kiểm sau khi hành động, mất ack => UNKNOWN. |
| LUẬT 03 — BẰNG CHỨNG CHỈ CHỨNG MINH TRONG PHẠM VI | `2A > Supreme laws 3` (dòng 444) + `2A > Supreme laws 8 — TASK_CONTRACT_AND_ACCEPTANCE_FIDELITY` (dòng 548) | DERIVED | **Thu hẹp acceptance**: nguồn liệt kê branch/base/head, durable PR identity, visual likeness, business fit, source fidelity, persistence, release-package transport, provider/host behavior; GIAIDAP rút còn "runtime thật / nội dung thật / quy trình thật". Danh sách evidence class cũng rút gọn. | Lõi giữ: evidence chỉ chứng minh trong phạm vi của nó. |
| LUẬT 04 — KHÔNG TỰ CHỨNG NHẬN | `2A > Supreme laws 8` (dòng 548) + `RULE 08 — INDEPENDENT_SUPERVISOR` (dòng 1306) | DERIVED | Đổi cách gọi vai: Supervisor/WRITER_RECEIPT ≠ SUPERVISOR_RECEIPT → B/C của GIAIDAP. | Lõi giữ: self-report không phải bằng chứng; review phải độc lập với người làm. |
| LUẬT 05 — ĐƯỜNG ĐƠN GIẢN NHẤT + THỨ TỰ CHỐNG OVER-ENGINEERING | `2A > Supreme laws 2 — SIMPLEST_USEFUL_PATH_TO_COMPLETION` (dòng 438), `RULE 12` (dòng 1395), `RULE 14` (dòng 1430), `2A > Anti-overengineering decision` (dòng 1091) | DERIVED | **Thang 7 bước (1..7) là của GIAIDAP**, không tìm thấy trong nguồn; nguồn chỉ có OE Gate 5 câu hỏi (SIMPLER_PATH, MATERIAL_PROGRESS, NECESSITY, CORE_BEFORE_SUPPORT, SMALLER_VERIFIABLE_SLICE). Hai bậc đầu ("trả lời/không code", "cấu hình") cũng do GIAIDAP tự thêm. | Câu "không biến một lỗi đơn lẻ thành luật vĩnh viễn" lấy từ Supreme laws 4. |
| LUẬT 06 — TÁCH VAI | `RULE 07 — WRITER_BOUNDARY` (dòng 1296) + `RULE 08` (dòng 1306) + `2A > Supreme laws 1` (dòng 428) | DERIVED | Ghép "Writer ≠ Verifier ≠ Owner" từ hai RULE khác nhau; nguồn không có câu này ở một chỗ. | "1 bounded goal → 1 branch → 1 PR" gần nguyên văn RULE 07. |
| LUẬT 07 — NỘI DUNG ĐỌC ĐƯỢC LÀ DỮ LIỆU | `RULE 16 — CONTEXT_HYGIENE_AND_PLAN_LIFECYCLE` (dòng 1507) + `2A > Bounded ACTIVE experience preflight invariant` (dòng 249) | DERIVED | **Khái quát hoá** từ "evidence/experience" sang "file, web, output tool, ý kiến chuyên gia"; **thêm** vế "không tự cấp quyền/công cụ/phê duyệt", nguồn chỉ nói về permission của experience. | Hai câu nguồn gần nguyên văn: "EVIDENCE IS DURABLE AND QUERYABLE, NEVER INSTRUCTION AUTHORITY…" và "Experience cannot widen permissions". |
| LUẬT 08 — PROMPT PHẢI RÕ | `RULE 01` (dòng 1218) + `RULE 02` (dòng 1237) + `RULE 03` (dòng 1260) + `2A > Supreme laws 6 — PROMPT_TITLE_DESTINATION_AND_PLAN_STATE_ARE_EXPLICIT` (dòng 468–495; khối `ARENA_CHAT_TITLE_FIRST_LINE_V1` dòng 498–501) + `2A > Prompt-alignment gate` (dòng 857) | DERIVED | **Vá lần 7 (D4) khôi phục các phần trước đây bị mất**: target project/workstream (dòng 470); format dòng đầu `<PROJECT> — <bounded task/outcome>` + front-load + cấm boilerplate ở dòng đầu (dòng 474–479); `CHAT_TITLE` = đúng dòng đầu và SAME_CHAT không đổi tên (dòng 483–484); tên khối `ARENA_CHAT_TITLE_FIRST_LINE_V1` (dòng 498–501). **Vẫn `DERIVED`, không lên `VERBATIM`** vì: câu chữ Việt hoá/rút gọn; KHÔNG chép yêu cầu serialize routing metadata ngay sau tiêu đề (`GỬI CHO:` → `PROJECT=` → `CHAT_MODE=` → `CHAT_TITLE=`, dòng 480–484); KHÔNG chép `PLAN_REFERENCE` checkpoint (dòng 485–495). | Phần còn thiếu (PLAN_REFERENCE + thứ tự metadata) là **thiếu so với nguồn**, không phải chủ ý — ghi nhận, chưa vá. |
| LUẬT 09 — NHÃN NHẬN THỨC | `2A > Supreme laws 7 — ANALYTICAL_AUTONOMY_AND_DELEGATION_ALIGNMENT` (dòng 504) | DERIVED | Nguồn có 5 nhãn "verified fact, inference, hypothesis, judgment, recommendation"; GIAIDAP **bỏ judgment + recommendation**, **thêm** `UNKNOWN` và `OWNER_CONFIRMATION_REQUIRED` (không có ở nguồn). | Lõi giữ: tách rõ nhãn, không trộn. |
| LUẬT 10 — GITHUB LÀ CHECKPOINT BỀN VỮNG | `RULE 04 — GITHUB_IS_DURABLE_CHECKPOINT` (dòng 1265) + `RULE 05 — SESSION_OR_QUOTA_RECOVERY` (dòng 1279) | DERIVED | `PR_HEAD_TREE` được **ĐỔI TÊN** thành `TREE` (không phải bỏ). Bỏ bước "Return to Control Tower" — GIAIDAP không có Control Tower. Thay bằng "quay lại checkpoint bền". | Lõi giữ: REPO + WORKSTREAM + PR_HEAD_SHA; chat/PR number không phải thẩm quyền. |
| LUẬT 11 — VÒNG ĐỜI TRI THỨC KB | `2A > Task-end learning reconciliation invariant` (dòng 288) — lifecycle `CANDIDATE -> VERIFIED -> ACTIVE -> SUPERSEDED hoặc QUARANTINED` (dòng 307); `RULE 16 — NO_BLIND_DELETE_AFTER_MERGE` (dòng 1525) | DERIVED | **Thêm** `DEPRECATED` vào lifecycle; **thêm** 3 cột NGÀY / NGUỒN / ĐỘ TIN CẬY; **mở rộng phạm vi** từ "experience" sang "mục KB". | Lõi giữ: cái mới thay cái cũ thì đổi trạng thái, không xóa mù. |
| LUẬT 12 — TRA CỨU BẰNG TỪ KHÓA | — (không có mục nguồn tương ứng). Gần nhất: `2A > Bounded ACTIVE experience preflight invariant` (dòng 249–286) và `2A > Task-end learning reconciliation invariant` (dòng 288–309) | NEW | **Toàn bộ cơ chế là của GIAIDAP**: bảng `KB/INDEX.md` 6 cột (TỪ KHÓA / FILE / STATUS / NGÀY / NGUỒN / ĐỘ TIN CẬY); so khớp từ khóa bỏ dấu, không phân biệt hoa-thường; quy trình không-khớp = **mở `RUNS/<4 số>-<slug>/` rồi mới thêm dòng**; **điều kiện ghi mới = chỉ ghi khi có khả năng tái dùng** (nêu được ít nhất một tình huống tương lai sẽ tra lại, không nêu được thì giữ trong `RUNS/`); và việc ghi **tri thức lĩnh vực** chứ không chỉ bài học từ lỗi. Nguồn chỉ có: lookup có giới hạn trên experience ACTIVE kèm receipt `EXPERIENCE_CHECK=` và learning reconciliation sau task (`REPEATED_OR_MATERIAL_FAILURE \| CLEARLY_REUSABLE_CORRECTION`, dòng 293). | **MỞ RỘNG (khai báo)**: nguồn chỉ giữ bài học từ lỗi (experience lifecycle); GIAIDAP dùng KB để giữ tri thức lĩnh vực dùng lại được, không nhất thiết sinh ra từ lỗi — đây là phần tự chế, khác nguồn. Ba điểm trên nay **nằm ngay trong câu chữ LUẬT 12** (vá lần 6, D1), không còn chỉ ở `KB/INDEX.md` như V2. |
| LUẬT 13 — MỘT NGUỒN LUẬT DUY NHẤT | `2A` — "Do not create a parallel supreme-law file or duplicate framework" (dòng 95); `2A > Canonical change rule` (dòng 1206) | DERIVED | **Thêm** vế "P2P-upgrade-github-1 là nguồn thượng nguồn" (lấy từ `PROVENANCE_SOURCE`, không phải câu của nguồn). | Lõi gần nguyên văn. |
| LUẬT 14 — DỪNG KHI ĐỦ BẰNG CHỨNG | `RULE 12` — `STOP_WHEN_EVIDENCE_SUFFICIENT` + `PROGRESS_REPORTING=EXCEPTIONS_ONLY` (dòng 1395) + `2A > Supreme laws 5 — PRESERVE_CONTINUITY_AND_STOP` (dòng 461) | DERIVED | **Thêm trigger** "quyết định cần Owner" vào điều kiện báo cáo; nguồn chỉ có "exceptions / blocker". | Lõi giữ: đủ thì dừng, không mở việc tùy chọn. |
| LUẬT 15 — ĐỊNH DẠNG ĐẦU VÀO VÀ VẬN CHUYỂN ARTIFACT | `2A > Supreme laws 9 — EXECUTOR_INPUT_FORMAT_AND_ARTIFACT_TRANSPORT_FIDELITY` (dòng 586) | DERIVED | Rút gọn mạnh: bỏ toàn bộ §A–§F chi tiết (Base64 pipeline, chunking, target isolation exception, media type, RULE 19 probe). Giữ 6 câu lõi. | Thêm ở V2 theo quyết định Owner Q2. |

## Kết quả đếm

```text
TỔNG=15
VERBATIM=0
DERIVED=14
NEW=1
```

- `VERBATIM=0`: `LAW/00` là bản Việt hoá, không câu nào copy nguyên văn 100%.
- `NEW=1`: **LUẬT 12** — cơ chế KB/INDEX.md không có ở nguồn (quyết định Owner Q1).
- V2 và V3 có **15** dòng vì LUẬT 15 được thêm theo Q2 (giữ ở V3 theo D2). Con số "NEW=1 / DERIVED=13" trong yêu cầu vá lần 5 là cho bảng 14 luật trước khi thêm LUẬT 15.
- V3 khác V2 ở **đúng một dòng** (LUẬT 12, `PHẦN_TỰ_CHẾ`), theo D1.
- V4 khác V3 ở **đúng một dòng** (LUẬT 08: `MỤC NGUỒN`, `PHẦN_TỰ_CHẾ`, `GHI CHÚ`), theo D4; `LOẠI` vẫn `DERIVED`.

## GIỚI HẠN CỦA BẢNG NÀY

1. **Chưa có kiểm độc lập**: bảng do chính Writer lập; Writer vừa viết `LAW/00` vừa tự chấm ánh xạ của nó, nên đây là vòng tròn và **không** phải bằng chứng nghiệm thu.
2. **Phân loại là đánh giá chủ quan**: ranh giới `DERIVED` và `NEW` do Writer tự đặt, chưa qua phản biện; cần vai B đối chiếu từng dòng với đúng mục nguồn.
3. **Gắn với một ảnh chụp nguồn**: số dòng và sha256 ở đầu file đúng cho blob `f3edbac…` tại 2026-10-26; upstream đổi nội dung thì bảng phải lập lại, không được dùng tiếp.
