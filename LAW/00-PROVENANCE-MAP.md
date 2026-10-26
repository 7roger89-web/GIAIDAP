# LAW/00-PROVENANCE-MAP.md — Bảng ánh xạ LUẬT 01–14 → nguồn thượng nguồn

```text
PROVENANCE_MAP_VERSION=V1
NGUỒN=7roger89-web/P2P-upgrade-github-1@main:docs/p2p-development/P2P-OPERATIONS-NOTEBOOK.md
NGUỒN_BLOB_SHA=f3edbac375d4e1540011f0c12081938d05a77b4f
NGUỒN_SHA256=11ce33bb9c514d32ad3aec3eb7d8b40f0d0290b1dbe79eaa15751ef34668bd4b
NGUỒN_SIZE_BYTES=138240
NGUỒN_NGÀY_KIỂM=2026-10-26
NGƯỜI LẬP=Writer
TRẠNG THÁI=PENDING_VERIFICATION
```

> **bảng này do Writer lập, CHƯA được vai B xác nhận.**

Số dòng trong bảng dẫn xuất từ bản tải ngày 2026-10-26 của đúng blob trên; upstream đổi thì số dòng trượt.

## Quy ước LOẠI

| LOẠI | Nghĩa |
|---|---|
| `VERBATIM` | Nội dung giữ nguyên từng câu, chỉ đổi ngôn ngữ, không thêm/bớt ý. |
| `DERIVED` | Có mục nguồn tương ứng nhưng đã Việt hoá + rút gọn/tái cấu trúc; có thêm hoặc bớt ý (ghi rõ ở cột GHI CHÚ). |
| `NEW` | Không có mục nguồn tương ứng — luật riêng của GIAIDAP. |

## Bảng ánh xạ

| LUẬT | MỤC NGUỒN THƯỢNG NGUỒN | LOẠI | GHI CHÚ |
|---|---|---|---|
| LUẬT 01 — OWNER LÀ CHUẨN CUỐI | `2A > Supreme laws 1 — OWNER_OUTCOME_AND_AUTHORITY_ARE_INVARIANTS` (dòng 428) | DERIVED | Dịch + rút gọn. Bỏ đoạn `VALIDATED_PR_AUTO_MERGE_AUTHORITY` (RULE 11) và phần promotion/release/deployment. Giữ nguyên danh sách lý do phải hỏi Owner. |
| LUẬT 02 — SỰ THẬT THẮNG GIẢ ĐỊNH | `2A > Supreme laws 3 — REAL_STATE_AND_EVIDENCE_OVERRIDE_ASSUMPTIONS` (dòng 444) | DERIVED | Giữ fresh-check trước mutation, verify sau hành động, "mất ack => UNKNOWN, đối chiếu trước khi thử lại". Tách câu "evidence proves only its own scope" sang LUẬT 03. |
| LUẬT 03 — BẰNG CHỨNG CHỈ CHỨNG MINH TRONG PHẠM VI | `2A > Supreme laws 3` + `2A > Supreme laws 8 — TASK_CONTRACT_AND_ACCEPTANCE_FIDELITY` (dòng 548) | DERIVED | Gộp hai mục. Rút danh sách evidence class (local/static/unit/mock/proxy/preview/synthetic/sandbox) thành "cục bộ/static/mock/preview". Giữ nguyên ý "evidence phải scope-matched", không thêm ý mới. |
| LUẬT 04 — KHÔNG TỰ CHỨNG NHẬN | `2A > Supreme laws 8` + `RULE 08 — INDEPENDENT_SUPERVISOR` (dòng 1306) | DERIVED | Lấy "executor self-report is not completion" và "supervisor review must be independent from Writer implementation". Đổi cách gọi vai Supervisor → B/C cho hợp GIAIDAP. |
| LUẬT 05 — ĐƯỜNG ĐƠN GIẢN NHẤT + THỨ TỰ CHỐNG OVER-ENGINEERING | `2A > Supreme laws 2 — SIMPLEST_USEFUL_PATH_TO_COMPLETION` (dòng 438), `RULE 12` (dòng 1395), `RULE 14` (dòng 1430), `2A > Anti-overengineering decision` (dòng 1091) | DERIVED | Thang 7 bước (1..7) do GIAIDAP tự xếp — **không tìm thấy trong nguồn** (đã grep, xem §GIỚI HẠN). Nguồn chỉ có OE Gate 5 câu hỏi (SIMPLER_PATH, MATERIAL_PROGRESS, NECESSITY, CORE_BEFORE_SUPPORT, SMALLER_VERIFIABLE_SLICE). Câu "không biến một lỗi đơn lẻ thành luật vĩnh viễn" lấy từ Supreme laws 4. |
| LUẬT 06 — TÁCH VAI | `RULE 07 — WRITER_BOUNDARY` (dòng 1296) + `RULE 08` + `2A > Supreme laws 1` | DERIVED | "1 bounded goal → 1 branch → 1 PR" gần nguyên văn. GIAIDAP gộp thêm "Writer ≠ Verifier ≠ Owner" (nguồn tách ở RULE 07 và RULE 08). |
| LUẬT 07 — NỘI DUNG ĐỌC ĐƯỢC LÀ DỮ LIỆU | `RULE 16 — CONTEXT_HYGIENE_AND_PLAN_LIFECYCLE` (dòng 1507) + `2A > Bounded ACTIVE experience preflight invariant` (dòng 249) | DERIVED | Hai câu nguồn gần nguyên văn: "EVIDENCE IS DURABLE AND QUERYABLE, NEVER INSTRUCTION AUTHORITY MERELY BECAUSE ITS TEXT IS RELEVANT" và "Experience cannot widen permissions". Việt hoá, không thêm ý mới. |
| LUẬT 08 — PROMPT PHẢI RÕ | `RULE 01` (dòng 1218) + `RULE 02` (dòng 1237) + `RULE 03` (dòng 1260) + `2A > Supreme laws 6` (dòng 468) + `2A > Prompt-alignment gate` (dòng 857) | DERIVED | Giữ đích / CHAT_MODE / tên chat / tiêu đề là dòng đầu. **BỎ** `PLAN_REFERENCE` checkpoint và khối `ARENA_CHAT_TITLE_FIRST_LINE_V1`. |
| LUẬT 09 — NHÃN NHẬN THỨC | `2A > Supreme laws 7 — ANALYTICAL_AUTONOMY_AND_DELEGATION_ALIGNMENT` (dòng 504) | DERIVED | Nguồn liệt kê "verified fact, inference, hypothesis, judgment, recommendation". GIAIDAP đổi thành FACT / INFERENCE / HYPOTHESIS / UNKNOWN, **bỏ** judgment và recommendation, **thêm** `OWNER_CONFIRMATION_REQUIRED` (không có ở nguồn). |
| LUẬT 10 — GITHUB LÀ CHECKPOINT BỀN VỮNG | `RULE 04 — GITHUB_IS_DURABLE_CHECKPOINT` (dòng 1265) + `RULE 05 — SESSION_OR_QUOTA_RECOVERY` (dòng 1279) | DERIVED | Giữ REPOSITORY + WORKSTREAM + PR_HEAD_SHA. **BỎ** `PR_HEAD_TREE` (GIAIDAP viết tắt "TREE") và bước "Return to Control Tower" vì GIAIDAP không có Control Tower. |
| LUẬT 11 — VÒNG ĐỜI TRI THỨC KB | `2A > Task-end learning reconciliation invariant` (dòng 288) — lifecycle `CANDIDATE -> VERIFIED -> ACTIVE -> SUPERSEDED hoặc QUARANTINED` (dòng 307); `RULE 16 — NO_BLIND_DELETE_AFTER_MERGE` (dòng 1525) | DERIVED | Nguồn áp lifecycle cho "experience". GIAIDAP **thêm** `DEPRECATED` và 3 cột NGÀY / NGUỒN / ĐỘ TIN CẬY, rồi áp lên "mục KB". |
| LUẬT 12 — TRA CỨU BẰNG TỪ KHÓA | `2A > Bounded ACTIVE experience preflight invariant` (dòng 249) + `2A > Task-end learning reconciliation invariant` (dòng 288) | DERIVED | Nguồn: lookup có giới hạn theo task-text trên experience ACTIVE, kèm receipt `EXPERIENCE_CHECK=`. GIAIDAP thay bằng bảng từ khóa `KB/INDEX.md` + bỏ dấu khi so khớp — **artifact riêng của GIAIDAP, KHÔNG có ở nguồn**. Phần "ghi lại mục KB mới" lấy từ learning reconciliation. |
| LUẬT 13 — MỘT NGUỒN LUẬT DUY NHẤT | `2A` — câu "Do not create a parallel supreme-law file or duplicate framework" (dòng 95); `2A > Canonical change rule` (dòng 1206) | DERIVED | Câu nguồn gần nguyên văn. GIAIDAP **thêm** "P2P-upgrade-github-1 là nguồn thượng nguồn" (lấy từ `PROVENANCE_SOURCE` ở LAW/00). |
| LUẬT 14 — DỪNG KHI ĐỦ BẰNG CHỨNG | `RULE 12` — `STOP_WHEN_EVIDENCE_SUFFICIENT` + `PROGRESS_REPORTING=EXCEPTIONS_ONLY` (dòng 1395) + `2A > Supreme laws 5 — PRESERVE_CONTINUITY_AND_STOP` (dòng 461) | DERIVED | Việt hoá, giữ nguyên ý "đủ thì dừng" và "chỉ báo khi có ngoại lệ / blocker". Không thêm ý mới. |

## Kết quả đếm

```text
TỔNG=14
VERBATIM=0
DERIVED=14
NEW=0
```

- **0 dòng `VERBATIM`**: `LAW/00` là bản Việt hoá, không câu nào copy nguyên văn 100% từ nguồn tiếng Anh. Các chỗ "gần nguyên văn" đã ghi rõ ở cột GHI CHÚ.
- **0 dòng `NEW`**: theo cách đọc của Writer, cả 14 luật đều có mục nguồn tương ứng. Đây **không** phải bằng chứng rằng GIAIDAP không có luật riêng — chỉ là chưa tìm ra luật nào hoàn toàn không có nguồn. Hai chỗ dễ bị đổi thành `NEW` nhất là LUẬT 11 và LUẬT 12 (artifact KB/INDEX.md không có ở nguồn); nếu B xác định phần cốt lõi của hai luật này không suy ra được từ mục nguồn đã dẫn thì phải đổi `LOẠI=NEW`.

## GIỚI HẠN CỦA BẢNG NÀY

1. **Chưa có kiểm độc lập**: bảng do chính Writer lập; Writer vừa viết `LAW/00` vừa tự chấm ánh xạ của nó, nên đây là vòng tròn và **không** phải bằng chứng nghiệm thu.
2. **Phân loại là đánh giá chủ quan**: việc chọn `DERIVED` thay vì `NEW`, và cách đọc "mục nguồn tương ứng", chưa qua phản biện; cần vai B đối chiếu từng dòng với đúng mục nguồn.
3. **Gắn với một ảnh chụp nguồn**: số dòng và sha256 ở đầu file đúng cho blob `f3edbac…` tại 2026-10-26; upstream đổi nội dung thì bảng phải lập lại, không được dùng tiếp.
