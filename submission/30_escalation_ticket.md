# Escalation ticket

## Ticket 1

- **Frame:** Tất cả các frame trong slice (đặc biệt `adasind_062370.jpg` và `adasind_019560.jpg`)
- **Ảnh chụp:** Xem lại các box lỗi trong `qa_overlay.html`
- **Expected impact:** Nghiêm trọng (High) - Model dự đoán trượt hoàn toàn ở vùng rìa (`edge`) và báo lỗi `SPURIOUS`/`MISSING` mật độ cao ở `center`, gây nguy hiểm nếu áp dụng thực tế cho hệ thống ADAS/xe tự hành.
- **Owner:** `ai_team`
- **Recommendation:** Yêu cầu đội AI huấn luyện bổ sung (fine-tune) model trên tập dữ liệu đã qua xử lý méo hình fisheye, hoặc áp dụng các kỹ thuật augmentation chuyên biệt cho thấu kính góc siêu rộng. Cần thiết kế lại hàm loss hoặc cơ chế đánh giá IoU để tương thích với hình khối cong.
