# PROTOCOL/resume-protocol.md — Thủ tục cold-start (hồi sinh)

TRẠNG THÁI: ACTIVE | NGÀY: 2026-10-27

MỤC ĐÍCH: một model mới, ở phiên mới, không có ký ức chat, chỉ đọc file trong repo mà biết đang ở đâu, biết việc kế tiếp, chứng minh đã đọc đúng bản, và ghi lại được việc đã làm.

## 1. Thứ tự cold-start

Đọc theo đúng thứ tự:

1. `AGENTS.md`
2. `STATE.md`
3. `LAW/00-SUPREME-LAW.md`
4. `PROTOCOL/multi-brain-loop.md`
5. `RUNS/INDEX.md`
6. `KB/INDEX.md`

`STATE.md` đọc TRƯỚC luật để biết mình đang ở đâu, nhưng biên lai `LAW_CHECK` vẫn phát riêng và vẫn bắt buộc. `STATE.md` không thay thế luật.

## 2. Biên lai hồi sinh

Phát ngay sau `LAW_CHECK`, trước khi làm việc thật:

```text
RESUME_CHECK=PASS | STATE_HEAD=<sha trong STATE.md> | READ_HEAD=<sha thật> | OPEN=<RUN_ID|NONE> | NEXT=<...> | LAW_CHANGED_SINCE_STATE=<YES|NO>
```

Khi không đối chiếu được:

```text
RESUME_CHECK=BLOCKED | REASON=<lý do>
```

## 3. Quy tắc đối chiếu

Tính `git diff --name-only STATE_HEAD..READ_HEAD`, trong đó `STATE_HEAD` là giá trị `SINH_TỪ_HEAD` trong `STATE.md` và `READ_HEAD` là HEAD thật lúc đọc.

- Nếu diff rỗng, hoặc chỉ chạm `STATE.md` / `RUNS/` / `KB/` -> `PASS`.
- Nếu diff chạm `LAW/` hoặc `PROTOCOL/` -> vẫn `PASS` nhưng bắt buộc `LAW_CHANGED_SINCE_STATE=YES` và phải đọc lại đúng file đã đổi trước khi làm việc.
- Nếu `STATE.md` không tồn tại, hoặc `STATE_HEAD` không phải tổ tiên của HEAD -> `BLOCKED`, ghi rõ chênh lệch, KHÔNG làm việc thật.

Kiểm tổ tiên: `git merge-base --is-ancestor <STATE_HEAD> HEAD`.

## 4. Quy tắc ghi lại (write-back)

Sau mỗi việc bounded, cập nhật `STATE.md` + `RUNS/INDEX.md` trong cùng commit. Không cập nhật thì việc đó coi như không tồn tại với model sau.

## 5. Quy tắc chống trôi

- Model mới KHÔNG được hỏi lại Owner những gì repo đã trả lời được.
- KHÔNG được đoán `NEXT_ONE_ACTION`; chỉ lấy từ `STATE.md` / `DECISION.md`.
- KHÔNG được coi `STATE.md` là thẩm quyền thay luật. Luật duy nhất là `LAW/00-SUPREME-LAW.md`.

## 6. Nhãn MODEL và truy vết phiên

Arena ẩn model nên luôn ghi `MODEL=UNKNOWN`. Bù lại, mọi file output phải ghi `SESSION_REF` (tên nhánh/PR) và `PR_HEAD_SHA` để truy vết được phiên nào làm ra cái gì.

## 7. Liên hệ với LAW_CHECK

`RESUME_CHECK` không thay `LAW_CHECK`. Thiếu một trong hai biên lai hợp lệ thì không làm việc thật.

## 8. NGHIỆM THU

Đây là nghiệm thu cần PHIÊN MỚI thật, không tự chấm trong phiên này.

- T1 — Cold start: Owner mở phiên mới (khác model), dán câu lệnh ở mục 9. Đạt khi: model phát `LAW_CHECK=PASS` với SHA thật, phát `RESUME_CHECK=PASS` với đúng `OPEN` và đúng `NEXT_ONE_ACTION`, không hỏi lại.
- T2 — Đọc lịch sử: model phải nêu đúng RUN đang mở, verdict gần nhất của B, và 2 quyết định gần nhất của Owner — CHỈ từ file, không từ chat.
- T3 — Chống trôi: model phải từ chối đoán; chỗ không có bằng chứng phải ghi `UNKNOWN`.
- T4 — Ghi lại: model làm 1 việc bounded rồi cập nhật `STATE.md` + `RUNS/INDEX.md` trong cùng commit.

## 9. PROMPT DÁN VÀO PHIÊN MỚI

```text
Đọc repo https://github.com/7roger89-web/GIAIDAP theo đúng thứ tự trong AGENTS.md, phát LAW_CHECK và RESUME_CHECK, rồi báo: việc đang mở, NEXT_ONE_ACTION, BLOCKER, UNKNOWN. Không đoán, không hỏi lại nếu repo đã trả lời được.
```
