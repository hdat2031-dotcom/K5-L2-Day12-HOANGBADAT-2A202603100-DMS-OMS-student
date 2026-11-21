# Khai báo dùng AI — Hoàng Bá Đạt

Nhắc lại: không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Antigravity (Gemini) | Cách thao tác trên giao diện CVAT (gắn tag `frame_meta`, vẽ rectangle, vẽ skeleton `face13`, bật cờ `occluded`, export CVAT 1.1 không kèm ảnh, upload annotations) | Làm theo từng bước thao tác UI trên CVAT local | Có, kiểm trực tiếp trên `localhost:8080` và đối chiếu `INSTALL_CVAT.md` |
| 2 | Antigravity (Gemini) | Giải thích quy tắc Guideline Cabin v1.0 bằng chữ (ánh xạ ghế `rear_right`/`rear_left`, phân biệt `child_seat`/`infant_seat`, quy tắc vẽ `object` trong ghế, quy tắc `face` và `phone`/`cup` trên OMS vs DMS, quy tắc `unknown`) | Áp dụng để tự quyết định nhãn và thuộc tính khi gán 22 ảnh cốt lõi và 4 ảnh mở rộng | Có, đối chiếu trực tiếp với `GUIDE.md` và `COMMON_ERRORS.md` |
| 3 | Antigravity (Gemini) | Hướng dẫn chạy `scripts/cabin_check.py` (check Checkpoint A/B/Final, diff review chéo với bạn Nguyễn Hồng Sơn) và cách sửa cảnh báo/lỗi `cabin_check` | Tự chạy lệnh trong Terminal VS Code, xử lý 20 dòng `disagreement_log.csv` và xuất `export_final_v2.zip` | Có, chạy `cabin_check.py check` đạt 0 lỗi, 0 cảnh báo và kiểm `python -m zipfile -l` |
| 4 | Antigravity (Gemini) | Góp ý câu chữ và cấu trúc cho `class_list_v0.md`, `TEAM.md`, `self_review.md`, `ir_log.csv` | Dùng làm bản nháp, tự rà soát và chỉnh lại đúng với quan sát thực tế trên bộ `G10` của mình | Có, đối chiếu với `SUBMISSION.md`, `RUBRIC.md` và các ảnh trong `G10` trên CVAT |
