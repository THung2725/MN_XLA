# Nhập Môn Xử Lý Ảnh Số - Lab 4

## Phân Vùng Ảnh
**Sinh Viên Thực Hiên:** Phạm Thế Hùng  **MSSV:** 2374802010164
**Môn Học:** Nhập Môn Xử Lý Ảnh Số
**Giảng viên:** Đỗ Hữu Quân

## Giới Thiệu:


## Công nghệ sử dụng
- **Python:** Ngôn ngữ chính
- **numpy:** Xử lý ảnh dưới dạng mảng số học
- **scipy:**  giải quyết các bài toán kỹ thuật và toán học phức tạp
- **skimage:** xử lý và phân tích hình ảnh
- **ImageIO:** Đọc file ảnh với định dạng hiện đại
- **Matplotlib:** Hiển thị ảnh trực quan
## Chi tiết các phép biến đổi & công thức

### 1. Phương pháp Otsu

**Mục đích:**  
- Tự động tìm giá trị ngưỡng tối ưu để phân chia ảnh thành hai lớp: foreground và background
- Tối đa hóa phương sai giữa các lớp 
- Tối thiểu hóa phương sai trong lớp
**Công thức toán học:**  
```math
\sigma_b^2(t) = \omega_1(t) \cdot \omega_2(t) \cdot [\mu_1(t) - \mu_2(t)]^2
```
**Ví dụ:**  
- Ảnh có histogram với 2 đỉnh rõ ràng, Otsu sẽ tìm ngưỡng ở giữa 2 đỉnh này

**Code chính:**  
```python
data = Image.open('moon.jpg').convert('L')
a = np.array(data)
thres = threshold_otsu(a)
b = a > thres
b = Image.fromarray(b)
```
### 2. Phương pháp Adaptive Thesholding
**Mục địch**
- phân ngưỡng thích nghi được sử dụng để chuyển ảnh xám thành ảnh nhị phân trong các trường hợp ánh sáng không đồng đều

**Nguyên lý**
- chia ảnh thành các vùng nhỏ sau đó tính ngưỡng riêng của mỗi vùng rôi đem so sanh từng điểm ảnh với ngưỡng của vùng nếu mà sáng hơn ngưỡng thì thành trắng nếu không thì thành màu đen

**Code chính**
```python
data = Image.open('moon.jpg').convert('L')
a = np.array(data)
thres = threshold_otsu(a)
b = threshold_local(a, 39, offset=10)
b = Image.fromarray(b)
```

### 3.Phân vùng theo region
**Mục địch**
Phân theo vùng chia ảnh thành các khu vực mà các điểm ảnh giống nhau về độ sáng hoặc màu sắc. Mục đích chính là tách vật thể ra khỏi nền để xử lý hoặc phân tích dễ dàng hơn.

**Nguyên lý**
Chuyển ảnh sang ảnh xám để dễ xử lý ảnh và nhị phân hóa bằng Otsu để tách nền và đối tượng, giảm nhiễu và tách rời các vùng gần nhau khoảng cách của cá điểm ảnh. Tính khoảng cách từ mỗi điểm ảnh nền đến điểm ảnh gần nhất thuộc đối tượng tạo các vùng cho thuật toán phân vùng

**Code chính**
```python
data = cv2.imread('moon.jpg')
a = cv2.cvtColor(data, cv2.COLOR_BGR2GRAY)
thresh, b1 = cv2.threshold(a, 0, 255, cv2.THRESH_BINARY_INV + cv2.THRESH_OTSU)
b2 = cv2.erode(b1, None, iterations = 2)
dist_trans = cv2.distanceTransform(b2, 2, 3)
thresh, dt = cv2.threshold(dist_trans, 1, 255, cv2.THRESH_BINARY)
labelled, ncc = label(dt)
labelled = labelled.astype(np.int32)
cv2.watershed(data, labelled)
b = Image.fromarray(labelled)
```