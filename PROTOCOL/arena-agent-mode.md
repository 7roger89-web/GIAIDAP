# PROTOCOL/arena-agent-mode.md — Arena Agent Mode (V1)

TRẠNG THÁI: ACTIVE | NGÀY: 2026-10-26

MỤC ĐÍCH: ghi cái Arena Agent Mode **làm được** và **không làm được**, kèm nguồn + ngày, để A/B/C và tay chân không phải đoán.

PHẠM VI: hành vi quan sát được từ tài liệu chính thức của Arena tại ngày truy cập (2026-10-26) và từ phiên đang chạy. Đây **không phải** tài liệu chính thức của Arena; đây là bản ghi chú của GIAIDAP. Arena có thể đổi sản phẩm bất cứ lúc nào.

Quy ước nhãn: `FACT` | `INFERENCE` | `HYPOTHESIS` | `UNKNOWN` | `OWNER_CONFIRMATION_REQUIRED`.

## 1. Nguồn đã đọc

| ID | Nguồn | Loại | Ngày |
|---|---|---|---|
| S1 | https://help.arena.ai/articles/5432423882-how-to-use-agent-mode | Trang trợ giúp chính thức | Truy cập 2026-10-26; trang ghi "Last updated 17 days ago" (không có ngày tuyệt đối) |
| S2 | https://help.arena.ai/articles/1655691990-how-to-use-coding-in-agent-mode | Trang trợ giúp chính thức | Truy cập 2026-10-26; trang ghi "Last updated 2 months ago" |
| S3 | https://help.arena.ai/articles/5595418316-arena-how-to-file-upload | Trang trợ giúp chính thức | Truy cập 2026-10-26; trang ghi "Last updated 5 days ago" |
| S4 | https://arena.ai/blog/agent-mode | Blog chính thức | Xuất bản 2026-06-04; cập nhật 2026-06-05 |
| S5 | https://arena.ai/blog/coding-in-agent-mode | Blog chính thức | Xuất bản 2026-08-24; cập nhật 2026-08-26 |
| S6 | https://arena.ai/resources/agent-arena-signals | Tài liệu định nghĩa signal | Cập nhật 2026-10-12 |
| S7 | https://arena.ai/leaderboard/agent | Leaderboard công khai | Ảnh chụp 2026-10-23: 2.557.423 phiên, 55 model |
| S8 | https://arena.ai/agent | Trang sản phẩm | Truy cập 2026-10-26 |
| S9 | https://arena.ai/blog/agent-arena-methodology | Blog chính thức | Xuất bản 2026-06-04; cập nhật 2026-10-15 |

Ghi chú: các trang trợ giúp chỉ ghi "Last updated ... days ago", không ghi ngày tuyệt đối. Vì vậy cột NGÀY ở trên là **ngày truy cập**, không phải ngày cập nhật chính xác của trang.

Trong các bảng dưới, `NGÀY` là ngày công bố/cập nhật của nguồn nếu biết; nếu nguồn chỉ là trang sống, đó là ngày truy cập `2026-10-26`.

## 2. Công cụ có gì

| Năng lực | Nhãn | Nguồn | Ngày | Ghi chú |
|---|---|---|---|---|
| Web search | FACT | S1, S4 | 2026-10-26 | Agent tự gọi để tìm thông tin |
| Đọc trang web (fetch page) | FACT | S1 (FAQ "fetching pages") | 2026-10-26 | Dùng để lấy nội dung nguồn |
| Bash trong sandbox | FACT | S1, S4 | 2026-10-26 | Chạy lệnh, git, test, cài package |
| Ghi file | FACT | S1, S2, S5 | 2026-10-26 | Tạo file trong workspace/repo |
| Đọc file | FACT (phiên) | Quan sát trực tiếp phiên 2026-10-26; S1 nói "sandbox/bash" + "write files" | 2026-10-26 | Suy rộng ra mọi phiên là `INFERENCE`, không đảm bảo |
| Sửa file | FACT (phiên) | Quan sát trực tiếp phiên 2026-10-26 | 2026-10-26 | Có thể sửa từng phần, không chỉ ghi đè |
| Tạo ảnh | FACT | S1, S4 | 2026-10-26 | Image generation |
| Hỏi lại / clarifying questions | FACT | S1, S4 | 2026-10-26 | Agent có thể hỏi trước khi làm |
| Upload file | FACT | S1, S3 | 2026-10-26 | Người dùng upload; không phải agent tự tải file bất kỳ |
| Connectors | FACT | S8 | 2026-10-26 | Trang sản phẩm hiển thị: GitHub, Drive, Google Docs, Docs, Notion, Gmail, Linear, Cal |
| Quản lý process nền / image search / speech | FACT (phiên) | Quan sát trực tiếp phiên 2026-10-26 | 2026-10-26 | Có trong phiên này; không thấy liệt kê đầy đủ trong tài liệu công khai => không đảm bảo cho phiên khác |

`FACT (phiên)` = thấy trực tiếp trong phiên đang chạy, chỉ đúng cho phiên đó. Muốn dùng cho phiên khác thì kiểm lại; không có thì ghi `UNKNOWN`.

## 3. Loại file upload được

Theo S3 (trang "How to Upload Files into Arena"), Agent Mode nhận:

| Loại | Đuôi |
|---|---|
| Ảnh | `.png`, `.webp`, `.jpg`, `.jpeg`, `.gif` |
| Tài liệu | `.pdf` |
| Văn bản | `.txt`, `.md`, `.csv` |
| Web/code | `.html`, `.xml`, `.css`, `.js`, `.json` |

Giới hạn upload trong Agent Mode (S3):

- 25 MB mỗi file.
- 10 MB mỗi PDF.
- 50 MB tổng mỗi lượt.

Lưu ý:

- Danh sách chính thức của S1 và S3 **lặp** `.xml` và `.js` hai lần; bảng trên đã gộp, không thêm loại mới.
- Các loại phổ biến như `.py`, `.ts`, `.yaml`, `.yml`, `.zip`, `.docx`, `.xlsx` **không** có trong danh sách chính thức. Không được giả định là upload được => `UNKNOWN`.
- Upload là đầu vào do người dùng cung cấp (S1, S3), không phải quyền để agent tự lấy file từ máy hoặc từ Internet.

## 4. Cách đẩy lên GitHub

| Bước | Dữ kiện | Nhãn | Nguồn | Ngày |
|---|---|---|---|---|
| 1 | Bật GitHub connector, chọn repo và branch | FACT | S5, S2 | 2026-10-26 |
| 2 | Arena clone repo vào sandbox đầu phiên | FACT | S5, S2 | 2026-10-26 |
| 3 | Agent đọc code, sửa file, chạy lệnh; thay đổi hiện trong Diff panel | FACT | S5, S2 | 2026-10-26 |
| 4 | Agent commit vào **nhánh làm việc** và mở **pull request** | FACT | S1, S5 | 2026-10-26 |
| 5 | Review trong tab **Diff** (last turn / full branch), rồi merge hoặc pull branch | FACT | S1, S2, S5 | 2026-10-26 |
| 6 | Mỗi phiên chat hiện chỉ tạo được **một PR** | FACT | S2 | 2026-10-26 |
| 7 | Có cửa sổ **Checks** cho commit/PR (passing, failing, pending) | FACT | S2 | 2026-10-26 |
| 8 | Có thể xem preview nếu prompt nói rõ muốn preview | FACT | S2 | 2026-10-26 |

Hệ quả cho GIAIDAP:

- Một task bounded => một nhánh => một PR, khớp với LUẬT 06 và giới hạn một PR/phiên.
- Không có repo connected: file nằm trong workspace, tải bằng nút **Download** (zip). Có repo connected: **không có zip download**, thay đổi đi qua GitHub (S1).
- Sau khi PR merge hoặc close: phiên **không push được nữa**; file tạo sau mốc đó **không push, không tải, không mang sang phiên mới** (S1). Phải push xong trước khi merge, hoặc mở phiên mới cho việc mới.

### 4.1. `BASE_PHAI_LA_MAIN` (bắt buộc)

- Mọi PR mặc định phải có `baseRefName=main`. Kiểm bằng lệnh thật TRƯỚC khi báo cáo PR và TRƯỚC khi coi một PR là "sẽ vào main": `gh pr view <n> --json baseRefName,state`.
- **Merge xong KHÔNG có nghĩa là đã vào main — chỉ có cây `main` là sự thật.** Một PR `MERGED` với base là nhánh khác chỉ đưa nội dung vào nhánh đó, không vào `main` (FACT 2026-10-27: PR #5 `MERGED` nhưng `baseRefName=arena/b960bf99-giaidap` — nhánh của #4 — nên nội dung #5 không vào main, phải reconcile bằng PR riêng).
- Nếu BUỘC phải stack (PR con có base là nhánh của PR cha): ghi rõ tình trạng stack trong mô tả PR, và (a) merge PR con TRƯỚC PR cha, hoặc (b) retarget PR con về `main` (`gh pr edit <n> --base main`) NGAY khi PR cha merge. Không làm (a) hoặc (b) => nội dung PR con coi như CHƯA tồn tại trên main, dù trạng thái là `MERGED`.
- Khi resume, trạng thái "đã vào main" phải được xác nhận lại bằng `MAIN_CONTENT_CHECK` (`PROTOCOL/resume-protocol.md` §2), không tin giá trị ghi sẵn.

## 5. Giới hạn phiên và model

| Dữ kiện | Nhãn | Nguồn | Ngày |
|---|---|---|---|
| Mỗi phiên Agent Mode được gán một **orchestrator model ngẫu nhiên** | FACT | S1 (FAQ leaderboard) | 2026-10-26 |
| Model được giữ nguyên trong suốt phiên | FACT | S1 (FAQ "It seems like my model changed?") | 2026-10-26 |
| Arena **không tiết lộ** model orchestrator, kể cả sau khi gửi feedback | FACT | S1 | 2026-10-26 |
| Nếu một phản hồi có khả năng thất bại và làm phiên hỏng, hệ thống **có thể tự đổi sang model khác** để phiên tiếp tục | FACT | S1 | 2026-10-26 |
| Vì model bị ẩn, mọi file GIAIDAP phải ghi `MODEL=UNKNOWN` nếu không xác minh được | INFERENCE (từ LUẬT 09 + dữ kiện trên) | S1 + `LAW/00` | 2026-10-26 |

Không được đoán model. Không được ghi "chắc là model X". Nếu Owner cung cấp bằng chứng xác minh được thì ghi kèm nguồn; nếu không, `MODEL=UNKNOWN`.

Leaderboard Agent Arena (S7) xếp hạng các orchestrator model theo tín hiệu, nhưng **không** cho biết model của một phiên cụ thể. Vì vậy leaderboard không dùng để suy ra `MODEL` của phiên đang chạy.

### 5.1. `/download-workspace`

- S1 (FAQ) nói: thêm `/download-workspace` vào cuối URL khi đang xem phiên Agent Mode để tải file workspace mới nhất; đây là workaround cho phiên bị hỏng.
- S1 cũng nói: phiên **có repo connected** thì không có zip download, thay đổi đi qua GitHub.
- Hai câu này va nhau với phiên có repo connected. Cách ghi đúng: `FACT` rằng lệnh `/download-workspace` tồn tại; `INFERENCE` rằng nó có thể là workaround; `UNKNOWN` rằng nó có tải được file trong phiên có repo connected hay không, và có tải được sau khi PR merge/close hay không.
- Quy tắc an toàn: **push trước khi merge**. Không dựa vào `/download-workspace` sau khi PR đã đóng.

## 6. Quy tắc tiêu đề chat

- **Quy ước GIAIDAP** (từ LUẬT 08): với `CHAT_MODE=NEW_CHAT`, **dòng không trống đầu tiên** của prompt là tiêu đề người đọc được, đúng format `<PROJECT> — <bounded task/outcome>`, front-load từ phân biệt được; **cấm** boilerplate ở dòng đầu (`GỬI CHO:`, `DESTINATION=`, `TASK_ID=`, code fence, prefix `P2P` chung); `CHAT_TITLE` phải **bằng đúng** dòng đó. Dòng 2 trở đi mới là yêu cầu chi tiết.
- **Trạng thái nguồn:** không tìm thấy tài liệu chính thức của Arena nói rằng Arena tự lấy dòng đầu tiên làm tiêu đề chat => đây là **quy ước vận hành của GIAIDAP**, không phải `FACT` về sản phẩm Arena. Hành vi UI thực tế: `UNKNOWN`.
- Cách áp dụng an toàn: vẫn viết dòng 1 là tiêu đề; đồng thời ghi `CHAT_TITLE` trong packet để người mở chat copy đúng. Không giả định Arena sẽ parse tiêu đề từ dòng 1.

## 7. Cách trả lời dialog feedback

### 7.1. Dữ kiện chính thức

| Dữ kiện | Nhãn | Nguồn | Ngày |
|---|---|---|---|
| Arena có nút approve/disapprove ở mỗi lượt; dùng quyết định cuối cùng của cả task để tính Confirmed Success | FACT | S1, S6, S9 | 2026-10-26 (S6 cập nhật 2026-10-12; S9 cập nhật 2026-10-15) |
| Pop-up hỏi "Did this complete your task?"; bấm "yes" mới tính confirmed success, "no" thì không | FACT | S6 | 2026-10-12 |
| Không có partial credit; "perfect, thanks" hoặc bấm accept **không** tự động tính confirmed | FACT | S6 | 2026-10-12 |
| Task bị bỏ dở, người dùng rời đi hoặc không trả lời sau lượt cuối **không** tính confirmed | FACT | S6 | 2026-10-12 |
| Khi task xong, người dùng có thể phản hồi để tiếp tục hoặc chọn "keep working" | FACT | S1 | 2026-10-26 |

### 7.2. Quy tắc trả lời của GIAIDAP

Cách hiểu của GIAIDAP (không phải định nghĩa chính thức của Arena):

| Tình huống | Trả lời | Lý do |
|---|---|---|
| Task đã chạm đúng **trạng thái terminal** mà Owner yêu cầu, có bằng chứng trong phạm vi | `YES` / approve | Xác nhận kết quả thật, không phải "cho xanh" |
| Còn việc, còn `UNKNOWN` ảnh hưởng nghiệm thu, hoặc bằng chứng chưa đủ | `KEEP WORKING` / để mở | Không đóng task non |
| Task thất bại thật, không đạt tiêu chí, hoặc bị chặn không thể tiếp tục | `NO` / disapprove | Ghi nhận thất bại thật |

- `YES` **không** đồng nghĩa với "PASS kỹ thuật". Một CI xanh, test mock hay preview chỉ là bằng chứng cục bộ; nếu nghiệm thu cần runtime thật / nội dung thật / quy trình thật thì phải có bằng chứng tương ứng (LUẬT 03). Ngược lại, không bắt buộc phải có một "PASS kỹ thuật" nếu trạng thái terminal yêu cầu đã đạt và có bằng chứng phù hợp.
- `KEEP WORKING` dùng khi còn việc thật hoặc còn `UNKNOWN` chưa xử lý. Không dùng `YES` để kết thúc phiên cho nhanh.
- `NO` dùng khi thất bại thật. Không dùng `NO` để "phạt" một task còn làm tiếp được.
- Sau khi chọn, ghi kết quả vào `RUNS/<id>/DECISION.md` hoặc `RETURN_PACKET->OWNER`.

**UNKNOWN:** không tìm thấy tài liệu chính thức dùng đúng câu "Was this task successful?" với ba nút `YES` / `KEEP WORKING` / `NO`. Tài liệu chính thức dùng "Did this complete your task?" (yes/no) và "keep working" (S1, S6). Nếu UI thực tế khác, map theo **ngữ nghĩa** ở bảng trên và ghi `UI_WORDING=UNKNOWN` trong biên bản.

### 7.3. Owner phê duyệt merge bằng MERGE_OK

Agent ĐƯỢC tự merge PR do chính nó mở SAU KHI Owner đã comment đúng chuỗi MERGE_OK trên PR đó; kiểm bằng `gh pr view <n> --json comments` (grep MERGE_OK) TRƯỚC khi merge; không có comment MERGE_OK thì không merge. Owner comment = phê duyệt, agent merge chỉ là thao tác cơ học, không phải tự chứng nhận.

## 8. Danh sách UNKNOWN

1. Hành vi UI chính xác của tiêu đề chat (Arena có tự lấy dòng đầu tiên làm tiêu đề không).
2. Câu chữ và bố cục chính xác của dialog feedback (`Was this task successful?` / 3 nút).
3. `/download-workspace` có hoạt động trong phiên có repo connected và sau khi PR merge/close không.
4. Các loại file ngoài danh sách chính thức (`.py`, `.ts`, `.yaml`, `.zip`, `.docx`, `.xlsx`, ...) có upload được không.
5. Danh sách công cụ đầy đủ của mọi phiên (một số công cụ chỉ quan sát được trong phiên này).
6. Model orchestrator của phiên hiện tại (Arena không tiết lộ).
7. Ngày cập nhật tuyệt đối của các trang trợ giúp (chỉ có "last updated ... days ago").

## 9. Checklist trước khi mở phiên

- [ ] Đã đọc `LAW/00-SUPREME-LAW.md` và phát `LAW_CHECK` (SHA-256 thật).
- [ ] Đã đọc `STATE.md` và phát `RESUME_CHECK`: so `sha256sum` thật (`LAW_HASH_MATCH`, `PROTOCOL_HASH_MATCH`, `SKILL_HASH_MATCH`), kiểm `STATE_TRUST=OK|DRIFT`, và xử lý `POST_MERGE_RECONCILE` nếu là phiên đầu sau merge (`PROTOCOL/resume-protocol.md §13`).
- [ ] Task bounded; một nhánh; một PR.
- [ ] Nguồn cho mọi dữ kiện dễ cũ có ngày kiểm.
- [ ] `UNKNOWN` được liệt kê, không bị giấu.
- [ ] Không merge; dừng sau khi mở PR.
