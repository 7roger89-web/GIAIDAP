RUN_ID: 0000-pr1-verify
STATUS: OPEN
DATE: 2026-10-26
LOẠI RUN: KIỂM LUẬT ĐỘC LẬP (không phải vòng A/B/C)
REVIEWED_HEAD: 84ae8b3dfd8271d11af40c49fb34715634af1d0f (head trước khi vá)
CONTAMINATED=YES
NGUỒN QUYẾT ĐỊNH: Owner quyết Q1/Q2/Q3 trong prompt vá ngày 2026-10-26.
B_REPORT: `B.md` trong folder này — **CHƯA CÓ NỘI DUNG** (`CONTENT_STATUS=MISSING`).

## 0. Cảnh báo phạm vi

- `B.md` **không** chứa báo cáo của B. Owner đã chép **bản tóm tắt** 8 điểm + Q1/Q2/Q3 vào prompt; Writer dùng bản tóm tắt đó.
- Vì vậy mọi câu trong `PHẦN_TỰ_CHẾ` của `LAW/00-PROVENANCE-MAP.md` là **Writer tự viết**, không phải nguyên văn của B, dù Owner yêu cầu "nguyên văn đề xuất của B". Không thể trích nguyên văn thứ chưa nhận được.
- Đây là RUN do Writer mở; không phải kiểm chứng độc lập. `PROVENANCE_STATUS` vẫn `PENDING_VERIFICATION`.

## 1. Đã áp (8 điểm)

| # | Điểm | Trạng thái | Ghi chú |
|---|---|---|---|
| 1 | `LAW/00-PROVENANCE-MAP.md`: `NEW=1`, `DERIVED=13`, thêm cột `PHẦN_TỰ_CHẾ`, `PROVENANCE_MAP_VERSION=V2`, giữ `PENDING_VERIFICATION` | ÁP DỤNG, **có điều chỉnh số** | Bảng V2 có **15 dòng** (thêm LUẬT 15 theo Q2) nên tổng kết là `VERBATIM=0 / DERIVED=14 / NEW=1`. Con số `DERIVED=13` đúng cho bảng 14 luật trước khi thêm LUẬT 15. Đã ghi rõ trong chính file map. |
| 2 | LUẬT 12 → `LOẠI=NEW` + `PHẦN_TỰ_CHẾ` + điều kiện ghi mới | ÁP DỤNG | `MỤC NGUỒN` ghi "— (không có mục nguồn tương ứng)"; `PHẦN_TỰ_CHẾ` liệt kê toàn bộ cơ chế KB/INDEX.md. Điều kiện ghi đặt ở `KB/INDEX.md` (xem mục 2 dưới). |
| 3 | `PHẦN_TỰ_CHẾ` cho LUẬT 05, 09, 10, 11 | ÁP DỤNG | Nội dung do Writer viết, không phải nguyên văn B. |
| 4 | Sửa ghi chú: 01 (rút gọn/gộp), 02 (bỏ "when it may have changed"), 03 (thu hẹp acceptance), 07 (khái quát hoá + thêm công cụ/phê duyệt), 08 (bỏ project/workstream; mất format `<PROJECT> — <outcome>` + lệnh cấm boilerplate), 10 ("BỎ" → "ĐỔI TÊN"), 14 (thêm trigger "quyết định cần Owner") | ÁP DỤNG | Cả 7 ghi chú đã viết lại đúng nội dung này. |
| 5 | Header `LAW/00`: thêm LUẬT 15; `(22 mục RULE)` → `(21 mục RULE)`; anchors chỉ liệt kê RULE thực dùng | ÁP DỤNG | Đã đếm lại: 21 heading `### RULE NN —`. RULE thực dùng: 01, 02, 03, 04, 05, 07, 08, 12, 14, 16. Ngoài phạm vi: 06, 09, 10, 11, 13, 15, 17, 18, 19, 20, 21 (RULE 15 ghi rõ là liên quan `PROTOCOL/arena-agent-mode.md §7`). |
| 6 | Thống nhất LUẬT 12 với `KB/INDEX.md` theo Q3 | ÁP DỤNG, **có điều chỉnh** | Điều kiện "chỉ ghi khi có khả năng tái dùng" + khai báo mở rộng nằm trong `KB/INDEX.md §MỞ RỘNG SO VỚI NGUỒN`. **Không sửa câu chữ LUẬT 12** (xem mục 2). |
| 7 | Mẫu `LAW_CHECK`: PASS chỉ khi `SOURCE_SHA256` thật; không tính được => `BLOCKED`; bỏ nhánh PASS-với-UNKNOWN; mọi ví dụ ghi TEMPLATE | ÁP DỤNG | Sửa ở `LAW/00 §0`, `AGENTS.md §1`, `PROTOCOL/multi-brain-loop.md §4`. |
| 8 | `PROTOCOL/multi-brain-loop.md`: sửa mâu thuẫn §2 vs §5 | ÁP DỤNG | §2 (bảng vai) ghi rõ B bị cấm xem tài liệu ngoài; §3 thêm quy tắc `CONTAMINATED=YES` + mở RUN mới; §5 `NGUỒN ĐỐI LẬP` giới hạn trong QUESTION/A. |

## 2. Đã KHÔNG làm và lý do

1. **Không sửa câu chữ LUẬT 01–14**, kể cả LUẬT 12. Lý do: ràng buộc "KHÔNG sửa LUẬT 01–14" (điểm Q2) + "Vá đúng 8 điểm, không viết lại kiến trúc". Hệ quả: điều kiện "chỉ ghi khi có khả năng tái dùng" hiện là quy định vận hành ở `KB/INDEX.md`, **chưa** phải là câu luật. Muốn nâng thành luật thì phải sửa LUẬT 12 — cần Owner quyết riêng.
2. **Không tái tạo B.md.** Không có nguyên văn thì không viết vào chỗ của B; file `B.md` để trống có cảnh báo (`CONTENT_STATUS=MISSING`).
3. **Không đổi `PROVENANCE_STATUS`** — vẫn `PENDING_VERIFICATION`.
4. **Không sửa `LAW/00-PROVENANCE-MAP.md` mục GIỚI HẠN** sang "đã kiểm" — vẫn 3 dòng nêu rõ chưa có kiểm độc lập.

## 3. Chỗ dễ gây tranh (để B kiểm)

- `LUẬT 12 = NEW` là quyết định của Owner (Q1), không phải kết luận độc lập của Writer. Bản thân LUẬT 12 vẫn có **mục liên quan** trong nguồn (experience lookup), chỉ là lõi cơ chế khác.
- `LUẬT 05`, `LUẬT 09`, `LUẬT 11` giữ `DERIVED` dù phần tự chế khá lớn. Ranh giới `DERIVED`/`NEW` vẫn là đánh giá chủ quan.
- `LUẬT 08` bị **mất** format tiêu đề và lệnh cấm boilerplate so với nguồn — đây là thiếu sót của bản V1, chưa vá; chỉ ghi nhận.

## 4. UNKNOWN

- Nguyên văn báo cáo của B và mọi điểm B nêu mà Owner không chép vào prompt.
- Việc `PHẦN_TỰ_CHẾ` do Writer viết có khớp với ý B hay không.
- Có nên nâng điều kiện "chỉ ghi khi có khả năng tái dùng" thành câu luật (sửa LUẬT 12) hay giữ ở `KB/INDEX.md`.

## 5. NEXT_ONE_ACTION

Owner dán nguyên văn B report vào `RUNS/0000-pr1-verify/B.md`, rồi giao B kiểm lại `LAW/00` + bảng ánh xạ V2.
