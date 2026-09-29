# Thành viên và phân vai — Day11 SVM 360 Fisheye

## 1. Thông tin nhóm

- Khóa/lớp: AI20K
- Tên nhóm: NoName
- Repo Public: [https://github.com/levietanhoffice/Day11-SVM360-Fisheye-Lab-Student](https://github.com/levietanhoffice/Day11-SVM360-Fisheye-Lab-Student)
- Máy giữ hồ sơ chính / người quản lý: Lê Việt Anh
- Slice chung lấy từ mode.json: B2-dense
- Tên định danh vai A dùng cho --self: nguyen (hoặc anh trên máy chủ hồ sơ)
- Kênh trao đổi nội bộ: Zalo / Discord nhóm
- Đại diện nộp (vai C): Lê Việt Anh, MSSV: 2A202602111
- Commit chốt bài: 4a176e8917c4d26b1a83063ea4daa8635d521f25

## 2. Ba vai chính

| Vai                       | Họ và tên         | MSSV        | Tên định danh trong mode | Trách nhiệm                                         | Bằng chứng đóng góp                                                                                                                                        |
| ------------------------- | ----------------- | ----------- | ------------------------ | --------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A · Gán nhãn              | Lê Võ Khôi Nguyên | 2A202602178 | nguyen                   | Parking/C0/slice, self-QC, lock, rework             | [`submission/r1_craft/`](submission/r1_craft/), [`submission/rework/`](submission/rework/), mã khóa `5A25-BE35`                                            |
| B · QA độc lập            | Trần Minh Nhật    | 2A202602079 | nhat                     | Review trước reference, finding QA, kiểm lại ca sửa | [`submission/r2_qa/qa_review.md`](submission/r2_qa/qa_review.md), [`submission/r2_qa/qa_overlay.html`](submission/r2_qa/qa_overlay.html)                   |
| C · Chẩn đoán & điều phối | Lê Việt Anh       | 2A202602111 | anh                      | Báo cáo, phân xử, kế hoạch, tích hợp, check và nộp  | [`submission/r3_diag/`](submission/r3_diag/), [`submission/findings.csv`](submission/findings.csv), [`submission/manifest.json`](submission/manifest.json) |

Bảng này xác định vai của nhóm. Vòng QA tự sinh trong team.json thuộc quy trình nhiều hồ sơ của CLI; nhóm dùng một slice chung và quy trình A → B → C đã nêu trong hướng dẫn.

## 3. Bàn giao theo pha

| Mốc                         | Người giao → nhận | File / commit / mã khóa                                   | Người nhận đã kiểm gì?                                    | Trạng thái / vướng mắc |
| --------------------------- | ----------------- | --------------------------------------------------------- | --------------------------------------------------------- | ---------------------- |
| P0 · Chốt môi trường và vai | C → A, B          | `mode.json`, slice `B2-dense`, phân vai A/B/C             | Kiểm tra môi trường CVAT local, cấu hình mode và doctor   | Hoàn thành             |
| P2 · Khóa bản đầu           | A → B, C          | `r1_craft/annotations.xml`, `lock.txt`, code: `5A25-BE35` | B kiểm tính nguyên vẹn mã hash, đối chiếu checklist 9 mục | Hoàn thành             |
| P3 · Chốt QA mù             | B → C, A          | `qa_review.md`, 3 findings `r2_qa`, ảnh lỗi               | C duyệt các ghi nhận lỗi bám sát guideline R01/R02/R07    | Hoàn thành             |
| P4 · Quyết định sửa         | C → A, B          | `findings.csv`, `40_decision_log.csv`, so sánh model      | Thống nhất ca rework: xóa box < 40px, bổ sung ego_body    | Hoàn thành             |
| P5 · Kiểm bản sửa           | A → B → C         | `annotations-v2.xml`, `lock2.txt`, `delta.md`             | B kiểm tra lại các ca đã sửa; C chạy rework & đo delta    | Hoàn thành             |
| P6 · Chốt nộp               | A, B → C          | `manifest.json`, commit chốt                              | Kiểm tra cổng `lab11.py check` exit 0, hồ sơ đầy đủ       | Sẵn sàng nộp           |

## 4. Bất đồng và phối hợp

- Một ca đã phân xử: Tại frame `adasind_062370.jpg`, đối tượng xe ở xa (L4): Người gán nhãn (A) vẽ box theo mắt nhìn, nhưng QA (B) bắt lỗi vi phạm rule R01 do chiều cao box < 40px. Quyết định (C): Thống nhất tuân thủ rule R01, loại bỏ box < 40px và ghi nhận vào decision log (ID: 2).
- Ca còn mở: Không còn (các vấn đề model trượt ở vùng rìa thấu kính fisheye đã được lập escalation ticket gửi cho ai_team theo dõi).
- Đóng góp của A/B/C vào kế hoạch và exit ticket: Cả nhóm cùng thảo luận phân bổ 200 frame (`45_sampling_plan.csv`) cho 4 camera quanh xe và thiết lập tiêu chí xây dựng Gold Set (`46_gold_set_plan.md`); C hoàn thiện tổng hợp và biên soạn `50_exit_ticket.md`.
- Thay đổi phân công nếu có: Giữ nguyên phân công ban đầu xuyên suốt quá trình thực hành.

## 5. Xác nhận trước khi nộp

- [x] A xác nhận nhãn và export đúng phiên bản: Lê Võ Khôi Nguyên (`submission/r1_craft/annotations.xml`, `submission/rework/annotations-v2.xml`)
- [x] B xác nhận đã QA độc lập trước reference và kiểm lại ca sửa: Trần Minh Nhật (`submission/r2_qa/qa_review.md`)
- [x] C xác nhận báo cáo đúng bản khóa, các file đầy đủ và check exit 0: Lê Việt Anh (`python3 lab11.py check` pass)
- [x] manifest.json tại commit chốt có failed_gates rỗng.
- [x] Repo nhóm Public, ảnh và các bằng chứng mở được.
- [x] C đã push và gửi link repo nhóm + commit qua kênh lớp công bố.

Chỉ đánh dấu việc đã kiểm thật. Nhóm nộp một hồ sơ chung; check không tự chấm đóng góp từng người. Giữ nguyên header/các cột enum của findings.csv; tên người được ghi trong tài liệu này hoặc phần note thích hợp.
