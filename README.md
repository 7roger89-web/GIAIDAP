# GIAIDAP

Bộ nhớ chung + sổ luật cho quy trình nhiều AI.

- Chat là nơi làm việc; **sự thật nằm trong repo**.
- Repo giữ luật, giao thức, tri thức và nhật ký chạy. Không dựa vào ký ức của một phiên chat.
- GIAIDAP là **bản chuyển thể** từ [P2P-upgrade-github-1](https://github.com/7roger89-web/P2P-upgrade-github-1), không phải bản sao. Khi bản gốc đổi, rà lại `LAW/00-SUPREME-LAW.md`.
- Provenance của luật hiện là `PENDING_VERIFICATION`; xem khối provenance đầu `LAW/00-SUPREME-LAW.md`. Chưa có bên độc lập xác nhận.

## 4 khối

| Khối | Vai trò | File vào |
|---|---|---|
| `LAW/` | Luật tối thượng, duy nhất | `LAW/00-SUPREME-LAW.md` |
| `PROTOCOL/` | Cách vận hành: Arena, A/B/C, handoff | `PROTOCOL/*.md` |
| `KB/` | Tri thức tra theo từ khóa | `KB/INDEX.md` |
| `RUNS/` | Nhật ký từng phiên chạy | `RUNS/<4 số>-<slug>/` |

## Cách một AI vào làm việc

1. Đọc `AGENTS.md`.
2. Đọc `LAW/00-SUPREME-LAW.md` và phát `LAW_CHECK`.
3. Đọc `PROTOCOL/multi-brain-loop.md`.
4. Tra `KB/INDEX.md` theo từ khóa (không phân biệt hoa/thường, bỏ dấu).
   - **Khớp** và còn `ACTIVE` => dùng làm điểm xuất phát; dữ kiện dễ cũ vẫn phải kiểm nguồn.
   - **Không khớp** => mở RUN mới, tự tìm, ghi lại rồi thêm dòng vào `KB/INDEX.md`.
5. Làm việc bounded => một nhánh => một PR; ghi kết quả vào `RUNS/`.
6. Dừng khi đủ bằng chứng; không tự nhận PASS.

## Cây file V1

```text
README.md
AGENTS.md
STATE.md
LAW/00-SUPREME-LAW.md
LAW/00-PROVENANCE-MAP.md
PROTOCOL/arena-agent-mode.md
PROTOCOL/multi-brain-loop.md
PROTOCOL/handoff-packet.md
PROTOCOL/resume-protocol.md
KB/INDEX.md
RUNS/README.md
RUNS/INDEX.md
RUNS/0000-pr1-verify/B.md
RUNS/0000-pr1-verify/DECISION.md
```

## Luồng hồi sinh

Phiên mới → `AGENTS.md` → `STATE.md` → phát `LAW_CHECK` + `RESUME_CHECK` (theo `PROTOCOL/resume-protocol.md`) → tiếp việc theo `NEXT_ONE_ACTION` trong `STATE.md`. Nếu `RESUME_CHECK=BLOCKED` thì dừng.

## GIAIDAP không phải

- Không phải bản luật song song; `P2P-upgrade-github-1` là nguồn thượng nguồn.
- Không phải nơi lưu transcript chat dài.
- Không phải daemon, script hay CI phức tạp.

TRẠNG THÁI: V1 + các vòng vá (mới nhất: vá lần 7) + cơ chế hồi sinh — 2026-10-27. `PROVENANCE_STATUS=PENDING_VERIFICATION`: bảng ánh xạ V4 chưa có kiểm độc lập cho bản này. Chưa có mục KB nội dung; `KB/INDEX.md` mới có dòng ví dụ. Điểm hồi sinh: `STATE.md`.
