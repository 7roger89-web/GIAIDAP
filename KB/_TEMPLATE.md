# KB/_TEMPLATE.md — Khuôn mẫu một mục tri thức KB

> **ĐÂY LÀ TEMPLATE, KHÔNG PHẢI MỤC TRI THỨC THẬT.** Không coi nội dung ngoặc nhọn `<...>` dưới đây là dữ kiện `ACTIVE`.
> Chỉ tạo file KB mới sau khi đã có `RUNS/<4 số>-<slug>/` và trả lời được mục **"Sẽ được tra lại khi nào"** bên dưới (LUẬT 12). Nếu không nêu được tình huống tái dùng cụ thể => giữ kết quả trong `RUNS/`, không tạo file KB.

## 1. Bản ghi 6 cột khớp `KB/INDEX.md`

Khi tạo mục KB mới, điền đủ bảng 6 cột dưới đây và chép cùng một dòng vào `KB/INDEX.md`:

| TỪ KHÓA | FILE | STATUS | NGÀY | NGUỒN | ĐỘ TIN CẬY |
|---|---|---|---|---|---|
| `<từ khóa 1, từ khóa 2, khong dau neu can>` | `KB/<slug>.md` | `ACTIVE` | `<YYYY-MM-DD>` | `<URL hoặc đường dẫn nguồn chính>` | `CAO \| TRUNG BÌNH \| THẤP \| UNKNOWN` |

Metadata vòng đời bổ sung (theo LUẬT 11 & LUẬT 12):

- `ORIGIN_RUN_ID`: `<4 số>-<slug>` (mã RUN đã kiểm chứng mục này)
- `LOẠI_DỮ_KIỆN`: `BỀN` | `DỄ_CŨ` (giá, luật, chính sách, model, API, hạn mức...)
- `NGÀY_KIỂM_NGUỒN`: `<YYYY-MM-DD>`
- `HẠN_KIỂM_LẠI`: `<YYYY-MM-DD hoặc KHÔNG_ÁP_DỤNG nếu là dữ kiện bền>`
- `THAY_THẾ_MỤC_CŨ`: `NONE` | `KB/<file-cũ>.md` (nếu thay thế mục cũ thì đổi mục cũ sang `SUPERSEDED`, không xóa)
- `SESSION_REF`: `<nhánh/phiên ghi file>`
- `PR_HEAD_SHA`: `<sha commit gốc khi ghi>`

## 2. Sẽ được tra lại khi nào (bắt buộc theo LUẬT 12)

- `<Nêu ít nhất 1 tình huống công việc tương lai cụ thể mà model/Owner sẽ tra lại mục này theo từ khóa. Không viết chung chung kiểu "khi cần tham khảo".>`

## 3. Nội dung tri thức (tách nhãn nhận thức theo LUẬT 09)

### FACT (có nguồn kiểm được)

- `FACT`: `<Dữ kiện đã xác minh trực tiếp>` — Nguồn: `<URL/file + dòng/mục>`, kiểm ngày `<YYYY-MM-DD>`.

### INFERENCE (suy ra từ FACT)

- `INFERENCE`: `<Kết luận suy diễn hợp lý>` — suy ra từ `<FACT nào ở trên>`. *(Không nâng thành FACT).*

### UNKNOWN (chưa xác minh được)

- `UNKNOWN`: `<Điểm chưa có bằng chứng hoặc phụ thuộc thay đổi bên ngoài; nếu không có thì ghi UNKNOWN=NONE>`.

*(Nếu có giả thuyết chưa kiểm hoặc điểm chờ duyệt, tách riêng thêm mục `### HYPOTHESIS` hoặc `### OWNER_CONFIRMATION_REQUIRED` — không trộn chung).*

## 4. Nguồn chi tiết

1. `<Nguồn 1: URL hoặc đường dẫn file — ngày công bố/cập nhật — ngày kiểm YYYY-MM-DD>`
