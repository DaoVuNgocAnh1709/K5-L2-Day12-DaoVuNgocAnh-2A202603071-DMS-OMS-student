# TEAM — Ngày 12

Mã bộ ảnh: **G05** · Hình thức: cá nhân

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Đào Vũ Ngọc Anh | 2A202603071 | có | Bạn ghép cặp nhóm G05 (`peer_export_final.zip`) | 46 dòng |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- `S02_rgb.png`, `S02_ir.png` và `S08_rgb.png`, `S08_ir.png`: Ghế trẻ em (`child_seat`) có hình nộm/trẻ em ngồi bên trong nhưng schema ban đầu chỉ có `unknown/no` mà thiếu giá trị `yes`. Đã hỏi coach và coach xác nhận cho phép cập nhật `scripts/cabin_schema.py` bổ sung giá trị `yes` đại diện cho trường hợp ghế có trẻ em ngồi.

## Cá nhân

### DaoVuNgocAnh-2A202603071
- **Phần mình làm:** Gán nhãn độc lập toàn bộ 22 ảnh cốt lõi (16 ảnh SVIRO + 6 ảnh Drive&Act), tự kiểm tra script đạt 0 lỗi 0 cảnh báo, chạy script diff so sánh và điền biên bản review chéo 46 dòng với bạn nhóm G05.
- **Điều mình học được hôm nay:** Nắm vững quy ước không gian cabin (ghế sau gọi theo xe nên trái ảnh là `rear_right`), nguyên tắc giải phẫu trên ảnh xoay 90° (mắt trái có y lớn hơn), và cách đánh cờ `occluded` khi gặp hiện tượng lóa LED hồng ngoại NIR.