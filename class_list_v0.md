# Danh sách lớp v0 — Đào Vũ Ngọc Anh · G05

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (Driver Monitoring System — 7 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `eye_state` | `open` / `closed` / `unknown` | Tính chỉ số PERCLOS để phát hiện buồn ngủ, ngủ gật (mắt nhắm > 80% trong khoảng thời gian xác định). | Có, trừ khi bị đốm phản xạ LED hồng ngoại che phủ. |
| 2 | `gaze_zone` | `road` / `cluster` / `center` / `lap` / `mirror_*` / `other` | Phát hiện tài xế xao nhãng, mất tập trung (nhìn đùi xem điện thoại, nhìn sang ghế phụ quá 2 giây). | Có, suy ra từ vector hướng nhìn kết hợp tư thế đầu. |
| 3 | `head_pose` | Pitch / Yaw / Roll (góc cúi, quay, nghiêng) | Đánh giá tư thế đầu tài xế (gục đầu ngủ, quay đầu nói chuyện, ngất xỉu mất nhận thức). | Rất rõ trên IR nhờ cấu trúc hình học khuôn mặt. |
| 4 | `hand_on_wheel` | `yes` / `no` / `unknown` | Kiểm tra điều kiện bàn giao quyền điều khiển (Take-over Request) trên xe tự hành cấp độ L2/L3. | Có, xác định bàn tay tiếp xúc với vành vô lăng. |
| 5 | `phone_interaction` | `held` / `mounted` / `lap` / `none` | Cảnh báo vi phạm giao thông: sử dụng điện thoại khi đang điều khiển phương tiện. | Có (dáng máy chữ nhật, viền màn hình sáng). |
| 6 | `glasses_type` | `none` / `clear` / `sun` / `unknown` | Điều chỉnh thuật toán trích xuất mắt phù hợp (bù trừ khúc xạ kính, loại trừ lóa phản xạ). | Có, tia NIR có thể xuyên qua một số tròng kính râm. |
| 7 | `driver_seatbelt` | `worn_correct` / `worn_incorrect` / `not_worn` | Cảnh báo chưa thắt dây an toàn hoặc thắt sai quy cách (luồn dây sau lưng, kẹp nách). | Có, thấy vệt dải đai chéo phản xạ NIR qua vai. |

## OMS (Occupant Monitoring System — 7 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `seat_occupancy` | `empty` / `person` / `child_seat` / `infant_seat` / `object` | Quản lý trạng thái từng ghế sau; tự động bật/tắt đèn trần và nhắc thắt dây an toàn. | Có, dựa trên biên dạng đối tượng trên ghế. |
| 2 | `child_presence` | `child_seat_occupied` / `infant_present` / `none` | Cảnh báo chống bỏ quên trẻ em trong xe (Child Presence Detection - tiêu chuẩn Euro NCAP). | Có hình dáng ghế nôi và cử động của trẻ. |
| 3 | `airbag_suppression` | `enable` / `disable` | Tắt túi khí tự động nếu ghế trước lắp nôi em bé quay ngược chiều (tránh chấn thương khi nổ túi khí). | Có, dựa vào loại nôi (`infant_seat`) và chiều quay (`facing`). |
| 4 | `rear_seatbelt` | `worn_correct` / `not_worn` / `unknown` | Nhắc nhở hành khách ghế sau cài dây an toàn theo luật giao thông. | Có trên ảnh thực tế (trên SVIRO mô phỏng luôn là `not_worn`). |
| 5 | `object_left_behind` | `bag` / `box` / `cup` / `other` | Cảnh báo quên đồ đạc có giá trị khi tài xế tắt máy rời xe. | Có, nhận diện khối đồ vật sót lại trên mặt ghế. |
| 6 | `seat_position` | `rear_left` / `rear_middle` / `rear_right` | Định vị chính xác vị trí hành khách để kích hoạt túi khí rèm hông và tối ưu điều hòa vùng. | Có, phân định 3 vị trí ghế theo tọa độ không gian xe. |
| 7 | `infant_facing` | `rear` / `front` | Xác định nôi xách em bé lắp quay mặt về sau (rear-facing) hay quay về trước (front-facing). | Có, phân biệt quai xách và chiều lòng nôi. |

## 2 câu hỏi leo thang

### Câu hỏi 1:
* **Nội dung:** Khi ghế trẻ em có búp bê / mô hình trẻ em ngồi bên trong (như trên bộ ảnh SVIRO), hệ thống nên gán nhãn như thế nào? Hiện tại nhãn `child_seat` chỉ có thuộc tính `occupied: no / unknown` mà không có giá trị `yes`, và quy tắc cấm vẽ `person` cho trẻ em. Điều này khiến bài toán Child Presence Detection (CPD) không có nhãn ground-truth để học.
* **Khung ví dụ:** Khung `S02_rgb.png` và `S02_ir.png` (ghế `rear_left` có ghế trẻ em và búp bê ngồi bên trong).
* **Cách tạm gán và lý do:** Nhóm tạm thời gán `child_seat` với thuộc tính `occupied: yes` (đã được coach phê duyệt cho phép cập nhật schema) và không vẽ đè box `person`, vì nhãn `person` theo quy định bài này chỉ dành cho người lớn.

### Câu hỏi 2:
* **Nội dung:** Trên ảnh hồng ngoại NIR chụp góc nghiêng 90° của Drive&Act, khuôn mặt tài xế quay hẳn sang một bên khiến một bên mắt bị sống mũi che khuất hoàn toàn. Nên chuẩn hóa quy tắc: điểm mốc của mắt bị khuất hoàn toàn đó đánh cờ `outside` hay kéo về vị trí giải phẫu ước lượng rồi đánh cờ `occluded`?
* **Khung ví dụ:** Khung `D03.png` và `D05.png` (mắt bên kia khuôn mặt bị che khuất hoàn toàn bởi góc quay nghiêng).
* **Cách tạm gán và lý do:** Nhóm tạm thời đặt điểm ở vị trí ước lượng giải phẫu sau sống mũi và bật cờ `occluded: 1` (kèm giải thích trong review log), nhằm giúp mô hình học được mối tương quan hình học 3D của khuôn mặt ngay cả khi bị che khuất một phần.