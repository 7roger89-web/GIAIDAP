# PROTOCOL/handoff-packet.md — Mẫu packet bàn giao

TRẠNG THÁI: ACTIVE | NGÀY: 2026-10-26

Quy tắc chung:

- Mỗi packet = một vai = một phiên/lần chạy.
- `INPUT` ghi **đường dẫn file**, không dán nội dung dài.
- Dòng đầu tiên của prompt `NEW_CHAT` là `CHAT_TITLE` (LUẬT 08).
- Không đưa `A.md`/`B.md`/`C.md` hoặc kết luận của Owner vào packet sai vai.
- Ghi rõ ràng buộc và điều kiện dừng. Hết điều kiện dừng là dừng, không tự mở vòng mới.
- Ba packet `PACKET->A/B/C` dùng đủ 8 trường: `TASK_ID`, `ROLE`, `CHAT_MODE`, `CHAT_TITLE`, `INPUT`, `OUTPUT`, `RÀNG BUỘC`, `ĐIỀU KIỆN DỪNG`.
- `RETURN_PACKET->OWNER` dùng 6 trường báo cáo: `STATUS`, `PR`, `FILES`, `LAW_SOURCE`, `UNKNOWN`, `NEXT_ONE_ACTION`.

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
- Không viết lại đề xuất của A; không phán quyết thay C.
- Ghi header chuẩn 6 trường; MODEL=UNKNOWN nếu không xác minh được.
ĐIỀU KIỆN DỪNG: B.md đã ghi đủ 6 mục + header + LAW_CHECK; không mở vòng mới.
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
