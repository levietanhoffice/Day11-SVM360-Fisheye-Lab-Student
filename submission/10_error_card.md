# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B2 | MISSING | 8 |
| center | B2 | SPURIOUS | 10 |
| center | C0 | SPURIOUS | 2 |
| edge | B2 | BOX_GEOMETRY | 1 |
| edge | B2 | MISSING | 1 |
| edge | B2 | SPURIOUS | 3 |
| mid | B2 | MISSING | 3 |
| mid | B2 | SPURIOUS | 3 |

## Top defects
- SPURIOUS: 18 (ví dụ frame adasind_019560.jpg)
- MISSING: 12 (ví dụ frame adasind_062370.jpg)
- BOX_GEOMETRY: 1 (ví dụ frame adasind_062370.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: Lỗi phổ biến nhất là `SPURIOUS` (18 lỗi) và `MISSING` (12 lỗi). Nguyên nhân chủ yếu là do sự bóp méo hình ảnh của camera fisheye khiến các vật thể bị biến dạng hoặc chồng lấp lên nhau, làm model dễ nhận diện sai (spurious) hoặc trượt box so với thực tế. Đối với người gán nhãn, lỗi `SPURIOUS` đến từ việc vẽ hộp cho các vật thể quá bé (chiều cao < 40px, vi phạm R01) hoặc nhầm class, còn `MISSING` là do bỏ sót xe bị che khuất hoặc nhỏ ở rìa (edge).
- Cách sửa và ai nhận việc (`owner`): Người gán nhãn (Lê Việt Anh) chịu trách nhiệm sửa (Rework). Cần rà soát kỹ các frame (đặc biệt `adasind_019560.jpg` và `adasind_062370.jpg`) trên CVAT, xóa bỏ các hộp < 40px, bổ sung các xe bị thiếu và nắn lại hộp (BOX_GEOMETRY) bám sát đường cong vật thể. Đồng thời, thêm polygon `ignore_region` cho `ego_body` để không bị nhận diện nhầm phần mui xe/tay lái.
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): Dựa vào số liệu trong bảng thống kê (18 SPURIOUS, 12 MISSING) và các dòng ghi nhận lỗi trong file `findings.csv` đối chiếu với bộ luật R01 (về kích thước H=40px) và R07 (yêu cầu vẽ ignore_region).
