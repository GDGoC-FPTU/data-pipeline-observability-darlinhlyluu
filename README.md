[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23573981&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student ID:** 2A202600119  
**Name:** Lưu Linh Ly

---

## Mô tả

Lab này yêu cầu xây dựng một ETL pipeline đơn giản để đọc dữ liệu JSON, kiểm tra chất lượng dữ liệu, biến đổi dữ liệu theo business logic và lưu kết quả ra file CSV. Bên cạnh phần pipeline, bài lab còn mô phỏng tác động của chất lượng dữ liệu đến AI Agent bằng cách so sánh kết quả trả lời khi agent dùng dữ liệu sạch và dữ liệu rác.

Trong bài làm này, tôi đã:
- Hoàn thiện đầy đủ các hàm `extract`, `validate`, `transform`, `load` trong `solution.py`
- Loại bỏ các record không hợp lệ có `price <= 0` hoặc `category` rỗng
- Thêm trường `discounted_price` và `processed_at`
- Chuẩn hóa cột `category` sang Title Case
- Chạy stress test với `processed_data.csv` và `garbage_data.csv`

---

## Cách chạy (How to Run)

### Yêu cầu trước khi chạy

```bash
pip install pandas pytest
```

### Chạy ETL Pipeline

```bash
python solution.py
```

Lệnh trên sẽ:
- Đọc dữ liệu từ `raw_data.json`
- Loại bỏ dữ liệu lỗi
- Tạo file `processed_data.csv`

### Chạy Stress Test với Agent

```bash
python generate_garbage.py
python agent_simulation.py
```

Lệnh đầu tạo file `garbage_data.csv` chứa các lỗi data quality phổ biến.  
Lệnh thứ hai so sánh phản hồi của agent khi dùng:
- `processed_data.csv` (clean data)
- `garbage_data.csv` (garbage data)

### Chạy bộ test autograder tại máy

```bash
python -m pytest tests/test_autograder.py -v
```

---

## Cấu trúc thư mục

```text
.
|-- solution.py
|-- raw_data.json
|-- processed_data.csv
|-- generate_garbage.py
|-- agent_simulation.py
|-- experiment_report.md
|-- README.md
`-- tests/
    `-- test_autograder.py
```

---

## Kết quả

Sau khi chạy pipeline:
- Tổng số record đầu vào: 5
- Số record hợp lệ được giữ lại: 3
- Số record bị loại: 2

Ba record hợp lệ trong `processed_data.csv` là:
- Laptop - Electronics - 1200.0 - discounted_price 1080.0
- Chair - Furniture - 45.0 - discounted_price 40.5
- Monitor - Electronics - 300.0 - discounted_price 270.0

Tất cả test local đều đạt:

```bash
python -m pytest tests/test_autograder.py -v
```

Kết quả: `9 passed`
