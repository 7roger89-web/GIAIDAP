# PROTOCOL/handoff-packet.md — Mẫu packet bàn giao

TRẠNG THÁI: ACTIVE | NGÀY: 2026-10-27

Quy tắc chung:

- Mỗi packet = một vai = một phiên/lần chạy.
- `INPUT` ghi **đường dẫn file**, không dán nội dung dài.
- Dòng **không trống** đầu tiên của prompt `NEW_CHAT` là tiêu đề, và `CHAT_TITLE` phải **bằng đúng** dòng đó (LUẬT 08); dòng đầu không được là boilerplate (`GỬI CHO:`, `DESTINATION=`, `TASK_ID=`, code fence, prefix `P2P` chung).
- Các khối `PACKET->A/B/C` dưới đây là **mẫu nội dung**: khi gửi thật, đưa tiêu đề lên dòng không trống đầu tiên (bỏ nhãn `PACKET->A` khỏi dòng 1), rồi mới tới phần còn lại.
- Không đưa `A.md`/`B.md`/`C.md` hoặc kết luận của Owner vào packet sai vai.
- Ghi rõ ràng buộc và điều kiện dừng. Hết điều kiện dừng là dừng, không tự mở vòng mới.
- Ba packet `PACKET->A/B/C` dùng đủ 10 trường: `TASK_ID`, `ROLE`, `CHAT_MODE`, `CHAT_TITLE`, `INPUT`, `OUTPUT`, `RESTATE`, `CÁCH CHỨNG MINH`, `RÀNG BUỘC`, `ĐIỀU KIỆN DỪNG`. Định nghĩa hai trường mới: `RESTATE` tại `PROTOCOL/cach-nghi.md` §1; `CÁCH CHỨNG MINH` (khối 4 dòng `LỆNH` / `KỲ VỌNG` / `ARTIFACT` / `NẾU KHÔNG CHẠY ĐƯỢC`) tại `PROTOCOL/kiem.md` §1. Cả hai điền TRƯỚC khi làm.
- `RETURN_PACKET->OWNER` dùng 6 trường báo cáo bắt buộc (`STATUS`, `PR`, `FILES`, `LAW_SOURCE`, `UNKNOWN`, `NEXT_ONE_ACTION`) cộng 3 trường chứng minh: `CÁCH CHỨNG MINH_ĐÃ CHẠY=YES|NO`, `MUI=<a|b|c|d|...|NONE>`, `RESTATE_MISMATCH=<YES|NO>` (định nghĩa tại `PROTOCOL/kiem.md` và `PROTOCOL/cach-nghi.md`).

## 1. PACKET->A

```text
PACKET->A
TASK_ID: 0001-nhap-khau-binh-nong-lanh
ROLE: A — Proposer
CHAT_MODE: NEW_CHAT
CHAT_TITLE: 0001 — Nhập khẩu bình nóng lạnh từ Trung Quốc
INPUT: RUNS/0001-nhap-khau-binh-nong-lanh/QUESTION.md
OUTPUT: RUNS/0001-nhap-khau-binh-nong-lanh/A.md
RESTATE: <diễn giải lại việc bằng lời của mình; lệch packet => RESTATE_MISMATCH=YES và DỪNG — PROTOCOL/cach-nghi.md §1>
CÁCH CHỨNG MINH:
- LỆNH: test -s RUNS/0001-nhap-khau-binh-nong-lanh/A.md && grep -c '^## ' RUNS/0001-nhap-khau-binh-nong-lanh/A.md
- KỲ VỌNG: in ra 5 (đủ 5 mục nội dung), exit 0
- ARTIFACT: RUNS/0001-nhap-khau-binh-nong-lanh/A.md
- NẾU KHÔNG CHẠY ĐƯỢC: chép nguyên văn lỗi shell + liệt kê tiêu đề mục thực có trong file
RÀNG BUỘC:
- Chỉ nhận câu hỏi thô; không nhận B/C, không nhận kết luận của Owner.
- Xuất đúng 5 mục: ĐỀ XUẤT, GIẢ ĐỊNH, ĐỘ TIN CẬY, UNKNOWN, NGUỒN.
- Ghi header chuẩn 6 trường; MODEL=UNKNOWN nếu không xác minh được.
- Không bịa nguồn; không tự nhận PASS.
ĐIỀU KIỆN DỪNG: A.md đã ghi đủ 5 mục + header + LAW_CHECK; không mở vòng mới.
```

## 2. PACKET->B

```text
PACKET->B
TASK_ID: 0001-nhap-khau-binh-nong-lanh
ROLE: B — Challenger / Verifier
CHAT_MODE: NEW_CHAT
CHAT_TITLE: 0001B — Phản biện đề xuất nhập khẩu bình nóng lạnh
INPUT: RUNS/0001-nhap-khau-binh-nong-lanh/QUESTION.md + RUNS/0001-nhap-khau-binh-nong-lanh/A.md
OUTPUT: RUNS/0001-nhap-khau-binh-nong-lanh/B.md
RESTATE: <diễn giải lại việc bằng lời của mình; lệch packet => RESTATE_MISMATCH=YES và DỪNG — PROTOCOL/cach-nghi.md §1>
CÁCH CHỨNG MINH:
- LỆNH: test -s RUNS/0001-nhap-khau-binh-nong-lanh/B.md && grep -c '^## ' RUNS/0001-nhap-khau-binh-nong-lanh/B.md
- KỲ VỌNG: in ra 7 (đủ 7 mục kể cả THU HẸP ĐỀ XUẤT), exit 0
- ARTIFACT: RUNS/0001-nhap-khau-binh-nong-lanh/B.md
- NẾU KHÔNG CHẠY ĐƯỢC: chép nguyên văn lỗi shell + liệt kê tiêu đề mục thực có trong file
RÀNG BUỘC:
- Chỉ nhận đúng 2 file trên; không xem C, không xem chat của A, không xem kết luận của Owner.
- Tấn công A: lỗi, thiếu, phản ví dụ, nguồn đối lập, chỗ A tự mâu thuẫn.
- Không viết lại đề xuất của A; không phán quyết thay C.
- Ghi header chuẩn 6 trường; MODEL=UNKNOWN nếu không xác minh được.
ĐIỀU KIỆN DỪNG: B.md đã ghi đủ 7 mục (kể cả `## THU HẸP ĐỀ XUẤT (không phải viết lại)`, đồng bộ `PROTOCOL/multi-brain-loop.md` §5) + header + LAW_CHECK; không mở vòng mới.
```

## 3. PACKET->C

```text
PACKET->C
TASK_ID: 0001-nhap-khau-binh-nong-lanh
ROLE: C — Judge / Synthesizer
CHAT_MODE: NEW_CHAT
CHAT_TITLE: 0001C — Phán quyết nhập khẩu bình nóng lạnh
INPUT: RUNS/0001-nhap-khau-binh-nong-lanh/QUESTION.md + RUNS/0001-nhap-khau-binh-nong-lanh/A.md + RUNS/0001-nhap-khau-binh-nong-lanh/B.md
OUTPUT: RUNS/0001-nhap-khau-binh-nong-lanh/C.md
RESTATE: <diễn giải lại việc bằng lời của mình; lệch packet => RESTATE_MISMATCH=YES và DỪNG — PROTOCOL/cach-nghi.md §1>
CÁCH CHỨNG MINH:
- LỆNH: grep -q '^## PHÁN QUYẾT' RUNS/0001-nhap-khau-binh-nong-lanh/C.md && grep -q '^## UNKNOWN' RUNS/0001-nhap-khau-binh-nong-lanh/C.md
- KỲ VỌNG: exit 0, không in gì (có cả mục PHÁN QUYẾT và UNKNOWN)
- ARTIFACT: RUNS/0001-nhap-khau-binh-nong-lanh/C.md
- NẾU KHÔNG CHẠY ĐƯỢC: chép nguyên văn lỗi shell + trích các tiêu đề mục thực có trong file
RÀNG BUỘC:
- Chỉ nhận đúng 3 file trên; không xem kết luận của Owner, không xem chat của A/B.
- Đối chiếu bằng chứng, không chọn bên nghe hợp lý hơn.
- Phán quyết + lý do + độ tin cậy + UNKNOWN + việc cần kiểm thêm.
- Không bịa nguồn; không nâng INFERENCE thành FACT.
- Ghi header chuẩn 6 trường; MODEL=UNKNOWN nếu không xác minh được.
ĐIỀU KIỆN DỪNG: C.md có VERDICT + UNKNOWN (hoặc UNKNOWN=NONE); không tự mở vòng mới.
```

## 4. RETURN_PACKET->OWNER

```text
RETURN_PACKET->OWNER
TASK_ID: 0001-nhap-khau-binh-nong-lanh
STATUS: PR_OPENED_PENDING_OWNER_REVIEW
PR: <URL pull request>
FILES:
- RUNS/0001-nhap-khau-binh-nong-lanh/QUESTION.md
- RUNS/0001-nhap-khau-binh-nong-lanh/A.md
- RUNS/0001-nhap-khau-binh-nong-lanh/B.md
- RUNS/0001-nhap-khau-binh-nong-lanh/C.md
- RUNS/0001-nhap-khau-binh-nong-lanh/DECISION.md
LAW_SOURCE: LAW/00-SUPREME-LAW.md (nguồn gốc: Owner cung cấp, mục "=== LUẬT ===")
UNKNOWN:
- <điều chưa xác minh>
NEXT_ONE_ACTION: <một việc duy nhất tiếp theo>
CÁCH CHỨNG MINH_ĐÃ CHẠY: <YES|NO — đã chạy thật các LỆNH trong packet trước khi báo cáo>
MUI: <a|b|c|d|...|NONE>
RESTATE_MISMATCH: <YES|NO>
```

`STATUS` dùng một trong:

- `PR_OPENED_PENDING_OWNER_REVIEW`
- `BLOCKED` (kèm lý do trong `UNKNOWN`)
- `DONE_NO_PR` (chỉ khi task không cần PR; ghi rõ lý do)

Không dùng `PASS`, `DONE`, `OK` thay cho trạng thái có thể kiểm.

- Có đổi trạng thái (ghi/sửa file, đổi `STATE.md`, push, mở PR) mà `CÁCH CHỨNG MINH_ĐÃ CHẠY=NO` => bắt buộc `STATUS=BLOCKED` (kèm lý do trong `UNKNOWN`); không được dùng `PR_OPENED_PENDING_OWNER_REVIEW`.

## 5. Kiểm tra trước khi gửi packet

- [ ] `TASK_ID` khớp tên folder `RUNS/<4 số>-<slug>/`.
- [ ] `INPUT` chỉ gồm đúng file vai đó được phép thấy.
- [ ] `OUTPUT` là đường dẫn file sẽ tạo, không phải nội dung.
- [ ] `CHAT_TITLE` là dòng đầu tiên của prompt `NEW_CHAT`.
- [ ] Có ràng buộc và điều kiện dừng rõ ràng.
- [ ] Không dán nội dung dài vào packet.
- [ ] Không có kết luận của Owner bị đưa vào packet của A/B/C.
- [ ] Mọi `PACKET->A/B/C` có đủ 2 trường `RESTATE` và `CÁCH CHỨNG MINH` (khối 4 dòng `LỆNH` / `KỲ VỌNG` / `ARTIFACT` / `NẾU KHÔNG CHẠY ĐƯỢC`), điền trước khi làm.
- [ ] `RETURN_PACKET->OWNER` có đủ 3 trường chứng minh; có đổi trạng thái mà `CÁCH CHỨNG MINH_ĐÃ CHẠY=NO` => `STATUS=BLOCKED`.
