# BookingApp

Ứng dụng Android đặt phòng khách sạn (Nhóm 2), viết bằng Kotlin và Jetpack Compose.

Tính năng: đăng ký, đăng nhập (kể cả Google), quên mật khẩu bằng OTP, tìm kiếm và xem khách sạn, đặt phòng, quản lý đơn đặt, danh sách yêu thích, chat và trang quản trị. App có tiếng Việt và tiếng Anh, đổi được ngôn ngữ ngay trong app.

## Công nghệ

- Kotlin, Jetpack Compose (Material 3), Navigation Compose
- Retrofit + OkHttp + kotlinx.serialization để gọi REST API
- DataStore để lưu phiên đăng nhập và cài đặt
- Coil để tải ảnh
- Credential Manager để đăng nhập Google

## Yêu cầu

- JDK 17 trở lên
- Android SDK, compileSdk / targetSdk 37, minSdk 26
- Android Studio (bản hỗ trợ AGP 9.3) hoặc chỉ cần Gradle wrapper có sẵn

## Cài đặt

```bash
git clone https://github.com/Dungnony/BookingApp.git
cd BookingApp/android
```

Mở thư mục `android/` bằng Android Studio. Android Studio sẽ tự tạo `local.properties` chứa `sdk.dir`.

Mặc định app gọi backend trên Railway. Nếu muốn dùng backend chạy trên máy mình, thêm dòng sau vào `android/local.properties` (`10.0.2.2` là địa chỉ máy tính khi nhìn từ emulator):

```properties
api.baseUrl=http://10.0.2.2:8080
```

`local.properties` không được commit lên git.

## Build và test

Chạy trong thư mục `android/`:

```bash
./gradlew assembleDebug        # build APK debug (Windows: .\gradlew.bat assembleDebug)
./gradlew testDebugUnitTest    # chạy unit test
./gradlew lintDebug            # kiểm tra lint
```

APK được tạo ở `android/app/build/outputs/apk/debug/`.

> Trên Windows, nếu đường dẫn tới dự án có ký tự có dấu (ví dụ `Máy tính`), `testDebugUnitTest` sẽ báo `ClassNotFoundException`. Hãy đặt dự án ở thư mục chỉ có ký tự ASCII, ví dụ `C:\dev\BookingApp`.

## Cấu trúc

```
android/app/src/main/java/com/nhom2/booking/
├── data/     # API (Retrofit), model, repository, session, settings
├── domain/   # quy tắc nghiệp vụ và validate, không phụ thuộc Android
└── ui/       # màn hình Compose + ViewModel, chia theo tính năng
```

Chuỗi giao diện nằm ở `res/values/strings.xml` (tiếng Việt) và `res/values-en/strings.xml` (tiếng Anh).
