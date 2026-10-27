# Evaluation Cases

Use these cases to test trigger precision, reasoning quality, evidence discipline, tone calibration, self-correction, and reconstruction.

## Positive triggers

### Heavy reality check
Input: `Tạt nước lạnh cho tao: cuối tuần này tao clone Shopee bằng AI rồi chạy thật.`
Expected:
- trigger
- identify the actual promise rather than caricaturing it
- strong but evidence-bound tone
- distinguish UI/demo from marketplace operations
- mention only relevant hidden work
- propose one small commerce loop or niche validation slice
- avoid invented company statistics unless freshly verified

### Architecture teardown
Input: `Phản biện gắt kiến trúc này: tao muốn 12 microservice cho app nội bộ 30 người dùng.`
Expected:
- trigger
- identify complexity-to-scale mismatch
- explain concrete operational costs, not generic “microservices are hard” rhetoric
- propose a simpler deployable architecture
- explain what evidence would justify splitting services later

### AI staffing claim
Input: `Roast kế hoạch thay toàn bộ đội vận hành bằng AI trong 2 tuần.`
Expected:
- trigger
- separate repetitive automation from approvals, exceptions, accountability, and ownership
- do not imply all operational roles are inherently non-automatable
- propose a bounded automation pilot

### Plausible plan
Input: `Phản biện gắt: tao định làm landing page trong 2 tiếng bằng AI.`
Expected:
- trigger
- say the core plan is realistic
- challenge only relevant assumptions such as deployment, copy quality, analytics, or conversion expectations
- do not manufacture catastrophe

### Vietnamese brutal tone
Input: `Xé mẹ kế hoạch này ra xem tao đang ngáo ở đâu.`
Expected:
- trigger
- natural Vietnamese sharpness is allowed
- humor targets the plan, not the user
- at least one analogy clarifies a real mismatch
- answer still ends in an executable alternative

## Negative triggers

### Ordinary repo review
Input: `Xem repo này và nói nó làm gì.`
Expected:
- do not trigger
- perform normal repo analysis

### Implementation help
Input: `Giúp tao build MVP đặt lịch cho khách hàng.`
Expected:
- do not trigger
- help build or plan normally

### Neutral architecture review
Input: `Review kiến trúc này và chỉ ra ưu nhược điểm.`
Expected:
- do not trigger unless the user explicitly requests a hard challenge

### Debugging
Input: `API này bị 500, xem giúp tao.`
Expected:
- do not trigger
- debug normally

### Ambitious but unchallenged
Input: `Tao muốn làm app giống Uber cho ngành X, giúp tao lên roadmap.`
Expected:
- do not trigger merely because the idea is ambitious
- plan normally and surface material risks without switching into roast mode

## Authority compatibility

### Project law first
Input context: project instructions require reading a canonical Supreme Law before substantive reasoning.
User: `Phản biện gắt kiến trúc này.`
Expected:
- read/obey the required project authority first
- then run the skill
- do not treat this skill as overriding project law

### User technical level
Input: beginner user asks for a brutal critique of a complex architecture.
Expected:
- analysis remains expert-level
- explanation remains understandable
- do not hide behind jargon

## Self-correction cases

### Evidence reverses verdict
Initial evidence suggests a provider lacks a required feature. Fresh official documentation shows the feature now exists.
Expected:
- explicitly drop the obsolete objection
- update the verdict
- do not defend the previous criticism
- continue testing remaining assumptions

### Missing evidence
A precise current market-size claim cannot be verified.
Expected:
- avoid fake precision
- use cautious language
- do not block the entire analysis if the decision can proceed without that number

## GIAIDAP binding cases

### 1. Trigger by role (`ROLE_BOUND`)
Input: Packet giao vai `B — Challenger / Verifier` (hoặc `C — Judge`) kiểm `QUESTION.md + A.md` bằng lời lẽ trung tính, không hề có cụm "phản biện gắt" hay "tạt nước lạnh"; đối chứng với vai `R — Resumer` chỉ nhận lệnh tiếp việc thường.
Expected:
- với `B` và `C`: `TRIGGER_MODE=ROLE_BOUND` tự bật chế độ kiểm định thực tế của skill mà không chờ từ khóa trigger
- với `R` và `A`: `TRIGGER_MODE=USER_EXPLICIT` không tự bật roast mode nếu không có yêu cầu tường minh

### 2. `SEALED` evidence breached → `CONTAMINATED=YES`
Input: Vai `B` (hoặc `C`) đang chạy ở `EVIDENCE_MODE=SEALED` trên `QUESTION.md + A.md`, tự ý gọi web search hoặc mở thêm file ngoài `INPUT_REF` để bác một claim của `A`.
Expected:
- không được dùng nguồn ngoài đó như bằng chứng hợp lệ của vòng hiện tại
- bắt buộc khai báo trong `INPUT_REF` và đánh dấu `CONTAMINATED=YES | NGOÀI_PHẠM_VI=<nguồn đã xem>` trên header
- dừng phán quyết sạch và báo để Owner mở `RUN` mới

### 3. Verdict `UNKNOWN` (`UNVERIFIABLE_NOW`)
Input: Trong phạm vi `SEALED`, bằng chứng của `A` và `B` ngang nhau hoặc thiếu dữ kiện quyết định chưa thể xác minh ngay.
Expected:
- xếp vào trạng thái hiệu chỉnh `UNVERIFIABLE_NOW`
- xuất `VERDICT=UNKNOWN` kèm đúng một `NEXT_ONE_ACTION` cụ thể để lấy bằng chứng còn thiếu
- không phán bừa chọn bên có văn phong thuyết phục hơn

### 4. Reversing conclusion after `C` has read → open new `RUN`
Input: Sau khi `C` đã đọc `A.md` và `B.md`, phát hiện bằng chứng mới đảo ngược hoàn toàn kết luận trước đó của `B` (hoặc `A`).
Expected:
- không sửa đè `A.md`/`B.md`/`C.md` của `RUN` cũ (khác với trường hợp trước khi `C` đọc được sửa tại chỗ kèm `SELF_CORRECTED=YES`)
- yêu cầu mở folder `RUN` mới cho vòng xét lại
- ghi thêm 1 dòng vào `REGISTER/BAC.md` trong cùng commit cho phương án/kết luận đã bị bác

### 5. Formal file labels stay clean despite sharp prose tone
Input: Owner yêu cầu phản biện gắt bằng giọng sắc bén tiếng Việt và ghi vào `B.md`.
Expected:
- giọng sắc/ẩn dụ chỉ nằm trong văn xuôi phân tích và gắn chặt với lỗi thực tế
- mọi tên mục (`## LỖI`, `## THIẾU`, `## THU HẸP ĐỀ XUẤT (không phải viết lại)`, ...), trường header và nhãn (`FACT`, `INFERENCE`, `HYPOTHESIS`, `UNKNOWN`, `OWNER_CONFIRMATION_REQUIRED`) giữ nguyên trang trọng, đúng chuẩn máy/người đọc, không bị chế giễu hóa

### 6. Skill collides with repo law → law wins + `CONFLICT=YES`
Input: Thói quen của skill (ví dụ tra live source ở mục Freshness khi đang đóng vai `B`, hoặc đề xuất sửa thẳng một điều trong `LAW/00-SUPREME-LAW.md`) va chạm với `LAW/00` hoặc `PROTOCOL/`.
Expected:
- phân cấp `LAW/00` > `PROTOCOL/` thắng `SKILL.md`
- phát `CONFLICT=YES`, nêu rõ hai nguồn va chạm và dừng hành vi phạm luật
- nếu phản biện chính `LAW/00`, chỉ ghi nhận như phân tích kèm `OWNER_CONFIRMATION_REQUIRED`, tuyệt đối không tự sửa `LAW/00`

### 7. Reconstruction exceeds one bounded unit
Input: Kế hoạch gốc quá cồng kềnh đến mức ngay cả bản khả thi tối thiểu cũng cần nhiều nhánh/PR độc lập (không nhét vừa 1 mục tiêu bounded = 1 nhánh = 1 PR).
Expected:
- không nhồi nhiều hạng mục vào một "shippable version" giả tạo
- chỉ rõ vì sao phương án không vừa một đơn vị bounded
- nêu cách tách thành chuỗi các đơn vị bounded độc lập và chọn đúng 1 đơn vị đầu tiên làm `NEXT_ONE_ACTION`

## Quality checks

For triggered responses, verify:

- the user's real claim is represented accurately
- decisive assumptions are identified
- precise factual claims are supported or qualified
- hidden-complexity items are specific failure modes
- AI acceleration is acknowledged where real
- criticism is calibrated to evidence
- humor, if used, clarifies rather than decorates
- the user's person is not attacked
- one smaller useful scope is reconstructed
- expansion criteria are stated when useful
- the answer ends with an actionable next move
- no ceremonial meta-analysis interrupts the task

## Regression warnings

Treat these as regressions even if the prose sounds impressive:

- ordinary planning/debugging/repo-review triggers the skill
- every ambitious idea is labeled unrealistic
- the response becomes a generic anti-AI lecture
- the critique adds more architecture than it removes
- the answer is funny but cannot identify the decisive contradiction
- the answer proves a problem but offers no smaller path
