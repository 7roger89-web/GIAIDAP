# KB/INDEX.md — Mục lục tri thức

TRẠNG THÁI: ACTIVE | NGÀY: 2026-10-26

Bảng tra theo từ khóa. Khớp thì dùng, không khớp thì tạo RUN mới rồi thêm dòng vào đây.

| TỪ KHÓA | FILE | STATUS | NGÀY | NGUỒN | ĐỘ TIN CẬY |
|---|---|---|---|---|---|
| nhập khẩu, bình nóng lạnh, trung quốc | (chưa có) | TODO | - | - | - |

## Quy ước

- **TỪ KHÓA**: tiếng Việt, có dấu hoặc không dấu, cách nhau bằng dấu phẩy; thêm tiếng Anh nếu cần. Không phân biệt hoa/thường; bỏ dấu khi so khớp.
- **FILE**: đường dẫn tương đối tới file KB thật. Nếu chưa có, ghi `(chưa có)`.
- **STATUS**: `ACTIVE` | `SUPERSEDED` | `DEPRECATED` | `QUARANTINED` | `TODO`.
  - `TODO`: mục chưa có nội dung, chỉ là dòng chờ.
- **NGÀY**: ngày kiểm nguồn gần nhất, `YYYY-MM-DD`. Dữ kiện dễ cũ (giá, luật, model, API) phải ghi ngày kiểm và hạn.
- **NGUỒN**: URL hoặc đường dẫn file. Không ghi "internet" hoặc "tìm trên mạng".
- **ĐỘ TIN CẬY**: `CAO` | `TRUNG BÌNH` | `THẤP` | `UNKNOWN`.

## Cách dùng

1. Chuẩn hóa từ khóa: chữ thường, bỏ dấu.
2. So khớp với cột `TỪ KHÓA`; chỉ cần một từ khóa khớp.
3. Khớp và `ACTIVE` => dùng làm điểm xuất phát; vẫn kiểm nguồn nếu là dữ kiện dễ cũ.
4. Không khớp => mở `RUNS/<4 số>-<slug>/`, tự tìm, ghi kết quả, rồi thêm dòng vào bảng này.
5. Có mục mới thay mục cũ => đổi mục cũ thành `SUPERSEDED`, không xóa.
6. Không đưa kết luận chưa kiểm vào KB; ghi nhãn `FACT` / `INFERENCE` / `UNKNOWN` trong file KB.

## Ghi chú

- Dòng ví dụ `nhập khẩu, bình nóng lạnh, trung quốc` là **TODO**, chưa phải tri thức đã kiểm.
- Khi thêm dòng thật, giữ đúng 6 cột và ghi nguồn cụ thể.
