# IAP Solver — Hệ Thống Giải Toán Phân Công Giám Thị

Hệ thống tối ưu hóa phân công giám thị coi thi (Invigilator Assignment Problem) sử dụng mô hình **Integer Linear Programming (ILP)** với bộ giải PuLP/CBC.

## Yêu Cầu Hệ Thống

- **Python**: `3.12.x` (khuyến nghị 3.12.8 — phiên bản phát triển gốc)
- **Hệ điều hành**: Windows 10/11, macOS, hoặc Linux

## Hướng Dẫn Cài Đặt & Chạy Code

### Bước 1: Tải project về

```bash
git clone <repository-url>
cd MHH
```

### Bước 2: Tạo Virtual Environment

**Windows (PowerShell):**
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

**Windows (Command Prompt):**
```cmd
python -m venv venv
.\venv\Scripts\activate.bat
```

**macOS / Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

>  **Lưu ý PowerShell**: Nếu gặp lỗi "cannot be loaded because running scripts is disabled", chạy lệnh sau với quyền **Administrator**:
> ```powershell
> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
> ```

### Bước 3: Cài đặt thư viện

```bash
pip install -r requirements.txt
```

### Bước 4: Chạy chương trình

```bash
python IAP_Solver.py
```

> **Quan trọng**: File dữ liệu `Dataset_Anonymized_Invigilator_Assignment_Problem.xlsx` phải nằm **cùng thư mục** với `IAP_Solver.py`.

## Thư Viện Sử Dụng

| Thư viện | Phiên bản | Mô tả |
|----------|-----------|-------|
| `pandas` | 3.0.3 | Đọc & xử lý dữ liệu Excel |
| `numpy` | 2.4.6 | Tính toán thống kê |
| `pulp` | 3.3.1 | Bộ giải quy hoạch tuyến tính nguyên (ILP) |
| `openpyxl` | 3.1.5 | Engine đọc file .xlsx cho pandas |

## Cấu Trúc Project

```
MHH/
├── IAP_Solver.py            # File chính — chạy toàn bộ hệ thống
├── Dataset_Anonymized_...   # File dữ liệu đầu vào (.xlsx)
├── requirements.txt         # Danh sách thư viện cần cài
├── .gitignore               # Bỏ qua venv, cache khi push git
└── README.md                # File hướng dẫn này
```

## Xử Lý Sự Cố Thường Gặp

### Lỗi `ModuleNotFoundError`
Đảm bảo bạn đã kích hoạt venv trước khi chạy:
```bash
# Kiểm tra đang dùng Python nào
python --version
pip list
```

### Lỗi encoding tiếng Việt
Code đã xử lý tự động cho Windows. Nếu vẫn gặp lỗi, chạy với:
```bash
python -X utf8 IAP_Solver.py
```

### Lỗi đọc file Excel
- Kiểm tra tên file chính xác: `Dataset_Anonymized_Invigilator_Assignment_Problem.xlsx`
- Đảm bảo file nằm cùng thư mục với `IAP_Solver.py`
- Thử chạy `pip install openpyxl` riêng nếu pandas báo lỗi engine

## Chức Năng Chính

1. **Requirement 7**: Giải mô hình ILP gốc — phân công tối ưu với ràng buộc trùng ca, vượt tải, sở thích cơ sở
2. **Requirement 8**: Weight Tuning & Relaxation — khảo sát trọng số Alpha/Beta trên biên Pareto + tự động nới lỏng khi Infeasible
3. **Requirement 9**: Performance Benchmark — so sánh định lượng lịch thủ công (Baseline) vs mô hình ILP tối ưu
