# Báo cáo Day 14 — Lê Vĩnh Khải — 2A202603322

- Mã học viên dùng với `--student`: `2A202603322`
- `seed_tag` trong `frames_A.txt`: `82ac3100fd`

## 1. Dự đoán trước sweep (bước 5b)

Ghi **trước** khi chạy `scripts/pp_sweep.py`, rồi commit và push ngay (lịch sử commit là bằng chứng thời điểm viết). Không sửa phần này sau khi có kết quả.

- Tham số tôi nghĩ giảm công sửa nhiều nhất: tăng `score_thr`.
- Vì sao (nhìn ảnh BEV tập A: box thừa nhiều hay box sót nhiều?): trên tập A, box thừa khá nhiều và phải xóa tay rất nhiều (cấu hình gốc: xóa 48, thêm 16, sửa 7, chi phí 33.9). Box thừa chủ yếu nằm ở các hàng rào cây, bụi cây bên đường và bị model nhận nhầm thành Car hoặc Cyclist: ở những chỗ điểm LiDAR dày, model dễ đoán đó là vật thể. Các box thừa này thường có độ tin cậy thấp (trung vị score khoảng 0.35, trong khi box giữ lại có trung vị khoảng 0.88). Vì vậy khi tăng `score_thr`, các box có score thấp sẽ bị loại, từ đó bớt được box thừa và giảm số box phải xóa tay.

## 2. Tập A: sửa tay và tune

| Cấu hình | Xóa | Thêm | Sửa | Chi phí |
|---|---:|---:|---:|---:|
| Gốc | 48 | 16 | 7 | 33.9 |
| `best_config.json` | | | | |

- Tham số đã đổi trong `best_config.json`: ...
- Kết quả leave-one-out (dán các dòng `scripts/pp_sweep.py` in ra): ...
- Cấu hình có ổn định trên từng frame không? Vì sao tôi vẫn chọn (hoặc không chọn) nó: ...

## 3. Trước/sau (bước 8)

![so sánh](../../d14_2A202603322/compare/<frame>.jpg)

- `scripts/pp_compare.py` báo giảm (hoặc tăng) ...% công sửa trên tập A.
- Dự đoán ở mục 1 đúng hay sai? Giải thích bằng số box xóa/thêm/sửa: ...

## 4. Tập B

Số đo từ `scripts/pp_prelabel.py --frames d14_2A202603322/frames_B.txt --config d14_2A202603322/best_config.json --gt d14_2A202603322/ref_B.json`:

| Xóa | Thêm | Sửa | Chi phí |
|---:|---:|---:|---:|
| | | | |

- Loại box tốn công sửa nhất ở tập B: ...

## 5. Giới hạn

- Nêu ít nhất 2 giới hạn (ví dụ: chỉ 3 frame tune; model KITTI không có Truck/Bus; chi phí là công thức, chưa phải thời gian sửa thật): ...
