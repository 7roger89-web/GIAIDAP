# RUNS/README.md — Quy ước nhật ký chạy

TRẠNG THÁI: ACTIVE | NGÀY: 2026-10-26

Mỗi lần chạy A/B/C là một folder:

```text
RUNS/<4 số>-<slug>/
  QUESTION.md   (tùy chọn nhưng nên có: câu hỏi thô + link nguồn thô)
  A.md
  B.md
  C.md
  DECISION.md
```

## 1. Tên folder

- 4 số, bắt đầu `0001`, tăng dần, không dùng lại số cũ.
- Slug tiếng Việt **không dấu**, chữ thường, gạch ngang.
- Ví dụ: `RUNS/0001-nhap-khau-binh-nong-lanh/`.
- Không đổi tên folder sau khi đã mở PR.

## 2. File tối thiểu

- `A.md`, `B.md`, `C.md`: output của ba vai, theo `PROTOCOL/multi-brain-loop.md`.
- Mọi file `B*.md` phải có **cả hai** field hash: `CONTENT_SHA256_B_DECLARED` (B tự khai; không khai ⇒ `UNKNOWN`) và `CONTENT_SHA256_WRITER_COMPUTED` (người ghi tự băm). Hai field khác nguồn, không thay thế nhau — chi tiết ở `PROTOCOL/multi-brain-loop.md` §4.
- Mọi file output ghi thêm `SESSION_REF` (tên nhánh/PR) và `PR_HEAD_SHA` để truy vết phiên nào làm ra file (nhóm `TRƯỜNG MỞ RỘNG` ở `PROTOCOL/multi-brain-loop.md` §4).
- `DECISION.md`: bản ghi kết luận, do Arena ghi từ `C.md` + quyết định của Owner.
- `QUESTION.md` (tùy chọn, nên có): câu hỏi thô. Không dán kết luận của A/B/C vào đây.

Không lưu transcript chat dài. Chỉ lưu output có cấu trúc, đường dẫn nguồn và quyết định.

## 3. Trạng thái

- `OPEN`: RUN đang chạy; chưa có `DECISION.md` hoặc `DECISION.md` ghi `STATUS: OPEN`.
- `CLOSED`: C đã ra phán quyết và `DECISION.md` đã ghi `STATUS: CLOSED`.

Không xóa RUN đã đóng. Không sửa `A.md`/`B.md`/`C.md` sau khi C đã đọc; nếu cần làm lại, mở RUN mới.

## 4. Mẫu DECISION.md

```text
RUN_ID: 0001-nhap-khau-binh-nong-lanh
STATUS: CLOSED
DATE: 2026-10-26
QUESTION_REF: QUESTION.md
A_REF: A.md
B_REF: B.md
C_REF: C.md
C_VERDICT: <chép nguyên văn hoặc tóm tắt trung thành từ C.md>
CONFIDENCE: CAO | TRUNG BÌNH | THẤP
OWNER_DECISION: PENDING | <quyết định của Owner>
UNKNOWN:
- <điều còn chưa biết>
NEXT_ONE_ACTION: <một việc duy nhất>
SOURCES:
- <URL/đường dẫn + ngày kiểm>
```

- `C_VERDICT` không được bóp méo thành ý của Arena.
- `OWNER_DECISION=PENDING` khi chưa có quyết định của Owner.
- Nếu `C_VERDICT=UNKNOWN`, vẫn đóng RUN; ghi `NEXT_ONE_ACTION` thay vì tự lặp.

## 5. Liên kết với KB

- Nếu RUN tạo ra tri thức mới: thêm file KB (nếu cần) và một dòng vào `KB/INDEX.md`.
- Nếu RUN lật một mục KB cũ: đổi mục cũ thành `SUPERSEDED`, thêm mục mới.
- Không copy toàn bộ `C.md` vào KB; chỉ chắt lọc dữ kiện có nguồn.

## 6. Liên kết với PR

- Một RUN có thể nằm trong một PR cùng các file khác nếu cùng một mục tiêu bounded.
- Không mở PR riêng cho từng file.
- PR phải ghi `RUN_ID` trong mô tả.
