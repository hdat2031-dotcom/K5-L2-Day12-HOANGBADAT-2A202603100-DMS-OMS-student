# Tự đánh giá — Hoàng Bá Đạt · G10

## 1. Tự rà soát 4 cảnh

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| `S03_rgb.png` | `frame_meta` | `wrong_class` | Để nhầm `modality = ir` trên ảnh `_rgb` (phát hiện khi `diff` với Nguyễn Hồng Sơn) | Đã sửa thành `rgb` ở `export_final_v2.zip` |
| `S04_ir.png` | `face` | `guess` | Để `glasses = none` dù trên ảnh IR-sim không chắc hoàn toàn có đeo kính hay không | Đã sửa thành `unknown` ở `export_final_v2.zip` |
| `D05.png` | `face13` (`left_eye_*`) | `flag` | Chọn `eye_left = unknown` nhưng ban đầu quên bật cờ `occluded` cho 4 điểm mắt trái (`cabin_check` báo WARN) | Đã bật `occluded = 1` cho cả 4 điểm ở `export_final.zip` |
| `D01.png` | `person`, `face`, `face13`, `hand` | `ok` | Đủ thuộc tính, trục mắt trái có y lớn hơn mắt phải đúng chiều ảnh xoay 90°, `on_wheel` đúng thực tế | Không cần sửa |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Quên cập nhật thuộc tính mặc định hoặc cờ phụ sau khi thao tác nhanh trên CVAT (như quên đổi `modality` trên `S03_rgb.png`, quên bật cờ `occluded` ở `face13` trên `D05.png`, và ban đầu để `occupied = yes` ở `S09` phần mở rộng).

Vì sao mình mắc: Chưa quen giao diện CVAT ở các khung đầu, tập trung vào việc vẽ box sát mép nên dễ bỏ qua bảng `DETAILS` hoặc danh sách `PARTS` của `face13`.

Lần sau tránh bằng cách: Luôn làm đúng thứ tự `frame_meta` → vẽ hình → mở ngay `DETAILS`/`PARTS` kiểm từng thuộc tính trước khi sang khung kế tiếp, rồi chạy `cabin_check.py` ở từng checkpoint nhỏ.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai: `S03_rgb.png | frame_meta | modality` (`mine = ir`, `peer = rgb`) và `S04_ir.png | face | glasses` (`mine = none`, `peer = unknown`). Mình học được rằng `cabin_check` không tự bắt hết mọi lỗi ngữ nghĩa (như `modality` ngược với tên file `_rgb` hay việc đoán `none` thay vì `unknown`), nên bước review chéo (`diff`) giúp phát hiện những lỗi rất nhỏ nhưng quan trọng cho chất lượng dữ liệu huấn luyện.
