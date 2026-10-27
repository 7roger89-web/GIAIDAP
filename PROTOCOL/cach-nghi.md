# PROTOCOL/cach-nghi.md — Cách nghĩ trước khi làm

TRẠNG THÁI: ACTIVE | NGÀY: 2026-10-27
SESSION_REF: arena/05b33e63-giaidap
PR_HEAD_SHA: 7563b9c1826c13998f0b74a13f931c7460724408

> Ghi chú thực tế (2026-10-27): `REGISTER/LICH-SU.md` do PR #5 thêm nhưng CHƯA merge vào nhánh này. Khi file chưa có, dùng `STATE.md §LỊCH SỬ GẦN NHẤT` + `git log` thay thế; sau khi PR #5 merge thì đọc đúng đường dẫn chính danh.

1. **RESTATE** — Trước khi làm bất cứ gì, diễn giải lại việc BẰNG LỜI CỦA MÌNH: mục tiêu, đầu vào, đầu ra, điều kiện dừng. Lệch với packet => `RESTATE_MISMATCH=YES` và DỪNG, hỏi lại thay vì làm bừa. Đây là van chống trôi rẻ nhất.
2. **HOW** — Lần theo cơ chế bằng FILE THẬT trong repo, không đọc tóm tắt thay. Mỗi claim phải nêu được `file + dòng`; không trỏ được dòng thì ghi `UNKNOWN`, không đoán.
3. **WHY** — Trước khi đề xuất, tra `REGISTER/BAC.md`, `REGISTER/LICH-SU.md` (xem ghi chú đầu file), `DECISION.md` của RUN liên quan và `git log`. Không đề xuất lại cái đã bị bác; đề xuất lại cần bằng chứng mới + nhãn `OWNER_CONFIRMATION_REQUIRED`.
4. **TEACH** — Trước khi làm, nói rõ ba thứ: SẼ LÀM GÌ · ĐÁNH ĐỔI gì (chi phí, rủi ro, cái bị cắt) · SẼ KHÔNG LÀM GÌ (ranh giới phạm vi).
5. **RECALL** — Trước khi hỏi Owner, tra `RUNS/INDEX.md` + `KB/INDEX.md` + `LICH-SU.md`/`git log`. Repo đã trả lời thì không hỏi lại (`PROTOCOL/resume-protocol.md` §6).
6. **REFERENCE** — Owner đưa mẫu (link/file/ví dụ) thì bám cấu trúc của mẫu và GỌI TÊN pattern đang dùng, để người kiểm đối chiếu được gốc.
7. **PROTOTYPE** — Việc đụng >1 file: dựng bản mỏng nhất trước, đưa Owner/B review, rồi mới viết đầy đủ. Không đổ khuôn lớn khi chưa ai thấy bản mỏng.
8. **SLICE** — Lát đầu tiên phải chạy được đầu-cuối dù mỏng: một đường đi hoàn chỉnh từ LỆNH tới kết quả kiểm được (nối `PROTOCOL/kiem.md`). Cấm làm nửa vời rồi mới ghép sau.

## Vị trí của file này

Đây là CÁCH NGHĨ, không phải tầng governance mới: không thêm vai, không thêm biên lai, không thêm quyền. Khi va nhau, LUẬT 00 và skill `scope-reality-check` vẫn thắng (`PROTOCOL/resume-protocol.md` §9); file này chỉ sắp thứ tự suy nghĩ để các quy tắc sẵn có được dùng đúng lúc.
