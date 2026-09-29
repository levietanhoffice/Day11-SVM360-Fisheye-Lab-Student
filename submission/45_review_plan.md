# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `adasind_019560.jpg` (zone `center`) | 18 lỗi SPURIOUS | Đây là nơi model "ảo giác" (hallucinate) vẽ thừa nhiều nhất do các vật thể nhỏ chồng lấp. | Hình chụp các hộp thừa không có vật thật để đối chứng quy tắc H=40px. |
| `adasind_062370.jpg` (zone `edge`) | 12 lỗi MISSING, 1 BOX_GEOMETRY | Thể hiện điểm yếu chí mạng của cả model và người gán nhãn trong việc xử lý độ méo fisheye ở rìa. | Hình chụp vật thể bị uốn cong ở rìa kèm tọa độ hộp bị sai để bổ sung vào guideline. |

Giới hạn của kết luận từ ba frame ADASIND: 3 bức ảnh là tập mẫu quá nhỏ bé và mang tính cục bộ tĩnh, không đại diện được cho tất cả các tình huống như thay đổi ánh sáng, thời tiết, hoặc các góc che khuất khác nhau khi xe di chuyển trên đường.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi:
- Để tránh trùng lặp bối cảnh (cùng một chiếc xe/góc rẽ), ta dùng chiến lược lấy mẫu có khoảng cách (ví dụ mỗi giây/chục giây chỉ trích 1 frame thay vì lấy liên tiếp).
- Kế hoạch 200 frame này mang tính chất lấy mẫu "corner case" (tìm kiếm có chủ đích vào các điều kiện khó như ban đêm, méo rìa, xe đông) để vạch trần lỗi (debug). Nó không được chọn ngẫu nhiên theo phân phối xác suất tự nhiên của thế giới thực, do đó không thể dùng để tính toán hay đo lường độ chính xác (%) tổng thể của hệ thống.
