# PROTOCOL/handoff-packet.md — Mẫu packet bàn giao

TRẠNG THÁI: ACTIVE | NGÀY: 2026-10-26

Quy tắc chung:

- Mỗi packet = một vai = một phiên/lần chạy.
- `INPUT` ghi **đường dẫn file**, không dán nội dung dài.
- Dòng **không trống** đầu tiên của prompt `NEW_CHAT` là tiêu đề, và `CHAT_TITLE` phải **bằng đúng** dòng đó (LUẬT 08); dòng đầu không được là boilerplate (`GỬI CHO:`, `DESTINATION=`, `TASK_ID=`, code fence, prefix `P2P` chung).
- Các khối `PACKET->A/B/C` dưới đây là **mẫu nội dung**: khi gửi thật, đưa tiêu đề lên dòng không trống đầu tiên (bỏ nhãn `PACKET->A` khỏi dòng 1), rồi mới tới phần còn lại.
- Không đưa `A.md`/`B.md`/`C.md` hoặc kết luận của Owner vào packet sai vai.
- Ghi rõ ràng buộc và điều kiện dừng. Hết điều kiện dừng là dừng, không tự mở vòng mới.
- Ba packet `PACKET->A/B/C` dùng đủ 8 trường: `TASK_ID`, `ROLE`, `CHAT_MODE`, `CHAT_TITLE`, `INPUT`, `OUTPUT`, `RÀNG BUỘC`, `ĐIỀU KIỆN DỪNG`.
- Mỗi packet ghi rõ `TRIGGER_MODE` / `EVIDENCE_MODE` đúng vai (`PROTOCOL/multi-brain-loop.md §11`): **A = `USER_EXPLICIT` / `LIVE`**, **B = `ROLE_BOUND` / `SEALED`**, **C = `ROLE_BOUND` / `SEALED`**. `PACKET->B` yêu cầu B.md đủ **7 mục** (kể cả `## THU HẸP ĐỀ XUẤT (không phải viết lại)`).
- `RETURN_PACKET->OWNER` dùng 6 trường báo cáo bắt buộc (`STATUS`, `PR`, `FILES`, `LAW_SOURCE`, `UNKNOWN`, `NEXT_ONE_ACTION`) cộng 2 trường trạng thái `STATE_UPDATED`, `REGISTER_UPDATED` (8 trường) khi phiên có cập nhật sổ / `STATE.md`.

## 1. PACKET->A

```text
PACKET->A
TASK_ID: 0001-nhap-khau-binh-nong-lanh
ROLE: A — Proposer
CHAT_MODE: NEW_CHAT
CHAT_TITLE: 0001 — Nhập khẩu bình nóng lạnh từ Trung Quốc
INPUT: RUNS/0001-nhap-khau-binh-nong-lanh/QUESTION.md
OUTPUT: RUNS/0001-nhap-khau-binh-nong-lanh/A.md
RÀNG BUỘC:
- Chỉ nhận câu hỏi thô; không nhận B/C, không nhận kết luận của Owner.
- `TRIGGER_MODE=USER_EXPLICIT`: skill scope-reality-check chỉ bật khi Owner/packet yêu cầu tường minh.
- `EVIDENCE_MODE=LIVE`: được tra nguồn sống, web, repo trong phạm vi câu hỏi; phải ghi nguồn + ngày kiểm.
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
RÀNG BUỘC:
- Chỉ nhận đúng 2 file trên; không xem C, không xem chat của A, không xem kết luận của Owner.
- Tấn công A: lỗi, thiếu, phản ví dụ, nguồn đối lập, chỗ A tự mâu thuẫn.
- B.md phải xuất đủ 7 mục: `## LỖI`, `## THIẾU`, `## PHẢN VÍ DỤ`, `## NGUỒN ĐỐI LẬP`, `## A TỰ MÂU THUẪN`, `## THU HẸP ĐỀ XUẤT (không phải viết lại)`, `## UNKNOWN`. Mục THU HẸP ĐỀ XUẤT (không phải viết lại) chỉ cắt lát nhỏ nhất kiểm chứng được từ chính đề xuất của A, không thiết kế giải pháp mới, không viết lại thay A.
- `EVIDENCE_MODE=SEALED`: chỉ dùng nguồn có trong 2 file INPUT (`QUESTION.md` + `A.md`); không tự tra web / mở file ngoài (vượt rào => `CONTAMINATED=YES`).
- `TRIGGER_MODE=ROLE_BOUND`: chạy skill scope-reality-check theo vai, không chờ câu chữ trigger của người dùng.
- Tone sắc/thẳng của skill CHỈ áp dụng cho văn xuôi; tên mục, trường header và nhãn nhận thức giữ nguyên trang trọng, không châm biếm hóa nhãn.
- Không phán quyết thay C; ghi header chuẩn 6 trường; MODEL=UNKNOWN nếu không xác minh được.
ĐIỀU KIỆN DỪNG: B.md đã ghi đủ 7 mục + header + LAW_CHECK; không mở vòng mới.
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
RÀNG BUỘC:
- Chỉ nhận đúng 3 file trên; không xem kết luận của Owner, không xem chat của A/B.
- `TRIGGER_MODE=ROLE_BOUND`: chạy skill scope-reality-check theo vai, không chờ câu chữ trigger của người dùng.
- `EVIDENCE_MODE=SEALED`: chỉ đối chiếu nguồn có trong 3 file INPUT; không tự tra ngoài (vượt rào => `CONTAMINATED=YES`).
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
STATE_UPDATED: <YES|NO — STATE.md + RUNS/INDEX.md cập nhật trong cùng commit?>
REGISTER_UPDATED: <YES|NO — REGISTER/BAC.md, REGISTER/LICH-SU.md cập nhật?>
```

`STATUS` dùng một trong:

- `PR_OPENED_PENDING_OWNER_REVIEW`
- `BLOCKED` (kèm lý do trong `UNKNOWN`)
- `DONE_NO_PR` (chỉ khi task không cần PR; ghi rõ lý do)

Không dùng `PASS`, `DONE`, `OK` thay cho trạng thái có thể kiểm.

## 5. Kiểm tra trước khi gửi packet

- [ ] `TASK_ID` khớp tên folder `RUNS/<4 số>-<slug>/`.
- [ ] `INPUT` chỉ gồm đúng file vai đó được phép thấy.
- [ ] `OUTPUT` là đường dẫn file sẽ tạo, không phải nội dung.
- [ ] `CHAT_TITLE` là dòng đầu tiên của prompt `NEW_CHAT`.
- [ ] Có ràng buộc và điều kiện dừng rõ ràng.
- [ ] Không dán nội dung dài vào packet.
- [ ] Không có kết luận của Owner bị đưa vào packet của A/B/C.
- [ ] Mỗi PACKET->A/B/C ghi đúng TRIGGER_MODE/EVIDENCE_MODE; PACKET->B yêu cầu B.md đủ 7 mục (có THU HẸP ĐỀ XUẤT).
