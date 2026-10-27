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
