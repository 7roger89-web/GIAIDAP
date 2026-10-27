# PROTOCOL/resume-protocol.md — Giao thức hồi sinh phiên mới (Cold-Start & Write-Back)

TRẠNG THÁI: ACTIVE | NGÀY: 2026-10-27

MỤC ĐÍCH: giúp một model mới, ở phiên mới, không có ký ức chat, chỉ đọc file trong repo là biết chính xác đang ở đâu, biết việc kế tiếp, chứng minh được đã đọc đúng bản, làm tiếp một đơn vị việc bounded và ghi lại cho phiên sau.

## 1. Thứ tự đọc cold-start

Phiên mới vào repo đọc theo thứ tự:

1. `AGENTS.md`
2. `STATE.md`
3. `LAW/00-SUPREME-LAW.md`
4. `PROTOCOL/resume-protocol.md` (file này) và `PROTOCOL/multi-brain-loop.md`
5. `PROTOCOL/cach-nghi.md`
6. `RUNS/INDEX.md`
7. `KB/INDEX.md`

Quy tắc định vị:

- **`STATE.md` đọc TRƯỚC `LAW/00-SUPREME-LAW.md`** để biết ngay repo đang ở đâu, việc gì đang mở và hash kỳ vọng là gì.
- **Nhưng `STATE.md` không thay thế việc đọc luật:** biên lai `LAW_CHECK` vẫn bắt buộc phải phát riêng từ nội dung thật của `LAW/00-SUPREME-LAW.md` (`sha256sum` thật) trước khi làm bất kỳ việc thật nào.
- Trước khi đề xuất phương án mới, bắt buộc đọc thêm `REGISTER/BAC.md` để không mở lại phương án đã bị bác.
- Xem §8 về phân tầng bộ đọc khi vai chỉ làm việc hẹp.

## 2. Biên lai hồi sinh (`RESUME_CHECK`)

Ngay sau dòng `LAW_CHECK`, mọi phiên tiếp việc phải phát biên lai `RESUME_CHECK`.

- Nếu packet của việc có trường `RESTATE` (mọi packet theo `PROTOCOL/handoff-packet.md` bản 10 trường đều có), phát `RESTATE` **trước cả `LAW_CHECK`**; thứ tự output là `RESTATE` → `LAW_CHECK` → `RESUME_CHECK`. Diễn giải lệch packet => `RESTATE_MISMATCH=YES`, dừng việc thật (chi tiết tại `PROTOCOL/cach-nghi.md` §1).

Hai khối dưới đây là **TEMPLATE**, không phải biên lai thật:

```text
RESUME_CHECK=PASS | STATE_HEAD=<sha> | READ_HEAD=<sha> | LAW_HASH_MATCH=<YES|NO> | PROTOCOL_HASH_MATCH=<YES|NO> | SKILL_HASH_MATCH=<YES|NO> | OPEN=<...> | NEXT=<...>
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
Đọc repo https://github.com/7roger89-web/GIAIDAP theo thứ tự trong AGENTS.md, phát RESTATE (nếu packet có trường này) rồi LAW_CHECK rồi RESUME_CHECK, đọc REGISTER/BAC.md, dùng skill scope-reality-check đúng vai, rồi báo: việc đang mở, NEXT_ONE_ACTION, BLOCKER, UNKNOWN. Không đoán, không hỏi lại nếu repo đã trả lời được.
```

## 13. Nhịp `MAINTAIN` (trỏ về `PROTOCOL/kiem.md` §5)

Khi cấu trúc repo đổi (thêm/xóa file, đổi luật, đổi `PROTOCOL/`) hoặc mỗi 10 phiên (đếm theo `SESSION_REF` trong `STATE.md`), bắt buộc chạy `MAINTAIN` theo đúng 3 bước tại `PROTOCOL/kiem.md` §5:

1. rà hash (`sha256sum` đối chiếu khối `HASH CHUẨN` trong `STATE.md`);
2. rà mọi con trỏ (`test -f <path>`), không để đường dẫn treo im lặng;
3. rà mọi `LỆNH` trong `PROTOCOL/kiem.md` và packet đã lưu còn chạy được nguyên văn; lệnh hỏng => báo `MUI=c`.

Bản ghi `MAINTAIN` đi trong cùng commit với lần cập nhật `STATE.md` (§5). Đây là bảo trì giao thức, không phải vòng A/B/C và không mở `RUN` mới.
