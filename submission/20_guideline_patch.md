# Guideline patch

- **Rule mới đề xuất:** R08 (Bổ sung cho R02): Đối với các vật thể nằm ở vùng rìa ảnh (`edge`) bị biến dạng cong mạnh do thấu kính fisheye, hộp giới hạn (bounding box) phải được vẽ chạm chính xác vào các điểm cực đại (cong nhất) của vật thể, không được tự ý "nắn thẳng" hình khối hay kéo hộp quá rộng bao lấy khoảng trắng.
- **Áp dụng cho:** Tất cả các class phương tiện (Car, Bike, Bus, Truck, ThreeWheeler) nằm trong zone `edge`.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** Luật R02 hiện hành chỉ yêu cầu "Bám sát mép ngoài nhìn thấy được" nhưng chưa có hướng dẫn rõ ràng về cách xử lý độ cong đặc thù của ảnh 360 độ, dẫn tới việc nhãn thủ công (L) hay dính lỗi `BOX_GEOMETRY` ở vùng rìa.
- **`rules_version` mới:** v1.1.0
- **Hiệu lực từ:** Vòng gán nhãn tiếp theo (Round 2 / Rework phase 2).
