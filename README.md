# 📱 Flutter Profile Screen UI (Light Theme & Auto Mobile Frame)

Giao diện hồ sơ cá nhân (**Profile Screen**) hiện đại, chuẩn UI/UX được xây dựng bằng **Flutter & Material 3** với chế độ giao diện sáng (**Theme: Light**) và **tự động đóng khung điện thoại (Mobile Frame Mockup)** khi mở trên Web/Desktop mà không cần bấm F12 hay chuyển chế độ thủ công!

---

## 🎨 Điểm nổi bật & Cấu trúc Giao diện

- **Auto Mobile Frame**: Khi chạy trên trình duyệt Web (Chrome/Edge) hoặc màn hình máy tính lớn (> 500px), ứng dụng tự động hiển thị trong một **chiếc khung điện thoại bo góc chuẩn (~410px)** có viền kim loại và hiệu ứng đổ bóng 3D chân thực (giống ảnh mẫu).
- **Hỗ trợ cuộn chuột & cảm ứng mượt mà**: Tích hợp `scrollBehavior` hỗ trợ kéo vuốt bằng chuột (`mouse drag`) y như vuốt màn hình cảm ứng trên điện thoại.
- **Theme**: `ThemeMode.light` với `Brightness.light`, nền sáng dịu mắt (`#F8FAFC`), bảng màu chủ đạo xanh dương hiện đại (`#2563EB`).
- **AppBar**: Nút quay lại (Back) bo góc, tiêu đề *Profile* căn giữa in đậm và nút chia sẻ (*Share*).
- **Profile Header**: 
  - Avatar bo tròn viền gradient màu cam - vàng nổi bật.
  - Tích xanh xác minh danh tính (*Verified badge*).
  - Tên nhân sự (*Alex Rivers*), chức danh (*Lead Mobile Engineer*) và địa điểm (*📍 Tokyo, Japan*).
- **Thống kê (Stats Card)**: 3 chỉ số chính (*148 Projects*, *9 Yrs Experience*, *4.9 ★ Rating*) trong khung thẻ bo tròn tinh tế.
- **Giới thiệu (About Me)**: Đoạn tóm tắt giới thiệu chuyên môn với khoảng cách dòng chuẩn tỉ lệ.
- **Kỹ năng (Skills & Expertise)**: Các chip màu sắc riêng biệt kèm biểu tượng:
  - 🔷 `Flutter`
  - 🟢 `Dart`
  - 🔴 `Clean Arch`
  - 🟣 `UI/UX`
  - 🟡 `Firebase`
- **Dự án nổi bật (Featured Projects)**: Lưới 2 thẻ dự án bo góc kèm hình ảnh trực quan (*E-Shop Flutter* & *Crypto Vault*).
- **Thông tin liên hệ (Contact Information)**: Danh sách thẻ liên hệ trực quan (*Email*, *Số điện thoại*) có mũi tên điều hướng.

---

## 💻 Toàn bộ Mã nguồn (lib/main.dart)

```dart
import 'dart:ui';
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Profile UI',
      // Cho phép kéo vuốt cuộn trang bằng cả chuột lẫn cảm ứng
      scrollBehavior: const MaterialScrollBehavior().copyWith(
        dragDevices: {
          PointerDeviceKind.mouse,
          PointerDeviceKind.touch,
          PointerDeviceKind.trackpad,
        },
      ),
      themeMode: ThemeMode.light,
      theme: ThemeData(
        brightness: Brightness.light,
        scaffoldBackgroundColor: const Color(0xFFF8FAFC),
        colorScheme: ColorScheme.fromSeed(
          seedColor: const Color(0xFF2563EB),
          brightness: Brightness.light,
        ),
        useMaterial3: true,
      ),
      // Tự động bọc trong khung điện thoại khi mở trên Web/Desktop
      home: const MobileFrame(child: ProfileScreen()),
    );
  }
}

/// Khung giả lập điện thoại tự động hiển thị trên Web / Desktop
class MobileFrame extends StatelessWidget {
  final Widget child;
  const MobileFrame({super.key, required this.child});

  @override
  Widget build(BuildContext context) {
    return LayoutBuilder(
      builder: (context, constraints) {
        // Nếu màn hình nhỏ (<= 500px như điện thoại thật), hiển thị toàn màn hình bình thường
        if (constraints.maxWidth <= 500) {
          return child;
        }

        // Trên máy tính / trình duyệt web: hiển thị sẵn khung điện thoại ở giữa màn hình
        return Scaffold(
          backgroundColor: const Color(0xFFE2E8F0),
          body: Center(
            child: Container(
              margin: const EdgeInsets.symmetric(vertical: 20, horizontal: 16),
              constraints: const BoxConstraints(
                maxWidth: 410,
                maxHeight: 880,
              ),
              decoration: BoxDecoration(
                color: Colors.white,
                borderRadius: BorderRadius.circular(46),
                border: Border.all(
                  color: const Color(0xFF94A3B8),
                  width: 4,
                ),
                boxShadow: [
                  BoxShadow(
                    color: Colors.black.withValues(alpha: 0.15),
                    blurRadius: 30,
                    spreadRadius: 2,
                    offset: const Offset(0, 12),
                  ),
                ],
              ),
              child: ClipRRect(
                borderRadius: BorderRadius.circular(42),
                child: child,
              ),
            ),
          ),
        );
      },
    );
  }
}

class ProfileScreen extends StatelessWidget {
  const ProfileScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: const Color(0xFFF8FAFC),
      appBar: AppBar(
        backgroundColor: Colors.transparent,
        elevation: 0,
        scrolledUnderElevation: 0,
        leading: Padding(
          padding: const EdgeInsets.all(8.0),
          child: Container(
            decoration: BoxDecoration(
              border: Border.all(color: Colors.grey.shade300),
              borderRadius: BorderRadius.circular(10),
            ),
            child: IconButton(
              padding: EdgeInsets.zero,
              icon: const Icon(Icons.arrow_back_ios_new, size: 16, color: Colors.black87),
              onPressed: () {},
            ),
          ),
        ),
        centerTitle: true,
        title: const Text(
          'Profile',
          style: TextStyle(
            fontWeight: FontWeight.bold,
            fontSize: 18,
            color: Colors.black87,
          ),
        ),
        actions: [
          IconButton(
            icon: const Icon(Icons.share_outlined, color: Colors.black87),
            onPressed: () {},
          ),
          const SizedBox(width: 8),
        ],
      ),
      body: SingleChildScrollView(
        padding: const EdgeInsets.symmetric(horizontal: 20, vertical: 12),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            // Avatar & Info
            Center(
              child: Column(
                children: [
                  Stack(
                    children: [
                      Container(
                        padding: const EdgeInsets.all(3.5),
                        decoration: const BoxDecoration(
                          shape: BoxShape.circle,
                          gradient: LinearGradient(
                            colors: [Color(0xFFF97316), Color(0xFFFB923C), Color(0xFFFBBF24)],
                            begin: Alignment.topLeft,
                            end: Alignment.bottomRight,
                          ),
                        ),
                        child: const CircleAvatar(
                          radius: 54,
                          backgroundImage: NetworkImage(
                            'https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=400&auto=format&fit=crop&q=80',
                          ),
                        ),
                      ),
                      Positioned(
                        bottom: 4,
                        right: 4,
                        child: Container(
                          padding: const EdgeInsets.all(4),
                          decoration: BoxDecoration(
                            color: const Color(0xFF2563EB),
                            shape: BoxShape.circle,
                            border: Border.all(color: Colors.white, width: 2),
                          ),
                          child: const Icon(
                            Icons.check,
                            size: 14,
                            color: Colors.white,
                          ),
                        ),
                      ),
                    ],
                  ),
                  const SizedBox(height: 14),
                  const Text(
                    'Alex Rivers',
                    style: TextStyle(
                      fontSize: 22,
                      fontWeight: FontWeight.bold,
                      color: Color(0xFF0F172A),
                    ),
                  ),
                  const SizedBox(height: 4),
                  Text(
                    'Lead Mobile Engineer',
                    style: TextStyle(
                      fontSize: 14,
                      color: Colors.grey.shade600,
                      fontWeight: FontWeight.w500,
                    ),
                  ),
                  const SizedBox(height: 10),
                  Container(
                    padding: const EdgeInsets.symmetric(horizontal: 12, vertical: 6),
                    decoration: BoxDecoration(
                      color: Colors.grey.shade100,
                      borderRadius: BorderRadius.circular(20),
                      border: Border.all(color: Colors.grey.shade200),
                    ),
                    child: Row(
                      mainAxisSize: MainAxisSize.min,
                      children: [
                        Icon(Icons.location_on_outlined, size: 15, color: Colors.grey.shade600),
                        const SizedBox(width: 4),
                        Text(
                          'Tokyo, Japan',
                          style: TextStyle(
                            fontSize: 12,
                            color: Colors.grey.shade700,
                            fontWeight: FontWeight.w500,
                          ),
                        ),
                      ],
                    ),
                  ),
                ],
              ),
            ),

            const SizedBox(height: 20),

            // Stats Card
            Container(
              padding: const EdgeInsets.symmetric(vertical: 16),
              decoration: BoxDecoration(
                color: Colors.white,
                borderRadius: BorderRadius.circular(16),
                border: Border.all(color: Colors.grey.shade200),
                boxShadow: [
                  BoxShadow(
                    color: Colors.black.withValues(alpha: 0.02),
                    blurRadius: 10,
                    offset: const Offset(0, 4),
                  ),
                ],
              ),
              child: Row(
                children: [
                  Expanded(
                    child: _buildStatItem('148', 'Projects'),
                  ),
                  Container(height: 32, width: 1, color: Colors.grey.shade200),
                  Expanded(
                    child: _buildStatItem('9 Yrs', 'Experience'),
                  ),
                  Container(height: 32, width: 1, color: Colors.grey.shade200),
                  Expanded(
                    child: _buildStatItem(
                      '4.9',
                      'Rating',
                      trailingIcon: const Icon(Icons.star, color: Color(0xFFFBBF24), size: 18),
                    ),
                  ),
                ],
              ),
            ),

            const SizedBox(height: 24),

            // About Me
            const Text(
              'About Me',
              style: TextStyle(
                fontSize: 16,
                fontWeight: FontWeight.bold,
                color: Color(0xFF0F172A),
              ),
            ),
            const SizedBox(height: 8),
            Text(
              'Passionate Lead Mobile Engineer specialized in Flutter, Dart, and building high-performance cross-platform applications. Focused on elegant...',
              style: TextStyle(
                fontSize: 13.5,
                color: Colors.grey.shade600,
                height: 1.5,
              ),
            ),

            const SizedBox(height: 24),

            // Skills & Expertise
            const Text(
              'Skills & Expertise',
              style: TextStyle(
                fontSize: 16,
                fontWeight: FontWeight.bold,
                color: Color(0xFF0F172A),
              ),
            ),
            const SizedBox(height: 12),
            Wrap(
              spacing: 8,
              runSpacing: 10,
              children: [
                _buildSkillChip(
                  icon: Icons.flutter_dash,
                  label: 'Flutter',
                  bgColor: const Color(0xFFE0F2FE),
                  textColor: const Color(0xFF0284C7),
                ),
                _buildSkillChip(
                  icon: Icons.code,
                  label: 'Dart',
                  bgColor: const Color(0xFFDCFCE7),
                  textColor: const Color(0xFF16A34A),
                ),
                _buildSkillChip(
                  icon: Icons.layers_outlined,
                  label: 'Clean Arch',
                  bgColor: const Color(0xFFFFE4E6),
                  textColor: const Color(0xFFE11D48),
                ),
                _buildSkillChip(
                  icon: Icons.draw_outlined,
                  label: 'UI/UX',
                  bgColor: const Color(0xFFF3E8FF),
                  textColor: const Color(0xFF9333EA),
                ),
                _buildSkillChip(
                  icon: Icons.local_fire_department_outlined,
                  label: 'Firebase',
                  bgColor: const Color(0xFFFEF3C7),
                  textColor: const Color(0xFFD97706),
                ),
              ],
            ),

            const SizedBox(height: 24),

            // Featured Projects
            const Text(
              'Featured Projects',
              style: TextStyle(
                fontSize: 16,
                fontWeight: FontWeight.bold,
                color: Color(0xFF0F172A),
              ),
            ),
            const SizedBox(height: 12),
            Row(
              children: [
                Expanded(
                  child: _buildProjectCard(
                    imageUrl: 'https://images.unsplash.com/photo-1557821552-17105176677c?w=500&auto=format&fit=crop&q=80',
                    title: 'E-Shop Flutter',
                    subtitle: 'Mobile App • 2026',
                  ),
                ),
                const SizedBox(width: 14),
                Expanded(
                  child: _buildProjectCard(
                    imageUrl: 'https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?w=500&auto=format&fit=crop&q=80',
                    title: 'Crypto Vault',
                    subtitle: 'Finance • Clean Arch',
                  ),
                ),
              ],
            ),

            const SizedBox(height: 24),

            // Contact Information
            Container(
              decoration: BoxDecoration(
                color: Colors.white,
                borderRadius: BorderRadius.circular(16),
                border: Border.all(color: Colors.grey.shade200),
              ),
              child: Column(
                children: [
                  _buildContactItem(
                    icon: Icons.alternate_email,
                    title: 'Contact Information',
                    isHeader: true,
                  ),
                  Divider(height: 1, color: Colors.grey.shade100),
                  _buildContactItem(
                    icon: Icons.mail_outline,
                    title: 'alex.rivers@email.com',
                  ),
                  Divider(height: 1, color: Colors.grey.shade100),
                  _buildContactItem(
                    icon: Icons.phone_outlined,
                    title: '+81 (90) 1234-5678',
                  ),
                ],
              ),
            ),

            const SizedBox(height: 30),
          ],
        ),
      ),
    );
  }

  Widget _buildStatItem(String value, String label, {Widget? trailingIcon}) {
    return Column(
      children: [
        Row(
          mainAxisAlignment: MainAxisAlignment.center,
          mainAxisSize: MainAxisSize.min,
          children: [
            Text(
              value,
              style: const TextStyle(
                fontSize: 17,
                fontWeight: FontWeight.bold,
                color: Color(0xFF0F172A),
              ),
            ),
            if (trailingIcon != null) ...[
              const SizedBox(width: 3),
              trailingIcon,
            ],
          ],
        ),
        const SizedBox(height: 4),
        Text(
          label,
          style: TextStyle(
            fontSize: 12,
            color: Colors.grey.shade500,
            fontWeight: FontWeight.w500,
          ),
        ),
      ],
    );
  }

  Widget _buildSkillChip({
    required IconData icon,
    required String label,
    required Color bgColor,
    required Color textColor,
  }) {
    return Container(
      padding: const EdgeInsets.symmetric(horizontal: 12, vertical: 7),
      decoration: BoxDecoration(
        color: bgColor,
        borderRadius: BorderRadius.circular(12),
      ),
      child: Row(
        mainAxisSize: MainAxisSize.min,
        children: [
          Icon(icon, size: 15, color: textColor),
          const SizedBox(width: 6),
          Text(
            label,
            style: TextStyle(
              fontSize: 12.5,
              fontWeight: FontWeight.w600,
              color: textColor,
            ),
          ),
        ],
      ),
    );
  }

  Widget _buildProjectCard({
    required String imageUrl,
    required String title,
    required String subtitle,
  }) {
    return Container(
      decoration: BoxDecoration(
        color: Colors.white,
        borderRadius: BorderRadius.circular(16),
        border: Border.all(color: Colors.grey.shade200),
      ),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          ClipRRect(
            borderRadius: const BorderRadius.vertical(top: Radius.circular(15)),
            child: Image.network(
              imageUrl,
              height: 90,
              width: double.infinity,
              fit: BoxFit.cover,
              errorBuilder: (context, error, stackTrace) => Container(
                height: 90,
                color: Colors.grey.shade200,
                child: const Icon(Icons.image, color: Colors.grey),
              ),
            ),
          ),
          Padding(
            padding: const EdgeInsets.all(10),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Text(
                  title,
                  style: const TextStyle(
                    fontSize: 13,
                    fontWeight: FontWeight.bold,
                    color: Color(0xFF0F172A),
                  ),
                  maxLines: 1,
                  overflow: TextOverflow.ellipsis,
                ),
                const SizedBox(height: 3),
                Text(
                  subtitle,
                  style: TextStyle(
                    fontSize: 11,
                    color: Colors.grey.shade500,
                  ),
                  maxLines: 1,
                  overflow: TextOverflow.ellipsis,
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }

  Widget _buildContactItem({
    required IconData icon,
    required String title,
    bool isHeader = false,
  }) {
    return Padding(
      padding: const EdgeInsets.symmetric(horizontal: 14, vertical: 12),
      child: Row(
        children: [
          Container(
            padding: const EdgeInsets.all(6),
            decoration: BoxDecoration(
              color: Colors.grey.shade100,
              shape: BoxShape.circle,
            ),
            child: Icon(icon, size: 16, color: Colors.grey.shade700),
          ),
          const SizedBox(width: 12),
          Expanded(
            child: Text(
              title,
              style: TextStyle(
                fontSize: 13.5,
                fontWeight: isHeader ? FontWeight.bold : FontWeight.w500,
                color: isHeader ? const Color(0xFF0F172A) : Colors.grey.shade700,
              ),
            ),
          ),
          Icon(Icons.chevron_right, size: 18, color: Colors.grey.shade400),
        ],
      ),
    );
  }
}
```

---

## 🚀 Hướng dẫn chạy thử dự án

Chỉ cần chạy:
```powershell
cd d:\BT\APP\flutter_application_1
flutter run -d chrome
```
> Trình duyệt Chrome sẽ tự động hiển thị chiếc điện thoại bo góc ở giữa màn hình, **không cần bấm F12 hay Ctrl + Shift + M**. Bạn có thể dùng chuột kéo vuốt lướt màn hình như trên điện thoại thật!
