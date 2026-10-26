RUN_ID: 0000-pr1-verify
TYPE: KIỂM LUẬT ĐỘC LẬP (không phải B RUN của vòng A/B/C)
DATE: 2026-10-26
CONTAMINATED=YES | LOẠI RUN=KIỂM LUẬT ĐỘC LẬP (không phải B RUN) | MODEL=UNKNOWN | TOOL=UNKNOWN
REVIEWED_HEAD=84ae8b3dfd8271d11af40c49fb34715634af1d0f
CONTENT_STATUS=MISSING

# B.md — CHƯA CÓ NỘI DUNG

> ⚠️ **FILE NÀY KHÔNG CHỨA BÁO CÁO CỦA B.**
>
> B report (bản đầy đủ) **chưa được cung cấp trong phiên này**. File này chỉ là chỗ giữ chỗ theo yêu cầu ghi RUN, **không** phải nhận xét của vai B và **không được trích dẫn như B report**.
>
> - `MODEL=UNKNOWN`, `TOOL=UNKNOWN` vì không có B khai trong phiên.
> - `CONTAMINATED=YES` vì RUN này được mở bởi chính Writer (người viết luật), không phải bởi B độc lập.
> - Những gì Writer đã dùng để vá là **bản tóm tắt 8 điểm + Q1/Q2/Q3 do Owner chép lại trong prompt**, không phải nguyên văn của B.

## Cần làm để đóng file này

1. Owner dán **nguyên văn** báo cáo của B vào đây (không biên tập, không rút gọn).
2. Điền lại `MODEL=` và `TOOL=` theo đúng B khai.
3. Ghi `CONTENT_STATUS=VERBATIM_RECEIVED` và ngày nhận.
4. Chỉ khi đó `RUNS/0000-pr1-verify/DECISION.md` mới được coi là có đối trọng độc lập; trước đó nó chỉ là bản ghi của Writer.

## Tóm tắt nội dung B mà Owner đã chuyển (KHÔNG phải nguyên văn)

- Q1: `LOẠI` mô tả **cái lõi**; phần thêm tách sang cột `PHẦN_TỰ_CHẾ`. `LUẬT 12 -> NEW`; `LUẬT 05/09/11` giữ `DERIVED` + `PHẦN_TỰ_CHẾ`.
- Q2: thêm `LUẬT 15` = `EXECUTOR_INPUT_FORMAT_AND_ARTIFACT_TRANSPORT_FIDELITY` (nguồn: notebook dòng 586); `LUẬT 01–14` giữ nguyên số và nội dung.
- Q3: quy trình không-khớp = "mở RUN rồi thêm dòng"; khai rõ GIAIDAP mở rộng (ghi KB cho tri thức lĩnh vực, không chỉ bài học từ lỗi) + điều kiện "chỉ ghi khi có khả năng tái dùng".
- 8 điểm vá: (1) map NEW=0→1, thêm cột, bump V2; (2) LUẬT 12 = NEW + PHẦN_TỰ_CHẾ; (3) PHẦN_TỰ_CHẾ cho 05/09/10/11; (4) sửa ghi chú 01/02/03/07/08/10/14; (5) header LAW/00 thêm LUẬT 15, sửa 22→21 RULE, anchors chỉ RULE thực dùng; (6) thống nhất LUẬT 12 với KB/INDEX.md; (7) LAW_CHECK: PASS chỉ khi SHA thật, không có PASS-với-UNKNOWN, mọi ví dụ là TEMPLATE; (8) sửa mâu thuẫn §2 vs §5 ở multi-brain-loop.

`UNKNOWN`: nội dung đầy đủ và cách diễn đạt gốc của B; các điểm B nêu mà Owner không chép vào prompt (nếu có).
