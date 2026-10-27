# PROTOCOL/resume-protocol.md — Giao thức hồi sinh phiên mới (Cold-Start & Write-Back)

TRẠNG THÁI: ACTIVE | NGÀY: 2026-10-27

MỤC ĐÍCH: giúp một model mới, ở phiên mới, không có ký ức chat, chỉ đọc file trong repo là biết chính xác đang ở đâu, biết việc kế tiếp, chứng minh được đã đọc đúng bản, làm tiếp một đơn vị việc bounded và ghi lại cho phiên sau.

## 1. Thứ tự đọc cold-start

Phiên mới vào repo đọc theo thứ tự:

1. `AGENTS.md`
2. `STATE.md`
3. `LAW/00-SUPREME-LAW.md`
4. `PROTOCOL/resume-protocol.md` và `PROTOCOL/multi-brain-loop.md`
5. `PROTOCOL/cach-nghi.md`
6. `RUNS/INDEX.md`
7. `KB/INDEX.md`

> **Bất biến:** thứ tự đọc ở `AGENTS.md` (đoạn mở đầu) và `PROTOCOL/resume-protocol.md §1` — **hai chỗ phải mô tả cùng một thứ tự**; sửa một bên thì phải sửa bên kia trong cùng commit. Nếu lệch, phiên mới đọc sai ngay từ bước 1.

Quy tắc định vị:

- **`STATE.md` đọc TRƯỚC `LAW/00-SUPREME-LAW.md`** để biết ngay repo đang ở đâu, việc gì đang mở và hash kỳ vọng là gì.
- **Nhưng `STATE.md` không thay thế việc đọc luật:** biên lai `LAW_CHECK` vẫn bắt buộc phải phát riêng từ nội dung thật của `LAW/00-SUPREME-LAW.md` (`sha256sum` thật) trước khi làm bất kỳ việc thật nào.
- Trước khi đề xuất phương án mới, bắt buộc đọc thêm `REGISTER/BAC.md` để không mở lại phương án đã bị bác.
- Xem §8 về phân tầng bộ đọc khi vai chỉ làm việc hẹp.

## 2. Biên lai hồi sinh (`RESUME_CHECK`)

Ngay sau dòng `LAW_CHECK`, mọi phiên tiếp việc phải phát biên lai `RESUME_CHECK`.

- Nếu packet của việc có trường `RESTATE` (mọi packet theo `PROTOCOL/handoff-packet.md` bản 10 trường đều có), phát `RESTATE` **trước cả `LAW_CHECK`**; thứ tự output là `RESTATE` → `LAW_CHECK` → `RESUME_CHECK`. Quy tắc lệch packet: `PROTOCOL/cach-nghi.md` §1.

Hai khối dưới đây là **TEMPLATE**, không phải biên lai thật:

```text
RESUME_CHECK=PASS | STATE_HEAD=<sha> | READ_HEAD=<sha> | LAW_HASH_MATCH=<YES|NO> | PROTOCOL_HASH_MATCH=<YES|NO> | SKILL_HASH_MATCH=<YES|NO> | POST_MERGE_RECONCILE=<NEEDED|DONE> | MAIN_CONTENT_CHECK=<PASS|FAIL> | OPEN=<...> | NEXT=<...>
```

```text
RESUME_CHECK=BLOCKED | REASON=<...>
```

Quy tắc kiểm hash:

- **Dùng SO HASH (`sha256sum`), KHÔNG dùng `git diff <A>..<B>`** (diff-range vỡ ở ranh giới merge commit, squash merge và clone nông).
- Tính `sha256sum` thực tế tại `READ_HEAD` cho:
  - `LAW/00-SUPREME-LAW.md` → so với `LAW_SHA256` trong `STATE.md` (`LAW_HASH_MATCH=YES|NO`).
  - Từng file trong `PROTOCOL/` → so với danh sách `PROTOCOL_HASHES` trong `STATE.md`; chỉ `YES` khi mọi file trong `PROTOCOL/` đều có mặt và khớp hash (`PROTOCOL_HASH_MATCH=YES|NO`).
  - `scope-reality-check/SKILL.md` → so với `SKILL_HASH` trong `STATE.md` (`SKILL_HASH_MATCH=YES|NO`).
- **Hash khớp (`YES`)**: trong cùng phiên không cần đọc lại file đã đọc; trong phiên mới (`NEW_CHAT`), chỉ đọc đúng các file thuộc bộ đọc của vai hiện tại (§8).
- **Hash lệch (`NO`)**: file đó đã đổi so với lúc ghi `STATE.md` => **bắt buộc đọc lại toàn bộ đúng file bị lệch** trước khi làm việc, đồng thời kiểm `STATE_TRUST` (§3).
- **`POST_MERGE_RECONCILE=NEEDED|DONE`**: `NEEDED` = đây là phiên ĐẦU TIÊN sau một merge mà `STATE.md` chưa được đối chiếu với `main` thật; `DONE` = đã đối chiếu xong (xem §13). Khi `NEEDED`, phải chạy §13 TRƯỚC mọi việc bounded khác.
- **`MAIN_CONTENT_CHECK=PASS|FAIL`** (bắt buộc MỖI lần resume, không chỉ sau merge):
  - (a) re-verify `PR_STATE` bằng `gh` thật (`gh pr list --state all` hoặc `gh pr view <n> --json state,baseRefName,mergedAt`) cho các PR ghi trong `STATE.md` — **KHÔNG tin giá trị ghi sẵn trong `STATE.md`**;
  - (b) với MỖI việc `STATE.md` khai là "đã có trên main", grep cây `main` thật để xác nhận nội dung thực sự nằm trên `main` (ví dụ `git show origin/main:<file> | grep '<chuỗi đặc trưng>'` sau khi `git fetch origin main`);
  - (c) bất kỳ chỗ nào lệch => ghi `MAIN_CONTENT_CHECK=FAIL` + `STATE_TRUST=DRIFT` (§3), báo rõ chỗ lệch, **KHÔNG tự sửa** khi chưa được giao.
  - Lý do tồn tại (FACT 2026-10-27): PR #5 `MERGED` nhưng base là nhánh của #4 nên nội dung không vào `main`, trong khi trạng thái ghi sẵn khiến phiên sau tưởng đã xong — chỉ có cây `main` là sự thật (`PROTOCOL/arena-agent-mode.md` §4.1 `BASE_PHAI_LA_MAIN`).

## 3. Đối chiếu độ tin cậy trạng thái (`STATE_TRUST`)

Khi đọc `STATE.md`, đối chiếu chéo với `RUNS/INDEX.md` và `DECISION.md` của mọi `RUN` đang `OPEN`:

- Khớp hoàn toàn về danh sách `RUN` đang mở, trạng thái `OPEN`/`CLOSED` và `NEXT_ONE_ACTION` => ghi `STATE_TRUST=OK`.
- Bất kỳ chỗ nào lệch (ví dụ `STATE.md` ghi `NONE` nhưng `RUNS/INDEX.md` còn `OPEN`, hoặc `NEXT_ONE_ACTION` va nhau, hoặc `HASH_MATCH=NO` do quên cập nhật `STATE.md`) => ghi `STATE_TRUST=DRIFT`, **bắt buộc báo rõ chỗ lệch**, **KHÔNG tự ý sửa ngầm** khi chưa được giao.

## 4. Điều kiện chặn (`BLOCKED`) và quan hệ tổ tiên

Phát `RESUME_CHECK=BLOCKED` và dừng ngay (không làm việc thật) khi gặp một trong các trường hợp:

1. `STATE.md` không tồn tại hoặc thiếu các trường bắt buộc (`SINH_TỪ_HEAD`, `LAW_SHA256`, `PROTOCOL_HASHES`, `SKILL_HASH`, `NEXT_ONE_ACTION`).
2. `STATE_HEAD` (`SINH_TỪ_HEAD` trong `STATE.md`) **không phải tổ tiên** của `READ_HEAD` (`HEAD` hiện tại; tính cả trường hợp `STATE_HEAD == READ_HEAD`).

Quy ước kỹ thuật bắt buộc:

- Một commit không thể chứa SHA của chính nó. Vì vậy `SINH_TỪ_HEAD` là SHA commit của `HEAD` bền vững tại thời điểm ghi `STATE.md` (khi mở nhánh PR từ `main`, ghi SHA của `main` làm gốc để quan hệ tổ tiên không bị đứt nếu PR được squash-merge hoặc rebase-merge).
- **Lưu ý môi trường clone nông (shallow clone) trên Arena:** sandbox mặc định clone với `--depth=1` (`git rev-parse --is-shallow-repository` trả về `true`), nên thiếu lịch sử cha trong `.git/objects`. Trước khi chạy `git merge-base --is-ancestor <STATE_HEAD> HEAD`, phải chạy `git fetch --unshallow` (hoặc đối chiếu qua GitHub API `compare/<STATE_HEAD>...<READ_HEAD>` đạt `ahead` hoặc `identical`). Không xác minh được quan hệ tổ tiên => phát `RESUME_CHECK=BLOCKED | REASON=CANNOT_VERIFY_ANCESTRY`, không đoán mò là `PASS`.

## 5. Quy tắc ghi ngược (`Write-back`)

- Sau mỗi đơn vị việc bounded làm thay đổi trạng thái công việc, mở/đóng `RUN`, đổi `NEXT_ONE_ACTION`, có quyết định mới của Owner, hoặc sửa `LAW/` · `PROTOCOL/` · `scope-reality-check/SKILL.md`: người làm **bắt buộc cập nhật `STATE.md` + `RUNS/INDEX.md` (và `REGISTER/BAC.md` nếu có phương án bị bác) TRONG CÙNG COMMIT**.
- Không cập nhật => phần việc đó coi như **không tồn tại** đối với model phiên sau (hoặc gây `STATE_TRUST=DRIFT`).
- **`STATE.md` là file ghi CUỐI CÙNG của phiên.** Sau khi ghi `STATE.md`, nếu còn sửa file khác (đặc biệt `LAW/` · `PROTOCOL/` · `scope-reality-check/SKILL.md`) thì **PHẢI tính lại và cập nhật lại MỌI hash** trong `STATE.md` (`LAW_SHA256`, 4 dòng `PROTOCOL_HASHES`, `SKILL_HASH`) bằng `sha256sum` của bản SAU khi sửa. Lý do: hash cũ sẽ lệch, phiên sau phát `*_HASH_MATCH=NO` và nghi ngờ oan (tự mục). Ghi `STATE.md` cuối cùng là cách đơn giản nhất để 6 hash luôn khớp (LUẬT 05).
- **LỊCH SỬ GẦN NHẤT có trần 8 dòng — đẩy xuống `REGISTER/LICH-SU.md` (append-only), KHÔNG xóa.** Khi `STATE.md > LỊCH SỬ GẦN NHẤT` đã có 8 dòng mà cần ghi thêm 1 dòng mới: đẩy đúng **1 dòng CŨ NHẤT** (cuối danh sách) xuống `REGISTER/LICH-SU.md` — ghi thêm một dòng `- [đẩy <ngày>] <nguyên văn dòng cũ>` vào CUỐI file đó, rồi mới thêm dòng mới lên ĐẦU `STATE.md`. `REGISTER/LICH-SU.md` là sổ dài hạn append-only: không sửa, không xóa, không sắp xếp lại dòng đã lưu; `STATE.md` vẫn chỉ giữ 8 dòng gần nhất.
- Ghi nhận trung thực: cổng kết phiên này là **kỷ luật tự nguyện bằng giấy tờ** — repo không có CI/hook cưỡng chế (LUẬT 05).

## 6. Kỷ luật chống trôi

- **Không hỏi lại Owner** những gì file trong repo (`STATE.md`, `DECISION.md`, `REGISTER/BAC.md`, `LAW/00`, `PROTOCOL/`) đã trả lời rõ.
- **Không đoán `NEXT_ONE_ACTION`:** nếu repo ghi rõ thì đọc đúng câu đó; nếu mơ hồ hoặc mâu thuẫn thì báo `UNKNOWN` / `CONFLICT=YES`.
- **`STATE.md` không phải thẩm quyền thay luật:** `STATE.md` chỉ là bảng định vị và con trỏ, không được chứa điều luật mới và không cấp quyền vượt `LAW/00`.

## 7. Danh tính phiên khi model bị ẩn

- Arena ẩn model orchestrator (`PROTOCOL/arena-agent-mode.md` §5), nên mọi file output mặc định ghi `MODEL=UNKNOWN` trừ khi có nguồn xác minh độc lập.
- Để truy vết thay cho tên model, **mọi file output mới bắt buộc ghi thêm hai trường mở rộng:**
  - `SESSION_REF`: định danh phiên hoặc nhánh làm việc của phiên (ví dụ `arena/b960bf99-giaidap`).
  - `PR_HEAD_SHA`: SHA commit của `HEAD` tại thời điểm ghi file (nếu ghi từ phiên ngoài kiểm một PR đã đẩy thì ghi SHA head của PR đó; nếu ghi ngay trong commit mới thì ghi SHA `HEAD` ngay trước khi tạo commit vì một commit không thể chứa SHA của chính nó — xem `PROTOCOL/multi-brain-loop.md` §4).

## 8. Phân tầng bộ đọc (tiết kiệm ngữ cảnh, đọc đủ là dừng)

- **`BỘ ĐỌC TỐI THIỂU` (luôn đọc ở mọi phiên):**
  `AGENTS.md`, `STATE.md`, `LAW/00-SUPREME-LAW.md`, `PROTOCOL/resume-protocol.md`, `PROTOCOL/cach-nghi.md`.
- **`ĐỌC KHI CẦN` (theo nhiệm vụ):**
  `PROTOCOL/multi-brain-loop.md` (khi chạy/kiểm vòng A/B/C hoặc dùng binding skill), `PROTOCOL/kiem.md` (khi soạn packet có khối `CÁCH CHỨNG MINH`, trước mọi thao tác ghi/đổi trạng thái, hoặc khi chạy `MAINTAIN`), `RUNS/INDEX.md`, `REGISTER/BAC.md` (bắt buộc trước mọi đề xuất phương án), `KB/INDEX.md` (khi tra cứu tri thức lĩnh vực theo LUẬT 12), `DECISION.md` của `RUN` đang mở.
- **`CHỈ ĐỌC KHI PACKET YÊU CẦU`:**
  `B.md` đầy đủ (hoặc hồ sơ chi tiết của các `RUN` đã đóng).
- **Quy tắc dừng đọc:** đọc theo tầng tới khi đủ bằng chứng trả lời đúng câu hỏi trong phạm vi của vai thì **DỪNG** (LUẬT 14); không đọc tràn các file ngoài phạm vi cách ly của vai (§2 `multi-brain-loop.md`).

## 9. Phân cấp thẩm quyền khi mâu thuẫn

Thứ tự ưu tiên từ cao xuống thấp:

```text
LAW/00-SUPREME-LAW.md > PROTOCOL/*.md > STATE.md > RUNS/* > KB/*
```

- `STATE.md` chỉ thắng `RUNS/` và `KB/` về câu hỏi **"đang ở đâu"** (khi đã qua kiểm `STATE_TRUST=OK`), tuyệt đối **KHÔNG thắng về "được làm gì"** (quyền hạn, cách ly vai, chuẩn nghiệm thu luôn thuộc `LAW/00` và `PROTOCOL/`).
- Gặp mâu thuẫn giữa hai nguồn bất kỳ => phát nhãn `CONFLICT=YES`, nêu đích danh hai file/dòng mâu thuẫn, **dừng phần việc liên quan**, không tự ý chọn một bên để làm tiếp.

## 10. Vai `R — Resumer`

`R — Resumer` là vai tiếp việc định kỳ hoặc khởi động lại sau khi đứt phiên:

1. Đọc `BỘ ĐỌC TỐI THIỂU` (+ `RUNS/INDEX.md`, `DECISION.md` đang mở, `REGISTER/BAC.md` khi cần).
2. Phát `LAW_CHECK` rồi `RESUME_CHECK` (kèm `STATE_TRUST=OK|DRIFT`).
3. Chỉ thực hiện đúng **`NEXT_ONE_ACTION`** đang ghi trong `STATE.md` hoặc đúng việc bounded mà packet cấp tường minh.
4. Nếu `NEXT_ONE_ACTION` mơ hồ, thiếu điều kiện đầu vào, hoặc đòi hỏi vai khác (ví dụ cần vai `B` độc lập kiểm chứng trong khi phiên hiện tại không được giao vai `B`) => báo rõ `UNKNOWN` / `BLOCKER`, **không tự ý bịa việc lớn để làm thay**.
5. `R` **không** tự mở vòng `A/B/C` mới, **không** phán xử thay `C`, **không** sửa `LAW/00-SUPREME-LAW.md`.
6. Dùng skill `scope-reality-check` ở chế độ `TRIGGER_MODE=USER_EXPLICIT` (xem `PROTOCOL/multi-brain-loop.md` §11).

## 11. NGHIỆM THU

> Sáu bài kiểm dưới đây là điều kiện để chuyển `MỐC` trong `STATE.md` từ `KHUNG` sang `ĐANG_VẬN_HÀNH`. Bắt buộc phải được thực hiện bởi một **PHIÊN MỚI thật** (LUẬT 03, LUẬT 04 — phiên viết giao thức không tự chấm nghiệm thu).

- **T1 Cold start:** phiên mới dán câu lệnh mục 12. Đạt khi phát `LAW_CHECK=PASS` (SHA thật), `RESUME_CHECK=PASS` đúng `OPEN` và `NEXT`, không hỏi lại.
- **T2 Đọc lịch sử:** nêu đúng RUN đang mở, verdict gần nhất của B, 2 quyết định gần nhất của Owner — CHỈ từ file.
- **T3 Chống trôi:** từ chối đoán; chỗ thiếu bằng chứng ghi `UNKNOWN`.
- **T4 Ghi lại:** làm 1 việc bounded rồi cập nhật `STATE.md` + `RUNS/INDEX.md` trong cùng commit.
- **T5 Skill đúng vai:** chạy skill ở chế độ `ROLE_BOUND`, không kiểm trigger; B dùng `SEALED`, không tra ngoài.
- **T6 Skill không phá luật:** gặp va chạm → luật thắng + `CONFLICT=YES`, không tự sửa luật.

## 12. CÂU LỆNH PHIÊN MỚI

```text
Đọc repo https://github.com/7roger89-web/GIAIDAP theo thứ tự trong AGENTS.md, phát RESTATE (nếu packet có trường này) rồi LAW_CHECK rồi RESUME_CHECK, đọc REGISTER/BAC.md, rồi đọc FILE skill tại đường dẫn scope-reality-check/SKILL.md NHƯ MỘT FILE (tự mở path scope-reality-check/SKILL.md ra mà đọc — đừng chờ auto-load, skill KHÔNG tự nạp), dùng skill đúng vai, rồi báo: việc đang mở, NEXT_ONE_ACTION, BLOCKER, UNKNOWN. Không đoán, không hỏi lại nếu repo đã trả lời được.
```

## 13. POST_MERGE_RECONCILE (phiên đầu tiên sau một merge)

**Quy tắc (bắt buộc):** Phiên ĐẦU TIÊN sau một merge phải: (1) đối chiếu `STATE.md` với thực tế `main`, (2) sửa `STATE.md` TRƯỚC khi làm việc khác, (3) ghi PR đã merge vào `LỊCH SỬ`.

Cách làm, theo đúng thứ tự:

1. `RESUME_CHECK` phát `POST_MERGE_RECONCILE=NEEDED` (§2) khi `STATE.md` còn giữ trạng thái PR/HEAD/hash của **trước** merge. Đối chiếu với `main` thật bằng `gh pr list` / `git log main` / `sha256sum`; chỗ nào lệch thì ghi rõ (`STATE_TRUST=DRIFT`, §3).
2. **Sửa `STATE.md` TRƯỚC**: cập nhật `PR_STATE` (PR vừa merge -> `MERGED` + ngày), `SINH_TỪ_HEAD` / `LAW_SHA256` / `PROTOCOL_HASHES` / `SKILL_HASH` nếu đổi, `VIỆC ĐANG MỞ`, `NEXT_ONE_ACTION`. Chưa làm việc bounded nào khác cho tới khi xong bước này; nếu sửa file khác sau khi ghi `STATE.md` thì áp §5 (tính lại mọi hash).
3. Ghi PR đã merge vào `LỊCH SỬ GẦN NHẤT`; đầy 8 dòng thì đẩy dòng cũ nhất xuống `REGISTER/LICH-SU.md` (§5). Rồi đổi `POST_MERGE_RECONCILE=DONE`.

Lý do tồn tại mục này: `STATE.md` nằm trên NHÁNH của từng phiên; trước khi merge, `main` chứa trạng thái CŨ. Nếu phiên đầu sau merge đọc `STATE.md` cũ rồi làm việc luôn, nó sẽ định vị sai (tự mục). Phiên đầu phải là phiên **SỬA `STATE.md`**, không phải phiên làm việc mới. Mục này KHÔNG phải cơ chế `claim/lock` (vẫn còn là `UNKNOWN` ở `STATE.md`).

## 14. Nhịp `MAINTAIN` (trỏ về `PROTOCOL/kiem.md` §5)

Khi cấu trúc repo đổi (thêm/xóa file, đổi luật, đổi `PROTOCOL/`) hoặc mỗi 10 phiên (đếm theo `SESSION_REF` trong `STATE.md`), bắt buộc chạy `MAINTAIN` theo đúng 3 bước tại `PROTOCOL/kiem.md` §5:

1. rà hash (`sha256sum` đối chiếu khối `HASH CHUẨN` trong `STATE.md`);
2. rà mọi con trỏ (`test -f <path>`), không để đường dẫn treo im lặng;
3. rà mọi `LỆNH` trong `PROTOCOL/kiem.md` và packet đã lưu còn chạy được nguyên văn; lệnh hỏng => báo `MUI=c`.

Bản ghi `MAINTAIN` đi trong cùng commit với lần cập nhật `STATE.md` (§5). Đây là bảo trì giao thức, không phải vòng A/B/C và không mở `RUN` mới.
