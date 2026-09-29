# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy tắc riêng? Vì sao?
   **Trả lời:** Cần một quy tắc riêng (ví dụ: Cross-camera matching policy). Vì trên mặt phẳng 2D, chúng nằm ở 2 bức ảnh khác nhau nên không thể gọi là `DUPLICATE` cục bộ được. Hệ thống cần thuật toán chiếu lên không gian 3D (BEV) và quy tắc xem camera nào được ưu tiên "giữ" box dựa trên diện tích vùng hiện diện.
2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera.
   **Trả lời:** Giữ cùng Track ID khi vật xuất hiện liên tục và quỹ đạo đoán trước được. Thêm keyframe khi vật đổi hướng/vận tốc đột ngột. Đổi sang trạng thái Outside khi vật tạm thời văng khỏi khung hình hoặc bị che khuất hoàn toàn. Bằng chứng cần trước khi nối track qua 2 camera: (1) Frame phải đồng bộ thời gian (cùng timestamp), (2) Đặc điểm xe khớp nhau và (3) Vị trí trên không gian 3D nối tiếp nhau hợp lý.
3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`), bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm?
   **Trả lời:** Tại `adasind_062370.jpg`, có vài xe ở xa tôi ước lượng bằng mắt thấy khá rõ nét nên vẽ box, nhưng hệ thống báo lỗi vi phạm R01 vì chiều cao dưới 40px. Tôi đã xử lý bằng cách nhượng bộ và xóa box để bám sát luật cứng. Nếu làm lại, tôi sẽ dùng công cụ đo kích thước pixel trực tiếp trên CVAT trước khi quyết định vẽ các vật thể ở rìa xa để không bị tốn công sửa.
