# PROTOCOL/multi-brain-loop.md — Vòng A/B/C + Arena tay chân

TRẠNG THÁI: ACTIVE | NGÀY: 2026-10-26

MỤC ĐÍCH: tạo phán quyết có kiểm chứng, không phải cuộc thi "ai nói nghe hợp lý".

## 0. Nguyên tắc

- Một `RUN` = một câu hỏi bounded.
- A, B, C độc lập. Arena là tay chân, **không phán xử**.
- Luật là **meta**: mọi vai đều phải đọc `LAW/00-SUPREME-LAW.md` để phát biên lai; việc đọc luật không tính là nội dung bài toán và không được dùng để gợi ý kết quả.
- Không có bằng chứng => `UNKNOWN`, không bịa.

## 1. Sơ đồ

```text
QUESTION.md (câu hỏi thô)
   |
   +--> A (chỉ QUESTION.md) -----------------> A.md
   |
   +--> B (QUESTION.md + A.md) --------------> B.md
   |
   +--> C (QUESTION.md + A.md + B.md) -------> C.md
                                                   |
                                                   v
                                              DECISION.md
                                      (C verdict + Owner decision)
```

Arena: ghi file vào `RUNS/`, chạy search khi được yêu cầu, mở PR; không sửa nội dung A/B/C và không sửa phán quyết của C.

## 2. Vai và phạm vi input

| Vai | Chỉ nhận | Không được xem | Xuất | Phải trả lời |
|---|---|---|---|---|
| **A — Proposer** | `QUESTION.md` (câu hỏi thô) | A/B/C của vòng khác, kết luận của Owner, KB kết luận | `A.md` | Đề xuất gì? Giả định gì? Độ tin cậy? `UNKNOWN` nào? |
| **B — Challenger / Verifier** | `QUESTION.md` + `A.md` | C, kết luận của Owner, chat của A, tài liệu ngoài 2 file (kể cả web search) | `B.md` | A sai/thiếu ở đâu? Phản ví dụ? Nguồn đối lập **đã có trong 2 file**? A tự mâu thuẫn chỗ nào? |
| **C — Judge / Synthesizer** | `QUESTION.md` + `A.md` + `B.md` | Kết luận của Owner, chat của A/B, tài liệu ngoài 3 file | `C.md` | Phán quyết? Lý do? Độ tin cậy? Còn `UNKNOWN` gì? Cần kiểm thêm gì? |

- **A** không nhận `A.md` cũ, không nhận `B.md`, không nhận `C.md`. Nếu Owner muốn A xét lại, đó là một `RUN` mới.
- **B** không được xem gì khác ngoài câu hỏi và `A.md`. Không đọc `C.md`, không đọc kết luận của Owner, không đọc chat của A.
- **C** không được xem gì khác ngoài câu hỏi, `A.md`, `B.md`.

## 3. Cách ly thật

- A/B/C phải **khác model hoặc khác phiên** để có "độc lập thật".
- Một phiên tự đóng vai A, rồi B, rồi C **không phải** A/B/C. Nếu buộc phải làm vậy, ghi `INDEPENDENCE=WEAK` và không được coi là phán quyết độc lập.
- Arena ẩn model: mỗi file phải ghi `MODEL=UNKNOWN` nếu không xác minh được. Không đoán model.
- Không copy `LAW_CHECK` của vai khác. Mỗi vai phát biên lai riêng.
- Không rò rỉ nội dung: A không thấy B/C; B không thấy C; C chỉ thấy đúng 3 file.
- Nếu một vai đã thấy tài liệu ngoài phạm vi, ghi rõ trong `INPUT_REF` (ví dụ `+ extra: ...`) và đánh dấu `CONTAMINATED=YES`. Owner quyết định mở RUN mới.
- **B chỉ được dẫn nguồn đã có trong `QUESTION.md` hoặc `A.md`.** B không tự tra web, không tự mở tài liệu ngoài. Nếu buộc phải tra ngoài: dừng, ghi `CONTAMINATED=YES | NGOÀI_PHẠM_VI=<cái gì>`, **kết quả RUN hiện tại không dùng làm phán quyết**, và Owner mở RUN mới.
- C cũng chỉ đối chiếu trong 3 file; nếu C phải tra ngoài thì áp cùng quy tắc `CONTAMINATED=YES`.

## 4. Header chuẩn mỗi file

Mọi file `A.md`, `B.md`, `C.md` mở đầu bằng đúng 6 trường, mỗi trường một dòng. Khối dưới đây là **TEMPLATE** cho `A.md` (không phải biên lai thật); `B.md` thêm `A.md`, `C.md` thêm `A.md` + `B.md` vào `INPUT_REF`:

```text
RUN_ID: 0001-nhap-khau-binh-nong-lanh
ROLE: A
INPUT_REF: RUNS/0001-nhap-khau-binh-nong-lanh/QUESTION.md
DATE: 2026-10-26
MODEL: UNKNOWN
LAW_CHECK: PASS | SOURCE=LAW/00-SUPREME-LAW.md | SOURCE_SHA256=<SHA256> | DATE=2026-10-26
```

- `RUN_ID`: 4 số + slug, khớp tên folder.
- `ROLE`: `A`, `B` hoặc `C` (kèm tên vai nếu muốn).
- `INPUT_REF`: đường dẫn file thật, không dán nội dung dài.
- `DATE`: ngày viết file, `YYYY-MM-DD`.
- `MODEL`: tên model nếu xác minh được; nếu không, `UNKNOWN`.
- `LAW_CHECK`: `PASS | SOURCE=... | SOURCE_SHA256=... | DATE=...` hoặc `BLOCKED | REASON=...`.
- **Riêng `B.md`** (và mọi file `B*.md`): bắt buộc thêm **2 trường hash tách riêng**, mỗi trường một dòng:
  - `CONTENT_SHA256_B_DECLARED=...`: giá trị B tự khai. B không khai ⇒ `UNKNOWN`; người ghi file **không** được điền thay.
  - `CONTENT_SHA256_WRITER_COMPUTED=...`: người ghi file tự băm.
  - Hai trường này **khác nguồn, không được thay thế nhau**. Quy ước băm: bỏ hẳn dòng `CONTENT_SHA256_WRITER_COMPUTED=...` (một dòng không thể băm chính nó) rồi `sha256sum` phần còn lại.

## 5. Nội dung tối thiểu

### A.md

- `## ĐỀ XUẤT` — phương án A chọn, phạm vi áp dụng.
- `## GIẢ ĐỊNH` — điều A đang tin là đúng nhưng chưa kiểm.
- `## ĐỘ TIN CẬY` — `CAO | TRUNG BÌNH | THẤP`, kèm lý do ngắn.
- `## UNKNOWN` — điều A không biết; nếu không có, ghi `UNKNOWN=NONE`.
- `## NGUỒN` — link/tài liệu A dùng; không bịa.

### B.md

- `## LỖI` — lỗi logic, lỗi dữ kiện, lỗi phạm vi.
- `## THIẾU` — bằng chứng/khía cạnh A bỏ sót.
- `## PHẢN VÍ DỤ` — trường hợp làm đề xuất A sai hoặc không đủ.
- `## NGUỒN ĐỐI LẬP` — nguồn mâu thuẫn với A **và đã có trong QUESTION.md/A.md**, kèm ngày. Muốn dẫn nguồn ngoài 2 file => xem §3, phải ghi `CONTAMINATED=YES` và mở RUN mới.
- `## A TỰ MÂU THUẪN` — chỗ A nói hai điều không khớp.
- `## UNKNOWN` — điều B không kiểm được.

### C.md

- `## PHÁN QUYẾT` — chọn phương án, bác một phần, hay `UNKNOWN`.
- `## LÝ DO` — đối chiếu bằng chứng A/B, không dựa vào giọng văn.
- `## ĐỘ TIN CẬY` — `CAO | TRUNG BÌNH | THẤP`, kèm lý do.
- `## UNKNOWN` — điều còn chưa biết; nếu không có, ghi `UNKNOWN=NONE`.
- `## VIỆC CẦN KIỂM THÊM` — nếu cần; không tự mở vòng mới.

## 6. Luật cho C

C **không được** chọn bên nghe hợp lý hơn. C phải:

1. Liệt kê từng claim quan trọng của A và B.
2. Gắn bằng chứng/nguồn cho từng claim; claim không có nguồn => đánh dấu `UNKNOWN` hoặc `INFERENCE`.
3. So sánh bằng chứng, không so sánh văn phong, độ dài, độ tự tin.
4. Chấp nhận cả hai đúng một phần; phán quyết có thể có phạm vi.
5. Không nâng `INFERENCE` thành `FACT`; không bịa nguồn.
6. Nếu bằng chứng ngang nhau => `VERDICT=UNKNOWN` + `NEXT_ONE_ACTION` (ví dụ: cần kiểm nguồn X).
7. Không dùng "có vẻ hợp lý", "nghe đúng" làm lý do chính.

## 7. Arena — tay chân

Arena **được**:

- Ghi `QUESTION.md`, `A.md`, `B.md`, `C.md`, `DECISION.md` đúng đường dẫn.
- Chạy search khi Owner hoặc packet yêu cầu, để kiểm nguồn; ghi link vào `DECISION.md` mục `SOURCES`, không sửa verdict của C.
- Mở một PR duy nhất trên nhánh làm việc.
- Trả `RETURN_PACKET->OWNER`.

Arena **không được**:

- Phán quyết thay C.
- Viết lại, tóm tắt làm đổi nghĩa A/B/C.
- Đưa nội dung A cho B/C ngoài file, hoặc đưa C cho A/B.
- Tự nhận PASS, tự merge PR, tự mở vòng 2.
- Đóng vai A/B/C trong cùng một phiên.

Nếu Arena phải vừa là tay chân vừa là một não: dùng **phiên khác** cho não đó, ghi `MODEL=UNKNOWN`, và ghi rõ `INDEPENDENCE=SESSION_SEPARATE`.

## 8. Điều kiện dừng

- **C ra phán quyết + liệt kê `UNKNOWN` thì dừng.**
- Nếu C ra `VERDICT=UNKNOWN`, vẫn dừng: ghi `NEXT_ONE_ACTION`, không tự lặp.
- Không tự chạy vòng A/B/C thứ hai trong cùng RUN. Cần vòng mới => Owner mở RUN mới.
- Không có "chờ thêm ý kiến" vô hạn; hết vòng là hết.

## 9. Khi nào mở RUN mới

- Câu hỏi mới, phạm vi mới, hoặc Owner đổi tiêu chí nghiệm thu.
- Có bằng chứng mới làm phán quyết cũ hết hiệu lực.
- RUN cũ bị `CONTAMINATED=YES`.
- Muốn A xét lại sau khi C đã phán quyết.

Không sửa `A.md`/`B.md`/`C.md` của RUN cũ sau khi C đã đọc. Mở folder mới.

## 10. Checklist

- [ ] `RUN_ID` khớp folder.
- [ ] Mỗi vai chỉ thấy đúng input của mình.
- [ ] Mỗi file có đủ 6 dòng header.
- [ ] `MODEL=UNKNOWN` nếu không xác minh được.
- [ ] C đối chiếu bằng chứng, không chọn theo cảm giác.
- [ ] C có `VERDICT` + `UNKNOWN`.
- [ ] Arena không phán quyết, không merge.
