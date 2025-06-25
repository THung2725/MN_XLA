# Nhập Môn Xử Lý Ảnh Số - Lab 4

## Phân Vùng Ảnh
**Sinh Viên Thực Hiên:** Phạm Thế Hùng  **MSSV:** 2374802010164
**Môn Học:** Nhập Môn Xử Lý Ảnh Số
**Giảng viên:** Đỗ Hữu Quân

## Giới Thiệu:


## Công nghệ sử dụng

## Chi tiết phương pháp & công thức

### 1. Phương pháp phân ngưỡng Otsu (Otsu's Thresholding)

**Mục đích:**  
- Tự động tìm giá trị ngưỡng tối ưu để phân chia ảnh thành hai lớp: foreground và background
- Tối đa hóa phương sai giữa các lớp 
- Tối thiểu hóa phương sai trong lớp
**Công thức toán học:**  
```math
\sigma_b^2(t) = \omega_1(t) \cdot \omega_2(t) \cdot [\mu_1(t) - \mu_2(t)]^2
```

- \omega_1(t), \omega_2(t): xác suất xuất hiện của hai lớp
- \mu_1(t), \mu_2(t): giá trị trung bình của hai lớp

**Ví dụ:**  
- Ảnh có histogram với 2 đỉnh rõ ràng, Otsu sẽ tìm ngưỡng ở giữa 2 đỉnh này

**Code chính:**  
```python
data = Image.open("moon.jpg").convert("L")
a = np.array(data)
thres = threshold_otsu(a)
b = a > thres
```


