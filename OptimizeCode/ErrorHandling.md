# Error Handling (Xử lý lỗi)

### 1. **Native (Android - Java/Kotlin)**

- **Exception Handling**: Sử dụng `try-catch` để xử lý các ngoại lệ. Tránh sử dụng ngoại lệ cho các tình huống thông thường để tránh ảnh hưởng đến hiệu năng.
- **Null Safety**: Sử dụng tính năng null safety của Kotlin để tránh NullPointerException.
- **Logging**: Sử dụng `Logcat` để ghi lại các log hữu ích cho việc debug. Sử dụng `Timber` cho logging cấu trúc hơn.
- **Error Reporting**: Tích hợp các công cụ như `Firebase Crashlytics` để báo cáo lỗi từ người dùng thực.

### 2. **Native (iOS - Swift)**

- **Error Handling**: Sử dụng `do-catch` cho các thao tác có thể phát sinh lỗi, và phân biệt rõ ràng lỗi bằng cách sử dụng `Error` protocol.
- **Optionals**: Sử dụng Optionals để xử lý giá trị có thể là nil và tránh crashes do nil.
- **Logging**: Sử dụng `print()` hoặc tích hợp các thư viện logging để ghi lại các thông tin debug.
- **Error Reporting**: Sử dụng `Firebase Crashlytics` hoặc các công cụ tương tự để báo cáo lỗi từ ứng dụng thực tế.

### 3. **Cross-Platform (Flutter)**

- **Error Boundaries**: Sử dụng `ErrorWidget` để hiển thị UI thay thế khi gặp lỗi trong quá trình render.
- **Exception Handling**: Sử dụng `try-catch` để quản lý ngoại lệ và `Future` với `onError` callback cho xử lý lỗi trong asynchronous code.
- **Logging**: Sử dụng `debugPrint()` hoặc các thư viện logging để theo dõi thông tin debug.
- **Error Reporting**: Tích hợp `Sentry` hoặc `Firebase Crashlytics` để thu thập và phân tích lỗi từ người dùng thực.

### 4. **Cross-Platform (React Native)**

- **Error Boundaries**: Sử dụng `ErrorBoundary` component để quản lý lỗi trong cây component.
- **Exception Handling**: Sử dụng `try-catch` và xử lý Promise rejections bằng `catch()` trong asynchronous code.
- **Logging**: Sử dụng `console.log`, `Reactotron`, hoặc các công cụ logging khác để theo dõi các sự kiện và lỗi.
- **Error Reporting**: Tích hợp `Sentry`, `Bugsnag`, hoặc `Firebase Crashlytics` để báo cáo lỗi từ ứng dụng.
