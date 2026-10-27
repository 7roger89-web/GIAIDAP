# STATE.md — Điểm hồi sinh GIAIDAP

TRẠNG THÁI: ACTIVE | CẬP NHẬT: 2026-10-27T06:04
SESSION_REF: arena/05b33e63-giaidap
SINH_TỪ_HEAD: d9074354bc735241c5faf03bc06efd24b72117f1
PROVENANCE_STATUS: PENDING_VERIFICATION
MỐC: KHUNG (hợp lệ: KHUNG | ĐANG_VẬN_HÀNH; ĐANG_VẬN_HÀNH chỉ đạt khi T1–T6 tại PROTOCOL/resume-protocol.md §11 đạt bởi một PHIÊN MỚI thật, kèm ngày + bằng chứng PR/commit)
QUY TẮC BẢO TRÌ: Mọi thay đổi trạng thái phải cập nhật STATE.md TRONG CÙNG COMMIT.
Cổng kết phiên là kỷ luật TỰ NGUYỆN — không có CI cưỡng chế.

## HASH CHUẨN
LAW_SHA256: 2cf47ae59380740b500402eb386ae3b63b06d28a4d1b90b1e58a9524784eee52
PROTOCOL_HASHES:
- PROTOCOL/arena-agent-mode.md:6e622bbab282b174a1ba360ffba6072b38c0a378add64eda1235042e5049cca2
- PROTOCOL/cach-nghi.md:e974cd42746b3c4dd76ee0765ed96db9b592189a6e0430482b1514d6c1555e30
- PROTOCOL/handoff-packet.md:0c92fd5582d45d00ba41cd96bd964d2ebf51d306f16939a85299485642342ac1
- PROTOCOL/kiem.md:d907a56d40414183a46df8d342fec24d5b267e9a7c28176824fd860e0cbb2037
- PROTOCOL/multi-brain-loop.md:523d15cebb081c099bbfc65ec313591588589a015f63b987b8f6576cc8f6169f
- PROTOCOL/resume-protocol.md:efcfb6ffca4c34d093392c776c81ebf7eb02e452b9563eccf7805b54b4c989f9
SKILL_HASH: 941ca990c137a33f1f18fbee43411e2b35a3635944c531905f974cd276221268

## VIỆC ĐANG MỞ
- 0000-pr1-verify — OPEN (verdict gần nhất của B cho head 84ae8b3: PASS_WITH_FIXES; bản V4 chưa kiểm lại) — Giao vai B ở phiên mới kiểm lại diff 84ae8b3..HEAD (LUẬT 12, LUẬT 08, map V4, KB/INDEX.md §MỞ RỘNG, cặp hash B.md)

## NEXT_ONE_ACTION
Giao vai B (ở một phiên mới độc lập, EVIDENCE_MODE=SEALED theo packet kiểm luật) kiểm lại phần thay đổi của vá lần 5–7 từ commit 84ae8b3dfd8271d11af40c49fb34715634af1d0f tới HEAD (LUẬT 12, LUẬT 08, LAW/00-PROVENANCE-MAP.md bản V4, KB/INDEX.md §MỞ RỘNG, cặp field hash trong RUNS/0000-pr1-verify/B.md) trước khi xét gỡ PENDING_VERIFICATION.

## BLOCKER & UNKNOWN
- BLOCKER (tuần tự PR): PR lớp chứng minh này (nhánh arena/05b33e63-giaidap) được soạn khi PR #4 và PR #5 vẫn OPEN (kiểm `gh pr list` ngày 2026-10-27), trong khi packet yêu cầu "chỉ chạy SAU KHI #4 và #5 đã merge". Nhánh hiện tại sinh từ 7563b9c = head PR #4 (chưa có nội dung PR #5). PR này KHÔNG được merge trước #4/#5; sau khi #4/#5 merge, phiên sau phải rebase + reconcile — các file hai bên cùng đụng: AGENTS.md, PROTOCOL/handoff-packet.md, PROTOCOL/resume-protocol.md, README.md, STATE.md. Va chạm đã biết: mục §13 trong resume-protocol (bản này là MAINTAIN; PR #5 cũng đặt §13 là POST_MERGE_RECONCILE) phải đánh số lại.
- BLOCKER: Chưa được gỡ PROVENANCE_STATUS=PENDING_VERIFICATION vì vai B chưa kiểm độc lập bản map V4 sau vá lần 5–7 (kiểm ngày 2026-10-27).
- UNKNOWN: `REGISTER/LICH-SU.md` chưa tồn tại trên nhánh này (chỉ được tạo trong PR #5 chưa merge). `PROTOCOL/cach-nghi.md` vẫn trỏ đúng đường dẫn chính danh theo packet nhưng kèm ghi chú thay thế tạm (`STATE.md §LỊCH SỬ GẦN NHẤT` + `git log`); con trỏ thành hợp lệ sau khi PR #5 merge.
- UNKNOWN: Cơ chế claim/lock chưa làm (để PR sau) vì lỗi thiết kế: STATE.md nằm trên nhánh riêng của từng phiên trước khi merge nên hai phiên chạy song song không thấy nhau (kiểm ngày 2026-10-27).
- UNKNOWN: CONTENT_SHA256_B_DECLARED=UNKNOWN trong RUNS/0000-pr1-verify/B.md do B không tự khai (kiểm ngày 2026-10-26).
- UNKNOWN: Chưa có bằng chứng phiên mới độc lập chạy nghiệm thu T1–T6 để nâng MỐC từ KHUNG lên ĐANG_VẬN_HÀNH (kiểm ngày 2026-10-27).
- UNKNOWN: PR #2 và PR #3 đang OPEN trên GitHub (ngoài nhánh main); quyết định xử lý của Owner chưa ghi trong main (kiểm ngày 2026-10-27). PR #4, #5 cùng trạng thái OPEN tại cùng thời điểm kiểm.

## OWNER_QUYẾT
- D5 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: tách hash B.md thành 2 field riêng, không gộp) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap
- D4 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: cho phép sửa riêng LUẬT 08, các LUẬT khác không đổi) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap
- D3 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: B.md ghi nguyên văn, CONTENT_SHA256 lấy theo B tự khai, không khai => UNKNOWN) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap
- D2 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: giữ bảng 15 dòng NEW=1/DERIVED=14, không bỏ LUẬT 15) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap
- D1 | OWNER_SAID=PARAPHRASE (không có comment nguyên văn trên PR #1; tóm tắt: cho phép sửa riêng LUẬT 12) | NGUỒN: RUNS/0000-pr1-verify/DECISION.md §1, https://github.com/7roger89-web/GIAIDAP/pull/1 (2026-10-26) | NGƯỜI CHÉP: arena/609eab3c-giaidap

## LỊCH SỬ GẦN NHẤT
- 2026-10-27 — Lắp lớp chứng minh verification-first: thêm PROTOCOL/kiem.md (khối CÁCH CHỨNG MINH 4 dòng, DRY_RUN, MÙI a–d, nhịp MAINTAIN, bản đồ workstream) + PROTOCOL/cach-nghi.md (8 bước nghĩ trước khi làm); packet A/B/C lên 10 trường, RETURN_PACKET thêm 3 trường chứng minh; cold-start thêm cach-nghi — nhánh arena/05b33e63-giaidap, sinh từ 7563b9c (head PR #4); chờ PR #4/#5 merge rồi mới merge
- 2026-10-27 — Khởi tạo cơ chế hồi sinh + bind skill scope-reality-check + vá khuôn RUN 0000 — nhánh arena/b960bf99-giaidap (sinh từ d907435)
- 2026-10-27 — Đưa thư mục skill scope-reality-check lên main — commit d907435
- 2026-10-26 — Merge khung luật và giao thức V1 vào main — commit 0a892a4 (PR #1: https://github.com/7roger89-web/GIAIDAP/pull/1)
- 2026-10-26 — Vá lần 7: khôi phục LUẬT 08 theo D4, tách 2 trường hash B.md theo D5, nâng map lên V4 — commit 9c4b63a (PR #1)
- 2026-10-26 — Vá lần 6: lưu nguyên văn B.md, sửa LUẬT 12 theo D1, nâng map lên V3 — commit b1ba697 (PR #1)
- 2026-10-26 — Vá lần 5: áp sửa theo báo cáo B (thêm LUẬT 15, bắt buộc SHA thật cho LAW_CHECK, map V2) — commit db14795 (PR #1)
- 2026-10-26 — Vai B kiểm độc lập PR #1 tại head 84ae8b3, ra verdict PASS_WITH_FIXES — RUNS/0000-pr1-verify/B.md (commit 84ae8b3)
- 2026-10-26 — Khởi tạo khung luật và giao thức GIAIDAP V1 — commit 612a8e6 (PR #1)

## CON TRỎ
- Luật & ánh xạ nguồn: LAW/00-SUPREME-LAW.md | LAW/00-PROVENANCE-MAP.md
- Giao thức & skill: PROTOCOL/resume-protocol.md | PROTOCOL/multi-brain-loop.md | PROTOCOL/kiem.md | PROTOCOL/cach-nghi.md | scope-reality-check/SKILL.md
- Sổ & mục lục: REGISTER/BAC.md | RUNS/INDEX.md | KB/INDEX.md
