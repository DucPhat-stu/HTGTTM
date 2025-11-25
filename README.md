# Hệ Thống Nhận Diện Biển Báo Giao Thông Thông Minh

Ứng dụng web (Flask + YOLOv8) nhận diện biển báo, đọc cấu hình nhóm biển cấm trực tiếp từ `data.yaml`, và hiển thị thống kê trực quan phục vụ thuyết trình.

## Yêu cầu

- Python ≥ 3.8
- pip, Git
- Webcam (tùy chọn – để trình diễn realtime)

##  Cài đặt nhanh

```bash
git clone https://github.com/trongphuccute/hethonggiaothongthongminh
cd C:\hethonggiaothongthongminh-main\HeThongGiaoThongThongMinh\src-main
python -m venv venv
venv\Scripts\activate  # hoặc source venv/bin/activate
pip install -r ../../requirements.txt
python app.py
```

Ứng dụng mở tại http://localhost:5000 – chuyển tới `/nhandien` để bắt đầu demo.

## Sử dụng

- **Upload ảnh/video**: nhấn “Tải Ảnh Lên” hoặc “Tải Video Lên”. Ảnh kết quả sẽ hiển thị cùng bảng **Phân tích biển cấm** (chỉ tính các nhãn nằm trong `data.yaml`).
- **Camera laptop**: nhấn “Mở Camera”, YOLO xử lý từng frame, camera tự tắt sau 2 phút nếu không thao tác, và bảng phân tích cập nhật liên tục. Thao tác `F12 → Console` để xem log `[CAMERA]`.
- **Thống kê**: dữ liệu phân loại dựa trên `backend/data.yaml` (trường `names`). Chỉ cần chỉnh sửa file YAML này để thêm/bớt nhóm hoặc cập nhật tên.

##  Cấu hình

| Thành phần | Vai trò | Ghi chú |
| --- | --- | --- |
| `CAMERA_ANALYSIS_INTERVAL` | Số frame giữa các lần cập nhật thống kê | Giá trị nhỏ → cập nhật nhanh hơn |
| `CAMERA_STREAM_TIMEOUT` | Tự tắt camera sau X giây không thao tác | Mặc định 120 |
| `DATA_YAML_PATH` | Đường dẫn tới `data.yaml` | Mặc định dùng file trong thư mục `backend` |

##  Cấu trúc gọn

```
app.py                  # Flask + xử lý nhận diện YOLO
templates/nhandien.html # UI nhận diện + bảng phân tích
static/assets/img       # Bộ ảnh demo
HeThong.../backend/data.yaml  # Nơi chỉnh tên & nhóm biển báo
```

##  Tính năng nổi bật

- Nhận diện biển báo chính xác bằng YOLOv8.
- Phân loại biển cấm dựa trên `data.yaml`, dễ tinh chỉnh nhóm.
- Streaming webcam + log DevTools để dễ mô tả khi thuyết trình.
- Camera tự tắt sau 2 phút nếu treo, đảm bảo tiết kiệm tài nguyên khi demo.
- Các trang kiến thức/quiz/luật giữ nguyên để hỗ trợ trình bày nội dung lý thuyết.

##  Ghi chú thực hành

- Luôn giữ lại vài ảnh kết quả trong `static/results/` (hoặc `runs/detect/predict_demo`) để minh họa nhanh nếu không có mạng/camera.
- Nếu thay template mới, nhớ khởi động lại ứng dụng để nạp lại cấu hình.
- Khi cần demo trên máy khác, chỉ cần copy dự án, `pip install -r requirements.txt`, bật server và dùng camera/ảnh có sẵn.

---