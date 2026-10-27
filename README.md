# GIAIDAP

Bộ nhớ chung + sổ luật cho quy trình nhiều AI.

- Chat là nơi làm việc; **sự thật nằm trong repo**.
- Repo giữ điểm hồi sinh, luật, giao thức, sổ phương án đã bác, tri thức và nhật ký chạy. Không dựa vào ký ức của một phiên chat.
- GIAIDAP là **bản chuyển thể** từ [P2P-upgrade-github-1](https://github.com/7roger89-web/P2P-upgrade-github-1), không phải bản sao. Khi bản gốc đổi, rà lại `LAW/00-SUPREME-LAW.md`.
- Provenance của luật hiện là `PENDING_VERIFICATION`; xem khối provenance đầu `LAW/00-SUPREME-LAW.md`. Chưa có bên độc lập xác nhận bản `V4`.

## Các khối

| Khối | Vai trò | File vào |
|---|---|---|
| `STATE.md` | Điểm hồi sinh cho phiên mới: đang ở đâu, hash chuẩn, việc kế tiếp | `STATE.md` |
| `LAW/` | Luật tối thượng, duy nhất + bảng ánh xạ nguồn | `LAW/00-SUPREME-LAW.md` |
| `PROTOCOL/` | Cách vận hành: hồi sinh, Arena, vòng A/B/C, handoff; lớp chứng minh (`kiem.md`) + cách nghĩ trước khi làm (`cach-nghi.md`) | `PROTOCOL/*.md` |
| `REGISTER/` | Sổ phương án đã bị bác — chống tái tranh luận + lịch sử dài hạn (append-only) | `REGISTER/BAC.md`, `REGISTER/LICH-SU.md` |
| `KB/` | Tri thức lĩnh vực tra theo từ khóa + khuôn mẫu | `KB/INDEX.md` |
| `RUNS/` | Mục lục + nhật ký từng phiên chạy | `RUNS/INDEX.md` |
| `scope-reality-check/` | Chế độ suy nghĩ kiểm định thực tế gắn theo vai (không thay luật) | `scope-reality-check/SKILL.md` |

## Luồng hồi sinh

Một model mới ở phiên mới (không có ký ức chat) tiếp việc hoàn toàn từ file trong repo:

1. Đọc `AGENTS.md` → `STATE.md` (biết đang ở đâu) → `LAW/00-SUPREME-LAW.md` (phát `LAW_CHECK` với SHA-256 thật).
2. Theo `PROTOCOL/resume-protocol.md`, kiểm quan hệ tổ tiên `SINH_TỪ_HEAD`, so `sha256sum` của `LAW/00`, `PROTOCOL/*`, `SKILL.md` (không dùng diff-range), đối chiếu `STATE_TRUST=OK|DRIFT` với `RUNS/INDEX.md` + `DECISION.md`, rồi phát `RESUME_CHECK`. Nếu `BLOCKED` => dừng.
3. Đọc `REGISTER/BAC.md` trước mọi đề xuất; chạy skill `scope-reality-check` đúng vai (`ROLE_BOUND` cho B/C, `USER_EXPLICIT` cho A/R).
4. Làm đúng một đơn vị việc bounded => cập nhật `STATE.md` + `RUNS/INDEX.md` (+ `REGISTER/BAC.md` nếu có phương án bị bác) **trong cùng commit** (kỷ luật tự nguyện, không có CI cưỡng chế).

## Lớp chứng minh và cách nghĩ (verification-first)

Hai file `PROTOCOL/` bịt lỗ "kiểm được việc ĐỌC nhưng chưa khai được cách chứng minh VIỆC LÀM":

- `PROTOCOL/kiem.md`: mọi packet mang khối `CÁCH CHỨNG MINH` 4 dòng — `LỆNH` (một dòng shell thật) · `KỲ VỌNG` (máy đọc được) · `ARTIFACT` (file/log để lại) · `NẾU KHÔNG CHẠY ĐƯỢC` (lý do + bằng chứng thay thế) — điền **trước khi làm**.
- Test xanh **chưa đủ**: phải chạy thật; quy tắc này nối LUẬT 03 thành quy trình, không thay LUẬT 03. Việc có ghi/đổi trạng thái phải khai lệnh kiểm trước (`DRY_RUN`).
- Danh sách MÙI `a–d` (quy tắc lặp ≥3 file, trường/hash lặp, quy tắc không kiểm bằng lệnh, câu chép lại mọi packet): gặp là ghi `MUI=<a|b|c|d>` và báo, không tự sửa.
- Nhịp `MAINTAIN`: bắt buộc khi cấu trúc đổi và mỗi 10 phiên — rà hash, rà con trỏ, rà LỆNH còn chạy.
- `PROTOCOL/cach-nghi.md` (≤40 dòng): 8 bước nghĩ trước khi làm (`RESTATE`, `HOW`, `WHY`, `TEACH`, `RECALL`, `REFERENCE`, `PROTOTYPE`, `SLICE`); đây là cách nghĩ, không phải tầng governance mới — luật và skill vẫn thắng khi va nhau.

## Cách một AI vào làm việc

1. Đọc theo thứ tự ở `AGENTS.md`; phát `LAW_CHECK` và `RESUME_CHECK`.
2. Xác định vai (`A` / `B` / `C` / `R — Resumer` / `Writer` / tay chân) theo `PROTOCOL/multi-brain-loop.md` và `PROTOCOL/resume-protocol.md`.
3. Khi tra cứu tri thức lĩnh vực: tra `KB/INDEX.md` theo từ khóa (không phân biệt hoa/thường, bỏ dấu).
   - **Khớp** và còn `ACTIVE` => dùng làm điểm xuất phát; dữ kiện dễ cũ vẫn phải kiểm nguồn.
   - **Không khớp** => mở RUN mới, tự tìm, ghi lại rồi thêm dòng vào `KB/INDEX.md` (theo `KB/_TEMPLATE.md` nếu có khả năng tái dùng).
4. Làm việc bounded => một nhánh => một PR; ghi kết quả vào `RUNS/` kèm `SESSION_REF` + `PR_HEAD_SHA`.
5. Dừng khi đủ bằng chứng; không tự nhận PASS; không tự merge.

## Cây file hiện tại (24 file, đếm bằng `git ls-files | wc -l` ngày 2026-10-27)

```text
AGENTS.md
KB/INDEX.md
KB/_TEMPLATE.md
LAW/00-PROVENANCE-MAP.md
LAW/00-SUPREME-LAW.md
PROTOCOL/arena-agent-mode.md
PROTOCOL/cach-nghi.md
PROTOCOL/handoff-packet.md
PROTOCOL/kiem.md
PROTOCOL/multi-brain-loop.md
PROTOCOL/resume-protocol.md
README.md
REGISTER/BAC.md
REGISTER/LICH-SU.md
RUNS/0000-pr1-verify/B.md
RUNS/0000-pr1-verify/DECISION.md
RUNS/0000-pr1-verify/QUESTION.md
RUNS/INDEX.md
RUNS/README.md
STATE.md
scope-reality-check/SKILL.md
scope-reality-check/agents/openai.yaml
scope-reality-check/references/evals.md
scope-reality-check/references/evidence-rules.md
```

## GIAIDAP không phải

- Không phải bản luật song song; `P2P-upgrade-github-1` là nguồn thượng nguồn.
- Không phải nơi lưu transcript chat dài.
- Không phải daemon, script hay CI phức tạp.

TRẠNG THÁI: Mốc hiện tại `MỐC=KHUNG` — cập nhật 2026-10-27 (đã lắp cơ chế hồi sinh + bind skill `scope-reality-check`; chỉ chuyển sang `ĐANG_VẬN_HÀNH` khi T1–T6 trong `PROTOCOL/resume-protocol.md` §11 đạt bởi một PHIÊN MỚI thật). `PROVENANCE_STATUS=PENDING_VERIFICATION`: bảng ánh xạ `V4` chưa qua B kiểm lại diff `84ae8b3..HEAD`. `KB/INDEX.md` chưa có mục tri thức `ACTIVE` (đã có `KB/_TEMPLATE.md`). Lớp chứng minh verification-first (`PROTOCOL/kiem.md` + `PROTOCOL/cach-nghi.md`) đã vào main qua PR #6 (merged 06:37:18Z). PR #5 (vá 4 lỗ tự mục) không vào main vì base là nhánh #4; nội dung đó được đưa lên main bởi PR reconcile từ nhánh `arena/ea8a6620-giaidap`, đang chờ Owner review. Chi tiết xem `STATE.md`.
