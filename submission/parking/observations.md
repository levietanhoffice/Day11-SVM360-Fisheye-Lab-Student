# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh): Các vạch sơn màu trắng nằm ở khu vực tiền cảnh (gần camera nhất), phân định ranh giới giữa hai ô đỗ xe kế tiếp nhau.
- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao: Không vẽ vạch sơn dài nằm ngang ngăn cách giữa khu vực đỗ xe và lối đi chung của xe cộ, vì quy tắc quy định chỉ đánh dấu vạch chia ô đỗ (parking_line), không vẽ vạch kẻ phân làn chạy.
- Polygon `free_space` dừng ở đâu; có phần bị che nào không: Vùng `free_space` dừng ở biên của các ô đỗ hợp lệ, và dừng ở mép bánh xe hoặc mép xe đối với những chiếc xe đang đỗ. Có những phần đằng sau các xe đang đỗ bị che khuất nên vùng free space không lấn qua đó.
- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”): Không có.
