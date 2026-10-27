# REGISTER/BAC.md — Sổ phương án đã bị bác

TRẠNG THÁI: ACTIVE | NGÀY: 2026-10-27

**Đây là đòn chống tái tranh luận.** Mọi model mới **BẮT BUỘC** đọc file này trước khi đề xuất phương án, kiến trúc hoặc cách sửa quy trình mới.

| NGÀY | PHƯƠNG ÁN ĐÃ BÁC (1 dòng) | LÝ DO BÁC | AI BÁC (Owner\|B) | RUN_ID |
|---|---|---|---|---|
| 2026-10-26 | Bỏ LUẬT 15 (EXECUTOR_INPUT_FORMAT_AND_ARTIFACT_TRANSPORT_FIDELITY) khỏi LAW/00 và bảng ánh xạ để giữ 14 luật | Nguồn thượng nguồn có 9 Supreme laws (mục 9 tại dòng 586 bị thiếu ở V1 theo B3.7); Owner quyết thêm LUẬT 15 theo Q2 và giữ bảng 15 dòng theo D2 (xem `RUNS/0000-pr1-verify/DECISION.md` §1, §6) | Owner | 0000-pr1-verify |
| 2026-10-26 | Gộp chung một trường `CONTENT_SHA256` duy nhất trong header `B.md` (hoặc để Writer tự băm rồi điền thay giá trị B khai) | Hash do B tự khai và hash do Writer tự băm khác nguồn, không thay thế nhau; theo D3 và D5 phải tách thành 2 trường riêng `CONTENT_SHA256_B_DECLARED` và `CONTENT_SHA256_WRITER_COMPUTED` (xem `RUNS/0000-pr1-verify/DECISION.md` §1) | Owner | 0000-pr1-verify |

## Quy tắc vận hành

1. **Cập nhật cùng commit:** mỗi khi `Owner` hoặc `B` bác một phương án cụ thể (hoặc khi một kết luận/phương án phải đảo lại sau khi `C` đã đọc theo `PROTOCOL/multi-brain-loop.md` §11), người ghi file bắt buộc thêm 1 dòng vào bảng này **TRONG CÙNG COMMIT** với kết quả `RUN` và `STATE.md`.
2. **Cấm đề xuất lại mù quáng:** model mới không được đề xuất lại phương án đã nằm trong bảng trên, trừ khi chỉ ra được bằng chứng mới làm thay đổi trực tiếp `LÝ DO BÁC` và gắn nhãn `OWNER_CONFIRMATION_REQUIRED`.
3. **Không xóa lịch sử:** phương án được mở lại hợp lệ thì ghi chú bằng dòng mới hoặc cập nhật tham chiếu `RUN_ID` mới, không xóa dòng cũ.

## Ghi chú trung thực

- Một sổ `BAC.md` rỗng lúc dự án mới khởi tạo là hoàn toàn bình thường; không bịa phương án giả để lấp bảng.
- Hai dòng seed trong bảng trên là **dữ liệu THẬT**, không phải ví dụ minh họa: trích từ `RUNS/0000-pr1-verify/DECISION.md` (quyết định Q2/D2 và D3/D5 trên PR #1; lưu ý câu chữ quyết định của Owner trong `DECISION.md` là bản do Writer chép lại `OWNER_SAID=PARAPHRASE`, chưa có comment nguyên văn của Owner trên PR #1).
