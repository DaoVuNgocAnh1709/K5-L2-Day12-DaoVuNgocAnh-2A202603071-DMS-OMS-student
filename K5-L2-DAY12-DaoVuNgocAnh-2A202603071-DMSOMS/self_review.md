# Tự đánh giá — Đào Vũ Ngọc Anh · G05

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_ir.png | object (túi xách ghế giữa) | `seat_flip` | Ban đầu bị CVAT tự động điền `seat: driver`, đã sửa thành `rear_middle` và `type: bag` | Đã sửa |
| S05_ir.png | frame_meta | `missing` | Bị sót chưa tạo tag frame_meta ở lượt gán đầu, đã bổ sung tag ir/unknown/no | Đã sửa |
| D02.png | face (mắt dưới đốm phản xạ) | `guess` | Ban đầu định gán open theo quán tính, sau đó đọc kỹ guideline đã đổi sang unknown và bật cờ occluded cho face13 | Đã sửa |
| D04.png | hand (tay lái) | `lr_flip` | Chú ý phân biệt tay trái/phải theo giải phẫu người lái thay vì theo hướng ảnh chụp | Đã sửa |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

* **Lỗi:** Bị CVAT tự động điền thuộc tính mặc định đầu tiên của danh sách (ví dụ box `object` tự gán `seat: driver` trên ảnh SVIRO, hoặc `child_seat` tự chọn giá trị đầu).
* **Vì sao mình mắc:** Thao tác vẽ nhanh nhiều đối tượng liên tiếp và lưu ngay mà chưa mở tab DETAILS để rà soát lại toàn bộ thuộc tính của từng shape.
* **Lần sau tránh bằng cách:** Áp dụng quy tắc kiểm tra 2 bước: sau khi vẽ xong tất cả hình của 1 ảnh, dừng lại 5 giây nhìn cột Objects bên phải để rà soát từng dòng thuộc tính trước khi bấm Ctrl+S chuyển ảnh.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó:
* Ở khung `S02_rgb.png`, bạn chọn thuộc tính `facing: rear` cho nôi em bé (`infant_seat`), trong khi mình chọn `front`. Sau khi trao đổi và đối chiếu kiến thức an toàn xe hơi, nôi xách sơ sinh bắt buộc phải lắp quay mặt về phía sau xe (rear-facing) để bảo vệ cổ và cột sống của trẻ nhỏ khi có va chạm trước. Mình đã học được thêm kiến thức domain ô tô thực tế và thống nhất cập nhật theo bạn.