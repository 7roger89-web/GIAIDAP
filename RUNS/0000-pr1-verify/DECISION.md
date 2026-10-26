RUN_ID: 0000-pr1-verify
STATUS: OPEN
DATE: 2026-10-26
LOẠI RUN: KIỂM LUẬT ĐỘC LẬP (không phải vòng A/B/C)
REVIEWED_HEAD: 84ae8b3dfd8271d11af40c49fb34715634af1d0f (head B đã kiểm). Vá lần 5: `db14795`. Vá lần 6: commit mới nhất của nhánh.
CONTAMINATED=YES
NGUỒN QUYẾT ĐỊNH: Owner quyết Q1/Q2/Q3 (vá lần 5) và D1/D2/D3 (vá lần 6).
B_REPORT: `B.md` trong folder này — `CONTENT_STATUS=VERBATIM_RECEIVED`, `CONTENT_SHA256=UNKNOWN` (B không tự khai, Writer không tính thay).

## 0. Phạm vi và cảnh báo

1. `B.md` **nay có nguyên văn báo cáo của B** (196 dòng), chép từ bản Owner dán, không biên tập một chữ. Lỗi chính tả của B giữ nguyên — xem §4.
2. Đây là **KIỂM LUẬT ĐỘC LẬP**, không phải B RUN: B đã xem LAW/00, bảng ánh xạ, protocol và notebook thượng nguồn, tức vượt xa `QUESTION.md + A.md` của một RUN thường. Header ghi `CONTAMINATED=YES`.
3. RUN này do **Writer** mở. `PROVENANCE_STATUS` vẫn `PENDING_VERIFICATION` cho tới khi B kiểm lại bản V3 của bảng và Owner chấp nhận. Không có câu nào trong repo được nâng thành VERIFIED bởi lần vá này.
4. B kết luận `PASS_WITH_FIXES` cho head `84ae8b3` (bảng V1, 14 dòng). Bản V2/V3 **chưa** qua kiểm lại.

## 1. Vá lần 6 — quyết định D1 / D2 / D3

| Mã | Owner quyết | Đã làm gì | Bằng chứng |
|---|---|---|---|
| **D1** | Cho phép **sửa riêng LUẬT 12**; ràng buộc "không sửa LUẬT 01–14" được nâng cho LUẬT 12 | Sửa đúng khối `## LUẬT 12` trong `LAW/00-SUPREME-LAW.md` (3 điểm ở §3). LUẬT 01–11 và 13–15 **không sửa một chữ** | `git diff main...HEAD -- LAW/00-SUPREME-LAW.md` chỉ cho thấy thay đổi trong khối LUẬT 12 (ngoài các thay đổi của vá lần 5) |
| **D2** | **Giữ bảng 15 dòng**, `NEW=1 / DERIVED=14`, **không bỏ LUẬT 15** | Bảng V3 vẫn 15 dòng, tổng kết không đổi; LUẬT 15 vẫn ở dòng cuối | `grep -c '^| LUẬT' LAW/00-PROVENANCE-MAP.md` = 15 |
| **D3** | `B.md` ghi **nguyên văn**; `CONTENT_SHA256` lấy theo **B tự khai**; B không khai ⇒ `UNKNOWN` | Header `B.md` ghi `CONTENT_SHA256: UNKNOWN`, không tự tính SHA rồi ghi như B khai | `head -12 RUNS/0000-pr1-verify/B.md` |

## 2. LUẬT 12 sau khi sửa (dán nguyên văn)

```text
## LUẬT 12 — TRA CỨU BẰNG TỪ KHÓA
Vào repo => tra KB/INDEX.md theo từ khóa. KHỚP và còn ACTIVE => dùng làm điểm xuất phát
(vẫn kiểm nguồn nếu là dữ kiện dễ cũ). KHÔNG KHỚP => mở `RUNS/<4 số>-<slug>/`, tự tìm, ghi kết quả
vào RUN, rồi mới thêm dòng mới vào KB/INDEX.md (không ghi thẳng vào bảng khi chưa có RUN).
Chỉ ghi mục KB mới khi có khả năng tái dùng: phải nêu được ít nhất một tình huống tương lai mà mục đó
sẽ được tra lại; không nêu được => giữ trong `RUNS/`, không thêm dòng.
MỞ RỘNG so với nguồn (khai báo): KB giữ TRI THỨC LĨNH VỰC — kiến thức dùng lại được, không nhất thiết
sinh ra từ một lỗi; nguồn chỉ có experience lifecycle (bài học từ lỗi). Đây là phần GIAIDAP tự chế.
Từ khóa không phân biệt hoa/thường, bỏ dấu.
```

## 3. Ba điểm sửa trong LUẬT 12 — đối chiếu yêu cầu

| # | Yêu cầu | Câu chữ đã đưa vào LUẬT 12 | Ghi chú nguồn |
|---|---|---|---|
| a | Thêm điều kiện "chỉ ghi KB mới khi có khả năng tái dùng" | "Chỉ ghi mục KB mới khi có khả năng tái dùng: phải nêu được ít nhất một tình huống tương lai mà mục đó sẽ được tra lại; không nêu được => giữ trong `RUNS/`, không thêm dòng." | **Không có câu nguồn tương ứng.** Gần nhất là `2A > Task-end learning reconciliation` dòng 293 (`REPEATED_OR_MATERIAL_FAILURE \| CLEARLY_REUSABLE_CORRECTION`) — cùng tinh thần "phải tái dùng được", nhưng nguồn nói về experience, không nói về mục KB. |
| b | Khai **MỞ RỘNG**: ghi tri thức lĩnh vực, không chỉ bài học từ lỗi | "MỞ RỘNG so với nguồn (khai báo): KB giữ TRI THỨC LĨNH VỰC — kiến thức dùng lại được, không nhất thiết sinh ra từ một lỗi; nguồn chỉ có experience lifecycle (bài học từ lỗi). Đây là phần GIAIDAP tự chế." | **Đây là phần tự chế, khai rõ ngay trong luật.** Nguồn dòng 292 và 298–299 nói ngược lại phạm vi: `ROUTINE_SUCCESS => LEARNING_RECONCILIATION=NONE`, "Do not manufacture memory or candidates from routine success" — nguồn chỉ sinh tri thức từ lỗi/correction, không sinh từ tri thức lĩnh vực thường. |
| c | Thống nhất quy trình không-khớp = "mở RUN rồi thêm dòng" | "KHÔNG KHỚP => mở `RUNS/<4 số>-<slug>/`, tự tìm, ghi kết quả vào RUN, rồi mới thêm dòng mới vào KB/INDEX.md (không ghi thẳng vào bảng khi chưa có RUN)." | Đồng bộ với `KB/INDEX.md` §Cách dùng bước 4 và `README.md` bước 4. Trước lần vá này LUẬT 12 chỉ nói "GHI LẠI mục KB mới", khác quy trình trong `KB/INDEX.md` — đó là điểm B3.12 của B. |

Ngoài ba điểm trên, **không đổi câu nào khác** của LUẬT 12 (vẫn giữ câu "Từ khóa không phân biệt hoa/thường, bỏ dấu." và vế "vẫn kiểm nguồn nếu là dữ kiện dễ cũ" của bản cũ).

## 4. Lỗi chính tả của B — ghi lại, KHÔNG sửa

| Vị trí | Nguyên văn (giữ nguyên) | Loại |
|---|---|---|
| `B.md` dòng 173 | "chỉ chứng minh nhánh PR **tồn tại tại** thời điểm fetch" | lặp từ "tại" |

Không sửa dòng nào trong `B.md`. Không phát hiện lỗi chính tả nào khác.

## 5. File đã đổi trong vá lần 6

| File | Thay đổi |
|---|---|
| `RUNS/0000-pr1-verify/B.md` | Thay placeholder 32 dòng bằng nguyên văn báo cáo B (196 dòng) + header 9 trường |
| `LAW/00-SUPREME-LAW.md` | Sửa **riêng** khối LUẬT 12 theo D1 (3 điểm ở §3) |
| `LAW/00-PROVENANCE-MAP.md` | `PROVENANCE_MAP_VERSION=V3`; cập nhật dòng `PHẦN_TỰ_CHẾ` của LUẬT 12; sửa ghi chú "chưa được B xác nhận" cho đúng bản V3 |
| `KB/INDEX.md` | Bỏ câu "không sửa câu chữ LUẬT 12" (đã lỗi thời sau D1), thay bằng "hai chỗ phải mô tả cùng một quy trình" |
| `RUNS/0000-pr1-verify/DECISION.md` | File này: ghi D1/D2/D3, dán LUẬT 12 mới, ghi lỗi chính tả của B |

## 6. Lịch sử vá lần 5 (giữ làm hồ sơ)

> Ghi chú: hai ô dưới đây đã **bị D1 thay thế** ở vá lần 6 — trước đó LUẬT 12 chưa được sửa.

| # | Điểm | Trạng thái | Ghi chú |
|---|---|---|---|
| 1 | Map: `NEW=1`, `DERIVED=13`, thêm cột `PHẦN_TỰ_CHẾ`, `V2`, giữ `PENDING_VERIFICATION` | ÁP DỤNG, **có điều chỉnh số** | Bảng V2 có **15 dòng** (thêm LUẬT 15 theo Q2) nên tổng kết là `VERBATIM=0 / DERIVED=14 / NEW=1`. |
| 2 | LUẬT 12 → `LOẠI=NEW` + `PHẦN_TỰ_CHẾ` + điều kiện ghi mới | ÁP DỤNG (phần map) — **câu chữ luật đã sửa ở vá lần 6 (D1)** | Vá lần 5 chỉ đặt điều kiện ở `KB/INDEX.md`; vá lần 6 đưa vào chính LUẬT 12. |
| 3 | `PHẦN_TỰ_CHẾ` cho LUẬT 05, 09, 10, 11 | ÁP DỤNG | Nội dung do Writer viết, không phải nguyên văn B. |
| 4 | Sửa ghi chú: 01 (rút gọn/gộp), 02 (bỏ "when it may have changed"), 03 (thu hẹp acceptance), 07 (khái quát hoá + thêm công cụ/phê duyệt), 08 (bỏ project/workstream; mất format `<PROJECT> — <outcome>` + lệnh cấm boilerplate), 10 ("BỎ" → "ĐỔI TÊN"), 14 (thêm trigger "quyết định cần Owner") | ÁP DỤNG | Cả 7 ghi chú đã viết lại đúng nội dung này. |
| 5 | Header `LAW/00`: thêm LUẬT 15; `(22 mục RULE)` → `(21 mục RULE)`; anchors chỉ liệt kê RULE thực dùng | ÁP DỤNG | Đếm lại: 21 heading `### RULE NN —`. RULE thực dùng: 01, 02, 03, 04, 05, 07, 08, 12, 14, 16. |
| 6 | Thống nhất LUẬT 12 với `KB/INDEX.md` theo Q3 | ÁP DỤNG (quy trình) — **câu chữ luật sửa ở vá lần 6** | Xem §3(c). |
| 7 | Mẫu `LAW_CHECK`: PASS chỉ khi `SOURCE_SHA256` thật; không tính được => `BLOCKED` | ÁP DỤNG | Sửa ở `LAW/00 §0`, `AGENTS.md §1`, `PROTOCOL/multi-brain-loop.md §4`. |
| 8 | `PROTOCOL/multi-brain-loop.md`: sửa mâu thuẫn §2 vs §5 | ÁP DỤNG | §2 ghi rõ B bị cấm xem tài liệu ngoài; §3 thêm `CONTAMINATED=YES` + mở RUN mới; §5 giới hạn `NGUỒN ĐỐI LẬP` trong QUESTION/A. |

## 7. Chỗ dễ gây tranh (để B kiểm)

- `LUẬT 12 = NEW` là quyết định của Owner (Q1), không phải kết luận độc lập của Writer.
- Câu "MỞ RỘNG so với nguồn" ở LUẬT 12 là **phần tự chế** — nó khai một phạm vi rộng hơn nguồn, không phải chuyển thể từ nguồn.
- `LUẬT 05`, `LUẬT 09`, `LUẬT 11` giữ `DERIVED` dù phần tự chế lớn; ranh giới `DERIVED`/`NEW` vẫn là đánh giá chủ quan.
- `LUẬT 08` mất format tiêu đề và lệnh cấm boilerplate so với nguồn — đã ghi nhận, **chưa vá** (ngoài phạm vi D1).

## 8. UNKNOWN

- `CONTENT_SHA256` của `B.md`: B không khai ⇒ `UNKNOWN`.
- B chưa kiểm bản map V2/V3 và chưa kiểm LUẬT 12 sau khi sửa ⇒ không có kết luận độc lập nào cho các bản này.
- Báo cáo của B dựa trên head `84ae8b3`; các kết luận về số dòng/anchors có thể đã lệch sau vá lần 5 (header LAW/00 đã đổi).
- Việc B có chấp nhận cách viết mới của LUẬT 12 (đặc biệt câu khai MỞ RỘNG) hay không — chưa có.

## 9. NEXT_ONE_ACTION

Giao B kiểm lại **đúng phần thay đổi của vá lần 5 + vá lần 6** (diff từ `84ae8b3` tới head hiện tại): LUẬT 12 mới, dòng `PHẦN_TỰ_CHẾ` LUẬT 12 trong map V3, và `KB/INDEX.md` §MỞ RỘNG. Chỉ sau đó mới xét gỡ `PENDING_VERIFICATION`.
