# Danh sách lớp v0 — Hoàng Bá Đạt · G10

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `face` (`eye_left`, `eye_right`) | `open` / `closed` / `unknown` | Tính tỷ lệ nhắm mắt (PERCLOS) để cảnh báo tài xế buồn ngủ hoặc ngủ gật | Có, trừ khi bị chói phản xạ LED trên tròng kính hoặc tóc/tay che |
| 2 | `face` (`gaze_zone`) | `road` / `mirror_l` / `mirror_r` / `mirror_c` / `cluster` / `center` / `lap` / `other` | Xác định vùng nhìn để cảnh báo tài xế mất tập trung rời mắt khỏi đường quá lâu | Có (qua hướng đầu và đồng tử trên ảnh NIR) |
| 3 | `face` (`glasses`) | `none` / `clear` / `sun` / `unknown` | Điều chỉnh độ tin cậy của nhánh ước lượng mắt/gaze khi tài xế đeo kính cận hoặc kính râm | Một phần: thấy gọng kính, nhưng khó phân biệt kính râm với kính trong trên NIR |
| 4 | `face13` (13 điểm mặt) | 13 tọa độ `(x, y)` + cờ `occluded` / `outside` | Ước lượng góc quay đầu (head pose: yaw/pitch/roll), độ mở mắt và trạng thái ngáp | Có (rõ nét cả ban đêm nhờ đèn NIR 940 nm, trừ vùng bị che/chói) |
| 5 | `hand` (`whose`, `side`, `on_wheel`) | `driver`/`passenger` · `left`/`right` · `yes`/`no`/`unknown` | Kiểm tra tài xế có đặt tay lên vô lăng để sẵn sàng tiếp quản xe (hands-off warning) | Có (hình dạng bàn tay và vị trí tương đối với vô lăng) |
| 6 | `phone` (`state`) | `held` / `mounted` / `lap` | Phát hiện hành vi cầm hoặc dùng điện thoại gây mất tập trung khi lái xe | Có nếu thấy cạnh/góc/màn hình; khó phân biệt với vật tối hình chữ nhật khác |
| 7 | `person` (`seatbelt`) | `worn_correct` / `worn_incorrect` / `not_worn` / `unknown` | Nhắc thắt dây an toàn và phát hiện thắt dây sai cách (dưới nách/sau lưng) cho tài xế | Có nếu độ tương phản giữa dây và áo đủ rõ; dễ bị chìm trên áo tối màu |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` (`seat`) | `rear_left` / `rear_middle` / `rear_right` | Đếm số hành khách và xác định đúng vị trí ghế đang có người ngồi để điều khiển túi khí/cảnh báo | Có (hình dạng cơ thể và vị trí ghế) |
| 2 | `person` (`seatbelt`) | `worn_correct` / `worn_incorrect` / `not_worn` / `unknown` | Cảnh báo hành khách hàng ghế sau chưa thắt dây hoặc thắt dây an toàn sai quy cách | Hạn chế: mất màu, dây tối màu trên áo tối khó phân biệt nếu không có độ tương phản |
| 3 | `face` (box) | rectangle | Xác nhận đối tượng là người thật (tránh nhận nhầm đồ vật lớn) và hỗ trợ theo dõi tư thế đầu hành khách | Có (nếu hành khách không quay lưng hoàn toàn) |
| 4 | `child_seat` (`seat`, `occupied`) | `rear_*` · `no` / `unknown` | Phát hiện ghế trẻ em lắp trên hàng ghế sau để hỗ trợ cảnh báo quên trẻ (CPD) và cấu hình an toàn ghế | Có (hình dạng ghế tựa lưng đặc trưng), nhưng khó thấy rõ bên trong nếu bị phủ tối |
| 5 | `infant_seat` (`seat`, `facing`) | `rear_*` · `rear` / `front` | Nhận diện nôi em bé và hướng lắp nôi (quay trước/sau) để kích hoạt cảnh báo an toàn & túi khí phù hợp | Có (hình dạng nôi xách), hướng `facing` nhìn theo cấu trúc nôi |
| 6 | `object` (`seat`, `type`) | `rear_*` · `bag` / `box` / `cup` / `other` | Phân biệt đồ vật đặt trên ghế với người ngồi (tránh báo giả chưa thắt dây) và nhắc quên đồ trên xe | Có về hình dạng/vị trí, nhưng mất thông tin màu sắc và hoa văn nên vật nhỏ tối màu dễ bị nhầm |

## 2 câu hỏi leo thang

1. Câu hỏi: Trên ảnh OMS (`S##`), trường `face` có cần giữ cố định mặc định `unknown` cho `eye_left`, `eye_right`, `glasses`, hay người gán được phép điền `open`/`none` nếu nhìn thấy rõ?
   Khung ví dụ: `S04_ir.png` (ghế hành khách phía sau).
   Bạn tạm gán thế nào và vì sao: Sau khi review chéo với bạn, mình thống nhất đưa cả `eye_left`, `eye_right`, `glasses` trên `S04_ir.png` về `unknown` cho đúng mặc định bảng §4.1 ("OMS chỉ vẽ box `face`") và tránh đoán trên ảnh IR-sim.

2. Câu hỏi: Với ảnh IR mô phỏng (`IR_sim` trong SVIRO) không có ai thắt dây an toàn (`seatbelt` chỉ có `not_worn`/`unknown`), dữ liệu này có nên đưa vào tập huấn luyện bộ phân loại `seatbelt` của OMS không, hay chỉ dùng để huấn luyện phát hiện người/ghế/vật?
   Khung ví dụ: `S03_rgb.png`, `S03_ir.png` (và toàn bộ chuỗi `S01–S08`).
   Bạn tạm gán thế nào và vì sao: Mình tuân thủ Guideline v1.0 chỉ chọn `not_worn` hoặc `unknown` (tuyệt đối không gán `worn_*`) và ghi nhận giới hạn phân bố lớp này để nhóm dữ liệu bổ sung thêm dữ liệu có thắt dây thật ở phiên bản tiếp theo.
