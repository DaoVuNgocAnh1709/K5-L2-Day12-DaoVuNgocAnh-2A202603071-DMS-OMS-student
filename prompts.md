# prompts — khai báo dùng AI (RULES §3)

Dùng AI để làm gì hôm nay: **hỏi quy tắc / hướng dẫn thao tác CVAT / giải thích thuộc tính gaze_zone và skeleton face13**

## Các prompt đáng chú ý

1. Mục đích: Hỏi về thuộc tính `gaze_zone` và cách xử lý thuộc tính `face` trên ảnh SVIRO ghế sau.
   * **Prompt:** "cái attibute kia là gì" (kèm ảnh chụp màn hình dropdown gaze_zone).
   * **Mô hình:** Gemini 3.8 Flash.
   * **Kết quả:** Dùng được ngay (hiểu rõ ý nghĩa các vùng nhìn và biết ảnh OMS ghế sau chỉ cần vẽ box, không bắt buộc thuộc tính chi tiết).

2. Mục đích: Tra cứu quy tắc gán mắt và skeleton `face13` khi tài xế đeo kính và bị tóc che.
   * **Prompt:** "tóc che mắt đeo kính đánh thế nào?" (kèm ảnh chụp cận mặt tài xế nghiêng 90°).
   * **Mô hình:** Gemini 3.8 Flash.
   * **Kết quả:** Dùng được ngay (biết gán `eye = unknown` và bật cờ `occluded` cho điểm mắt để khớp với hàm kiểm tra của script).

3. Mục đích: Tra cứu vị trí file script kiểm tra schema khi coach thông báo bổ sung trường hợp `occupied: yes`.
   * **Prompt:** "bảo các em tự sửa file chấm bao vào trường hợp yes, hãy cho tôi biết file chấm là file nào trước khi sửa".
   * **Mô hình:** Gemini 3.8 Flash.
   * **Kết quả:** Dùng được ngay (xác định đúng dòng 48 trong `scripts/cabin_schema.py` và cập nhật thành công).