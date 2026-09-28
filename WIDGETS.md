# 📚 Cẩm Nang Chi Tiết Các Widget Được Sử Dụng Trong Dự Án

Tài liệu này tổng hợp toàn bộ các **Widget Flutter** được sử dụng trong màn hình **Profile UI** ([`lib/main.dart`](file:///d:/BT/APP/flutter_application_1/lib/main.dart)), giải thích chi tiết vai trò, vị trí và cách thức hoạt động của từng widget.

---

## 📑 Bảng Phân Loại Widget

| Nhóm | Các Widget sử dụng | Mục đích chính |
| :--- | :--- | :--- |
| **Cấu trúc & Nền tảng** | `MaterialApp`, `Scaffold`, `LayoutBuilder` | Định hình ứng dụng, hệ thống theme và responsive |
| **Bố cục (Layout)** | `Column`, `Row`, `Stack`, `Positioned`, `Wrap`, `Center`, `Expanded` | Sắp xếp vị trí các phần tử trên màn hình |
| **Kích thước & Khoảng cách**| `Container`, `SizedBox`, `Padding`, `Divider` | Định dạng lề (margin/padding), khoảng cách, vạch ngăn |
| **Hiển thị nội dung** | `Text`, `Icon`, `CircleAvatar`, `Image.network` | Hiển thị chữ, biểu tượng, ảnh đại diện, ảnh dự án |
| **Trang trí & Cắt xén** | `ClipRRect`, `BoxDecoration`, `LinearGradient` | Bo góc, làm khung viền, đổ bóng, chuyển sắc gradient |
| **Cuộn trang & Tương tác**| `SingleChildScrollView`, `IconButton`, `ScrollBehavior` | Cuộn lướt nội dung, nhận thao tác bấm chuột/chạm |

---

## 🔍 Chi Tiết Chức Năng Từng Widget

### 1. Nhóm Cấu trúc & Nền tảng (Core & App Structure)

#### `MaterialApp`
- **Chức năng:** Là widget gốc cấu hình toàn bộ ứng dụng theo chuẩn **Google Material Design 3**.
- **Vai trò trong dự án:**
  - Cấu hình giao diện sáng: `themeMode: ThemeMode.light` và `brightness: Brightness.light`.
  - Bật tính năng kéo chuột cuộn trang trên Web thông qua `scrollBehavior`.
  - Khai báo màn hình khởi chạy đầu tiên (`home: const MobileFrame(...)`).

#### `LayoutBuilder`
- **Chức năng:** Đọc thông số kích thước của màn hình/khung nhìn cha (`constraints.maxWidth`).
- **Vai trò trong dự án:** 
  - Tạo tính năng **Responsive thông minh**: Nếu màn hình `<= 500px` (như điện thoại thật), app sẽ hiển thị toàn màn hình. Nếu `> 500px` (như màn hình máy tính), app sẽ tự động bọc giao diện vào **Khung điện thoại giả lập (Mobile Mockup Frame)**.

#### `Scaffold`
- **Chức năng:** Tạo khung layout tiêu chuẩn cho màn hình (AppBar, Body, Background).
- **Vai trò trong dự án:**
  - Được dùng làm nền máy tính bên ngoài (`Scaffold(backgroundColor: Color(0xFFE2E8F0))`).
  - Được dùng làm khung chính của trang Profile (`ProfileScreen`), chứa thanh điều hướng `AppBar` và vùng nội dung `Body`.

---

### 2. Nhóm Bố cục (Layout Widgets)

#### `Column`
- **Chức năng:** Sắp xếp danh sách các widget con theo **chiều dọc** từ trên xuống dưới.
- **Vai trò trong dự án:**
  - Xếp tuần tự: Avatar & Tên ➔ Thẻ Stats ➔ About Me ➔ Skills ➔ Projects ➔ Contact Information.

#### `Row`
- **Chức năng:** Sắp xếp danh sách các widget con theo **chiều ngang** từ trái qua phải.
- **Vai trò trong dự án:**
  - Tạo 3 cột trong thẻ Thống kê (**148 Projects** | **9 Yrs Experience** | **4.9 ★ Rating**).
  - Ghép Icon và Chữ trong các thẻ kỹ năng (`Icon` + `Text`).
  - Xếp 2 thẻ dự án nằm song song cạnh nhau.
  - Xếp Icon, Chữ và Mũi tên điều hướng trong mục thông tin liên hệ.

#### `Stack` & `Positioned`
- **Chức năng:** 
  - `Stack`: Xếp các widget con đè chồng lên nhau theo trục Z (tạo hiệu ứng nhiều lớp).
  - `Positioned`: Đặt widget con vào vị trí chính xác (top, bottom, left, right).
- **Vai trò trong dự án:**
  - Đặt chiếc **Huy hiệu tích xanh (Verified badge)** đè lên góc dưới bên phải của Avatar ảnh đại diện.

#### `Wrap`
- **Chức năng:** Sắp xếp các widget con theo chiều ngang, tự động nhảy xuống dòng tiếp theo khi hàng bị đầy (khác với `Row` sẽ bị lỗi tràn màn hình).
- **Vai trò trong dự án:**
  - Dùng trong mục **Skills & Expertise** để xếp các thẻ kỹ năng (Flutter, Dart, Clean Arch, UI/UX, Firebase) tự động co giãn theo chiều ngang.

#### `Expanded`
- **Chức năng:** Buộc widget con giãn ra để chiếm trọn phần không gian còn trống trong `Row` hoặc `Column`.
- **Vai trò trong dự án:**
  - Chia đều 3 ô thông tin trong Thẻ thống kê (Stats card) theo tỷ lệ 1:1:1.
  - Chia đều 2 ô thẻ dự án trong hàng Featured Projects theo tỷ lệ 1:1.
  - Giúp chữ trong thẻ Contact giãn hết cỡ để đẩy icon mũi tên sang sát mép phải.

#### `Center`
- **Chức năng:** Căn giữa widget con bên trong nó cả theo chiều dọc lẫn chiều ngang.
- **Vai trò trong dự án:**
  - Căn giữa khung điện thoại trên màn hình máy tính.
  - Căn giữa cụm Avatar, Tên và Chức danh cá nhân.

---

### 3. Nhóm Kích thước, Đổ bóng & Trang trí (Decorations)

#### `Container`
- **Chức năng:** Widget đa năng nhất trong Flutter, kết hợp định kích thước (width/height), khoảng cách lề (margin/padding) và trang trí (`BoxDecoration`).
- **Vai trò trong dự án:**
  - **Khung điện thoại**: Đặt giới hạn `maxWidth: 410`, bo góc `46px`, viền kim loại xám và đổ bóng 3D chân thực.
  - **Viền Avatar Gradient**: Tạo dải chuyển màu cam - vàng xung quanh avatar (`LinearGradient`).
  - **Pill vị trí**: Tạo viên thuốc bo tròn nền xám chứa `📍 Tokyo, Japan`.
  - **Thẻ Stats, Thẻ Project, Thẻ Contact**: Tạo nền trắng bo góc viền nhẹ xám.

#### `ClipRRect`
- **Chức năng:** Cắt gọt (clip) widget con bên trong theo hình chữ nhật bo tròn các góc (`BorderRadius`).
- **Vai trò trong dự án:**
  - Cắt toàn bộ màn hình Profile theo khung bo góc của điện thoại (`borderRadius: 42`).
  - Bo tròn 2 góc trên của ảnh bìa dự án để ăn khớp với thẻ bài viết.

#### `SizedBox`
- **Chức năng:** Tạo một hộp vô hình có kích thước cố định để tạo khoảng cách giữa các widget.
- **Vai trò trong dự án:**
  - Tạo khoảng cách đệm dọc giữa các phần (ví dụ: `SizedBox(height: 24)`).
  - Tạo khoảng cách ngang giữa Icon và Chữ (ví dụ: `SizedBox(width: 6)`).

#### `Padding`
- **Chức năng:** Tạo khoảng trống đệm lùi vào bên trong cho widget con.
- **Vai trò trong dự án:**
  - Đệm lề xung quanh nút Back trên AppBar và khoảng cách nội dung các mục liên hệ.

#### `Divider`
- **Chức năng:** Vẽ một đường chỉ ngang mờ phân cách giữa các phần tử.
- **Vai trò trong dự án:**
  - Ngăn cách giữa 3 dòng thông tin (Contact Info, Email, Số điện thoại) trong thẻ liên hệ.

---

### 4. Nhóm Hiển thị Nội dung & Dữ liệu

#### `Text` & `TextStyle`
- **Chức năng:** Hiển thị văn bản, tuỳ biến font chữ, kích cỡ (`fontSize`), độ đậm (`fontWeight`), màu sắc (`color`), khoảng cách dòng (`height`), số dòng tối đa (`maxLines`) và hiệu ứng cắt chữ (`TextOverflow.ellipsis`).
- **Vai trò trong dự án:**
  - Hiển thị tên `Alex Rivers`, chức danh, đoạn văn bản `About Me`, các chỉ số số liệu và tên kỹ năng.

#### `Icon`
- **Chức năng:** Hiển thị biểu tượng vector từ bộ sưu tập Material Icons chuẩn của Google.
- **Vai trò trong dự án:**
  - `Icons.arrow_back_ios_new`: Mũi tên quay lại.
  - `Icons.share_outlined`: Nút chia sẻ.
  - `Icons.check`: Tích xanh xác nhận.
  - `Icons.star`: Ngôi sao đánh giá vàng.
  - `Icons.flutter_dash`, `Icons.code`, `Icons.layers_outlined`, `Icons.draw_outlined`, `Icons.local_fire_department_outlined`: Bộ icon cho các kỹ năng.
  - `Icons.alternate_email`, `Icons.mail_outline`, `Icons.phone_outlined`, `Icons.chevron_right`: Bộ icon thông tin liên hệ.

#### `CircleAvatar`
- **Chức năng:** Hiển thị ảnh đại diện cắt tròn sẵn với bán kính định trước (`radius: 54`).
- **Vai trò trong dự án:**
  - Hiển thị ảnh chân dung đại diện tải qua đường dẫn `NetworkImage`.

#### `Image.network`
- **Chức năng:** Tải và hiển thị ảnh trực tiếp từ đường link URL Internet.
- **Vai trò trong dự án:**
  - Hiển thị ảnh bìa cho 2 dự án nổi bật (*E-Shop Flutter* & *Crypto Vault*).
  - Có sẵn `errorBuilder` để hiển thị khung màu xám dự phòng khi mất kết nối mạng.

---

### 5. Nhóm Cuộn trang & Tương tác (Interactivity & Scrolling)

#### `SingleChildScrollView`
- **Chức năng:** Cho phép toàn bộ vùng nội dung bên trong có thể cuộn lướt theo chiều dọc khi chiều cao vượt quá màn hình điện thoại.
- **Vai trò trong dự án:**
  - Đảm bảo ứng dụng chạy trơn tru trên mọi độ phân giải màn hình mà không bao giờ bị lỗi tràn viền vàng đen (`RenderFlex overflowed`).

#### `IconButton`
- **Chức năng:** Nút bấm chứa biểu tượng có hiệu ứng gợn sóng khi chạm/click.
- **Vai trò trong dự án:**
  - Nút Back ở góc trái trên và Nút Share ở góc phải trên thanh AppBar.

#### `ScrollBehavior` (với `dragDevices`)
- **Chức năng:** Cấu hình hành vi cuộn chuột và cảm ứng cho toàn ứng dụng.
- **Vai trò trong dự án:**
  - Cho phép người dùng máy tính dùng **chuột kéo giữ và vuốt màn hình** tương tự như lướt ngón tay trên điện thoại thật.
