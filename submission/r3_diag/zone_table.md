# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 13 | 2 | 2 | 6 | 7 | MISSING (2) |
| mid | 5 | 0 | 0 | 2 | 3 | — |
| edge | 2 | 1 | 1 | 2 | 3 | BOX_GEOMETRY (1) |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên: Cả người (L) và model (M) đều mắc nhiều lỗi nhất ở zone `center` về mặt số lượng (L có 2 missing, 2 spurious; M có 6 missing, 7 thừa trên tổng 13 vật). Xét theo tỷ lệ thì ở zone `edge`, model gãy hoàn toàn (n_ref = 2 nhưng M missing 2 và vẽ thừa 3), người cũng dính 1 missing, 1 spurious cùng lỗi BOX_GEOMETRY.
- Giả thuyết vì sao (méo fisheye, box lỏng, thiếu `ego_body`, ...) và giới hạn của slice ba frame: Model có thể không được huấn luyện chuyên sâu với độ biến dạng của ảnh fisheye, dẫn đến trượt box hoặc nhận diện sai ở các vùng rìa cong. Lỗi của người (L) có thể do chưa bám sát được vật thể bị bóp méo ở `edge` hoặc do quên loại trừ vùng `ego_body`. Hạn chế: Slice chỉ có 3 frame là mẫu dữ liệu quá nhỏ, không đủ đại diện để đưa ra kết luận tổng quát về khả năng của model hay người dán nhãn trên toàn bộ hệ thống camera.
