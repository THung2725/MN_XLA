# THỰC HÀNH 3: BIẾN ĐỔI HÌNH HỌC


## 2. BÀI TẬP
### Bài tập 1: Viết chương trình chọn quả kiwi từ ảnh colorfull-ripe-tropical-fruit.jpg trong thư mục exercise. Tịnh tiến quả kiwi sang 30 pixel

### CÔNG NGHỆ SỬ DỤNG
* Gồm các thư viện:
- **numpy**: Xử lý toán học với mảng 
- **SciPy**: Tính toán khoa học
- **imageio**: Đọc và ghi ảnh
- **matplotlib.pyplot**: Hiển thị ảnh và biểu đồ
### THUẬT TOÁN SỬ DỤNG
- Bài này dung ndimage.shift() từ thư viện sciPy, cho phép dịch chuyển một ảnh theo trục x, y. Với yêu cầu bài ảnh được tịnh tiến sang phải 30 pixel 
### GIẢI THÍCH HOẠT ĐỘNG

```python
data = iio.imread("exercise/colorful-ripe-tropical-fruits.jpg")
```
* Đọc ảnh từ thư mục exercise để tiến hành chọn ra ảnh kiwi trong tất cả các loại hoa qua trong bức hình 

```python
bmg = data[920:1100, 390:570]
```
* Cắt ảnh để được quả kiwi, để cắt được thì tọa độ y từ 920-1100, tọa độ x từ 390-570

```python
bdata = nd.shift(bmg, (0, 30, 0))
```
* Sử dụng thuật toán của thư viện scipy.ndimage.shift để tịnh tiến ảnh kiwi đã cắt được sang bên phải 30px. 
- 0 đầu tiên là trục y và có nghĩa là ảnh không di chuyển lên hoặc xuống và điều này đúng với yêu cầu của bài
- 30 là trục x và có nghĩa là ảnh sẽ di chuyển qua bên phải 30px nếu và ngược lại dịch chuyển qua trái sẽ có giá trị là âm
- 0 cuối cùng là kênh màu và ở đây để 0 là để không thay đổi màu của ảnh

```python
print(data.shape)
```
* In ra kích thước của ảnh gốc ban đầu chưa cắt

```python
iio.imsave("kiwi.jpg", bdata)
```
* Lưu ảnh sau khi cắt và đã được tịnh tiến với tên là kiwi.jpg

```python
plt.imshow(bdata)
plt.show()
```
* Cuối cùng hiển thị kết quả ra màn hình trên cửa sổ popup
