# PROTOCOL/kiem.md — Lớp chứng minh: khai cách kiểm TRƯỚC khi làm

TRẠNG THÁI: ACTIVE | NGÀY: 2026-10-27
SESSION_REF: arena/05b33e63-giaidap
PR_HEAD_SHA: 7563b9c1826c13998f0b74a13f931c7460724408

MỤC ĐÍCH: GIAIDAP đã có biên lai chứng minh việc **ĐỌC** (`LAW_CHECK`, `RESUME_CHECK`). File này bịt nốt lỗ còn lại: repo chưa có chỗ bắt khai **CÁCH CHỨNG MINH VIỆC LÀM**. File này là GIAO THỨC — bậc dưới `LAW/00` theo `PROTOCOL/resume-protocol.md` §9; nó **nối LUẬT 03 thành quy trình, không thay LUẬT 03**, và không tạo bản luật song song (LUẬT 13).

## 1. Khối `CÁCH CHỨNG MINH` (bắt buộc trong mọi packet, điền TRƯỚC khi làm)

Mọi `PACKET->A/B/C` và mọi việc bounded giao tay chân phải mang khối 4 dòng:

```text
CÁCH CHỨNG MINH:
- LỆNH: <một dòng shell THẬT, chạy được nguyên văn trong repo>
- KỲ VỌNG: <kết quả máy đọc được: exit code, số dòng, chuỗi in ra, hash...>
- ARTIFACT: <file/log để lại sau khi chạy; đường dẫn thật trong repo hoặc log của phiên>
- NẾU KHÔNG CHẠY ĐƯỢC: <lý do môi trường/quyền + bằng chứng thay thế khả kiểm>
```

Quy tắc:

- **LỆNH phải thật:** cấm lệnh giả, cấm ghi "sẽ kiểm sau". Một dòng shell, không phải kịch bản nhiều bước; không dựng script/CI để thay (LUẬT 05).
- **KỲ VỌNG phải khả bác:** nêu đúng chuỗi/số/exit code để người kiểm chạy lại là biết ngay đúng sai; không chấp nhận kỳ vọng mơ hồ kiểu "ra kết quả đúng".
- **NẾU KHÔNG CHẠY ĐƯỢC không phải cửa thoát:** phải nêu bằng chứng thay thế cụ thể (log nguyên văn, ảnh, đường dẫn), không để trống.

Ví dụ cho việc xuất một file `A.md`:

```text
CÁCH CHỨNG MINH:
- LỆNH: test -s RUNS/0001-nhap-khau-binh-nong-lanh/A.md && grep -c '^## ' RUNS/0001-nhap-khau-binh-nong-lanh/A.md
- KỲ VỌNG: in ra 5 (đủ 5 mục nội dung), exit 0
- ARTIFACT: RUNS/0001-nhap-khau-binh-nong-lanh/A.md
- NẾU KHÔNG CHẠY ĐƯỢC: chép nguyên văn lỗi shell + liệt kê các tiêu đề mục thực có trong file
```

## 2. Test xanh CHƯA đủ — phải chạy thật

LUẬT 03 quy định bằng chứng cục bộ/static/mock không được nâng thành PASS sống. Lớp này bổ sung quy trình, không bổ sung luật:

- Test xanh, file tồn tại, preview xem được là **chưa đủ** nếu nghiệm thu cần runtime thật / nội dung thật / quy trình thật.
- Khối `CÁCH CHỨNG MINH` phải được **chạy thật trong phiên làm việc**; chỉ sau khi chạy mới được điền `CÁCH CHỨNG MINH_ĐÃ CHẠY=YES` vào `RETURN_PACKET->OWNER` (xem `PROTOCOL/handoff-packet.md` §4).
- Tự khai "đã kiểm" mà không có lệnh + kết quả chạy thật là tự nhận công (LUẬT 04), vô giá trị nghiệm thu.

## 3. DRY_RUN — lệnh kiểm trước khi ghi

Việc có ghi file, đổi trạng thái, push hoặc mở PR thì **TRƯỚC khi ghi** phải nêu được:

1. Lệnh kiểm trạng thái TRƯỚC khi ghi (ví dụ `sha256sum <file>`, `git status --short`, `grep '<chuỗi>' <file>`).
2. Lệnh kiểm LẠI sau khi ghi (ví dụ so lại hash, `git diff --stat`, đếm số dòng).

Không nêu được lệnh kiểm trước => việc chưa định hình đủ để bắt đầu: dừng, làm rõ packet, không ghi mò.

## 4. Danh sách MÙI — gặp là báo, KHÔNG tự sửa

| Mã | Mùi | Chẩn đoán |
|---|---|---|
| `a` | Cùng một quy tắc phải nhắc lại ở ≥3 file | Thiếu một nguồn duy nhất cho quy tắc |
| `b` | Cùng một trường/hash lặp ở nhiều file | Thiếu một khuôn (template) chung |
| `c` | Một quy tắc không kiểm được bằng lệnh | Quy tắc mơ hồ, vi phạm tinh thần §1 |
| `d` | Phải chép lại cùng một câu vào mọi packet | Thiếu một file chứa sẵn câu đó |

Gặp mùi: ghi `MUI=<a|b|c|d>` (nhiều mùi nối bằng dấu phẩy, ví dụ `MUI=a,c`) vào output và `RETURN_PACKET`, nêu rõ file/dòng, báo Owner. **KHÔNG tự sửa ngoài phạm vi packet**; việc sửa mùi là một đơn vị bounded mới do Owner cấp.

## 5. Nhịp `MAINTAIN` (bắt buộc)

Chạy `MAINTAIN` khi: (1) cấu trúc repo đổi — thêm/xóa file, đổi luật, đổi `PROTOCOL/`; (2) mỗi 10 phiên (đếm theo `SESSION_REF` trong `STATE.md`). Ba bước:

1. **Rà hash:** chạy `sha256sum LAW/00-SUPREME-LAW.md PROTOCOL/*.md scope-reality-check/SKILL.md`, đối chiếu khối `HASH CHUẨN` trong `STATE.md`. Lệch => đọc lại đúng file bị lệch theo `PROTOCOL/resume-protocol.md` §2, không tự sửa hash ngầm.
2. **Rà con trỏ:** mọi đường dẫn được trỏ trong `AGENTS.md`, `STATE.md §CON TRỎ` và các file `PROTOCOL/*.md` phải tồn tại (`test -f <path>`). File bị trỏ nhưng chưa merge vào nhánh hiện tại phải được ghi rõ trạng thái — không để con trỏ treo im lặng.
3. **Rà LỆNH:** mọi `LỆNH` trong file này và trong packet đã lưu phải còn chạy được nguyên văn. Lệnh hỏng => báo `MUI=c`.

Bản ghi `MAINTAIN` đi trong cùng commit với lần cập nhật `STATE.md` (`PROTOCOL/resume-protocol.md` §5).

## 6. BẢN ĐỒ workstream

Mỗi WORKSTREAM phải có **BẢN ĐỒ** nêu đủ ba thứ: workstream có gì (file/folder) · vào ở đâu (đường dẫn vào) · kiểm bằng gì (LỆNH thật). Bản đồ đặt **kèm workstream** (trong `RUNS/<id>/` hoặc folder riêng của workstream), không tách rời dữ liệu nó mô tả.

**KHÔNG tạo file `BAN-DO.md` ở gốc repo.** Lý do, ghi rõ để phiên sau không mở lại:

1. Packet ngày 2026-10-27 cấm tường minh tạo file này (giới hạn của đơn vị bounded).
2. Một bản đồ gốc tập trung sẽ trùng con trỏ với `STATE.md §CON TRỎ` và `RUNS/INDEX.md` — đúng mùi `a` và `b` ở §4: mỗi lần cấu trúc đổi phải sửa hai nơi.
3. LUẬT 05 chọn đường đơn giản nhất: toàn repo hiện đã được định vị qua `STATE.md` + `RUNS/INDEX.md`; chưa có workstream thứ hai ngoài `RUNS/` cần bản đồ riêng. Khi có, tạo bản đồ **kèm workstream đó**, không nâng thành hạ tầng ở gốc.
