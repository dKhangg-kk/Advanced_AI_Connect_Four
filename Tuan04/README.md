# Lab 04 — Constraint Satisfaction Problems (CSP)


## 1. Nội dung được giao

| Bài tập | Mô tả ngắn |
|---|---|
| Graph Coloring (CSP) | Cài đặt backtracking + heuristic (MRV, degree, LCV, forward checking) và min-conflicts; so sánh trên đồ thị ngẫu nhiên n=10,15,20,25 |
| N-Queens (Local Search — CSP context) | Cài đặt lại 3 biến thể HC, random restart, SA; so sánh mở rộng theo n; Advanced 4 toán tử |

> **Lưu ý:** `n_queens.ipynb` trong thư mục lab04 vẫn dùng đề **n-Queens Local Search** (không phải giải n-Queens bằng backtracking CSP). Đánh giá theo nội dung task thực tế trong file.


## 2. Bài làm

| File | Loại | Mô tả | Trạng thái |
|---|---|---|---|
| [`CSP_graph_coloring_example.ipynb`](CSP_graph_coloring_example.ipynb) | Notebook | Backtracking + MRV/LCV/FC + min-conflicts; thí nghiệm n=10–25 | Đủ task; chạy lại thành công |
| [`n_queens.ipynb`](n_queens.ipynb) | Notebook | HC, SA, random restart, Advanced; so sánh theo n | Đủ task; chạy lại thành công |
| [`baocao(lab04).docx`](baocao(lab04).docx) | Báo cáo | Báo cáo thực hành lab 04 | — |


## 3. Cách chạy

### Môi trường

| Notebook | Python | Kernel |
|---|---|---|
| `CSP_graph_coloring_example.ipynb` | 3.13.5 | CS7320-AI |
| `n_queens.ipynb` | 3.13.5 | `.venv (3.12.3)` |

> Khuyến nghị dùng **Python 3.10+** với Anaconda hoặc virtualenv.

### Thư viện cần cài

```bash
pip install numpy pandas matplotlib scipy
```

### Các bước chạy

```bash
cd lab04_csp_PhanLeNgocNhuY_3124720079
jupyter notebook
```

- Mở từng file `.ipynb` và chạy tất cả cell **từ đầu đến cuối** (Kernel → Restart & Run All).
- Dữ liệu đồ thị được sinh tự động bằng Delaunay triangulation (scipy) — không cần file ngoài.

> **Đã kiểm tra:** Cả hai notebook chạy lại thành công toàn bộ cell. `CSP_graph_coloring_example.ipynb` có `assert` kiểm tra complete/consistent ở mỗi nghiệm — tất cả pass.


## 4. Kết quả và nhận xét

### Graph Coloring (`CSP_graph_coloring_example.ipynb`)

| Thành phần | Cell | Kết quả |
|---|---|---|
| Variable ordering: MRV + degree heuristic | 12–13 | Giảm nhánh cần duyệt, đặc biệt ở n lớn |
| Value ordering: LCV | 12–13 | Ít bị kẹt hơn backtracking thuần |
| Forward checking | 12–13 | Phát hiện dead-end sớm |
| Min-conflicts (restart) | 22 | Nhanh hơn backtracking trên đồ thị dày |
| Thí nghiệm n=10,15,20,25 | 24–25 | 3 seed/kích thước; 3 và 4 màu; bảng thời gian + số bước; đã phân biệt "chạm giới hạn" với "vô nghiệm" |

**Nhận xét:**
- Backtracking + MRV/LCV/FC vượt backtracking cơ sở rõ rệt; min-conflicts nhanh nhất trên đồ thị thưa.
- **Điểm chưa khớp yêu cầu:** `steps` của min-conflicts tăng ở *mọi* vòng chọn/gán màu (kể cả giữ màu hoặc bước không cải thiện) → chưa đếm riêng số "uphill moves"/bước thực sự cải thiện. Cần bổ sung bộ đếm hoặc giải thích rõ khác biệt.
- **Hình cũ sai màu:** cell 17 dùng `list(res.values())[i]` — thứ tự gán của MRV khác thứ tự chỉ số đỉnh → màu vẽ có thể không khớp nghiệm. Cell 27 đã có hình đúng dùng `res[str(i)]`, nhưng hình cell 17 vẫn còn — cần xoá hoặc sửa để tránh hai hình mâu thuẫn.
- Thí nghiệm dừng ở n=25; nếu câu hỏi yêu cầu "tăng n lớn nhất có thể", nên thử thêm n=30,50 hoặc giải thích ngưỡng dừng.

### N-Queens (`n_queens.ipynb`)

| Task | Cell | Kết quả |
|---|---|---|
| Task 1–4: 3 biến thể HC + random restart | 14, 16, 19, 21 | Chạy đúng |
| Task 5: SA — geometric/linear cooling, biểu đồ trace | 23 | SA vượt HC ở n lớn |
| Task 6: 100 lần/thuật toán, n=4,8; hội tụ; log-log n=4,8,12,16,20 | 25, 27, 29 | Bảng sinh từ code đầy đủ; bảng Markdown ở cell 24 để trống nhưng bảng kết quả ngay sau đó |
| Advanced: 4 toán tử, 100 lần n=8,12; bảng/biểu đồ | 31 | Đủ nội dung và thảo luận |

**Vấn đề còn gặp:**
- **Task 6:** mô tả ghi "dùng cùng bàn cờ đầu vào trong mỗi trial", nhưng `_start` được sinh bên trong vòng lặp từng thuật toán → thực tế mỗi thuật toán nhận một tập bàn cờ khác nhau. Cần tạo tập bàn cờ một lần cho từng n rồi truyền vào, hoặc sửa mô tả để kết quả so sánh đáng tin cậy hơn.
- Cell 1 vẫn còn placeholder `[Add your name]`, `[list tools]`, `[your initials]` — cần điền trước khi nộp.
- Genetic Algorithm ở cell 33 là "not for credit" — để trống không phải thiếu task bắt buộc.


## 5. Phân công

| Thành viên | Phần việc thực tế |
|---|---|
| Bùi Quyền Kiệt | Tổng hợp, viết báo cáo (`baocao(lab04).docx`) |
| Phan Lê Ngọc Như Ý| Cài đặt backtracking + heuristic + min-conflicts; thí nghiệm; assert kiểm tra |
| Phạm Thái Duy Khang, Bùi Anh Đức | Cài đặt HC/SA, Task 6 so sánh mở rộng, Advanced 4 toán tử |
