# TEAM — Ngày 12

Mã bộ ảnh: **G10** · Hình thức: cá nhân (ghép cặp review chéo)

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Hoàng Bá Đạt | 2A202603100 | có | Nguyễn Hồng Sơn | 20 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- Không có ca nào chưa thống nhất: sau khi đối chiếu lại Guideline Cabin v1.0, cả 20/20 dòng trong `disagreement_log.csv` đều đã thống nhất hoàn toàn (Đạt sửa 4 dòng ở `S03_rgb.png` và `S04_ir.png`; Sơn sửa 16 dòng ở `D05.png`, `S03`, `S05`, `S07`, `S08`).

## Cá nhân

### HoangBaDat-2A202603100
- Phần mình làm: Tự gán đủ 22 ảnh cốt lõi (`S01–S08`, `D01–D06`) và 4 ảnh mở rộng (`S09–S10`) trên CVAT local; chạy `cabin_check.py` ở Checkpoint A, B, Final; review chéo (`diff`) với Nguyễn Hồng Sơn; sửa 2 lỗi phát hiện sau review (`S03_rgb.png` `modality=rgb`, `S04_ir.png` `glasses=unknown`) để xuất `export_final_v2.zip` đạt 0 lỗi, 0 cảnh báo.
- Điều mình học được hôm nay: Ánh xạ vị trí ghế theo xe ngược trái/phải với ảnh camera OMS (`trái ảnh = rear_right`), luôn bật cờ `occluded` cho điểm `face13` bị che trên ảnh NIR xoay 90°, chọn `unknown` thay vì đoán khi không chắc, và tách biệt rõ hiện tượng của ảnh IR mô phỏng (`IR_sim`) với ảnh cận hồng ngoại thật (`real_IR`).
