# Summarize about the method optimize performance

### 1. **Native(Android - Java/Kotlin)**

- **Memory Management**: Sử dụng các cấu trúc dữ liệu hợp lý, tránh giữ các tham chiếu không cần thiết để tránh memory leaks. Sử dụng `WeakReference` khi cần thiết.
- **Optimize Layouts**: Tránh sử dụng quá nhiều view lồng nhau. Sử dụng `ConstraintLayout` thay vì `RelativeLayout` hoặc `LinearLayout` để giảm độ phức tạp của layout.
- **Use RecyclerView Instead of ListView**: `RecyclerView` hiệu quả hơn `ListView` khi xử lý danh sách lớn.
- **Lazy Loading**: Tải dữ liệu theo yêu cầu, đặc biệt là đối với hình ảnh và video.
- **Background Tasks**: Sử dụng `WorkManager`, `AsyncTask`, hoặc `Coroutines` để thực hiện các tác vụ nền mà không ảnh hưởng đến UI.
- **Optimizing Drawables**: Sử dụng ảnh vector hoặc `WebP` để tối ưu hóa kích thước tệp.
- **Caching**: Sử dụng caching cho dữ liệu tải từ mạng để giảm tải cho server và tăng tốc độ tải lại dữ liệu.

### 2. **Native (iOS - Swift)**

- **Memory Management**: Sử dụng `ARC (Automatic Reference Counting)` để quản lý bộ nhớ, tránh retain cycles bằng cách sử dụng `weak` và `unowned`.
- **Optimize Auto Layout**: Tránh sử dụng quá nhiều ràng buộc (constraints), và sử dụng layout trực tiếp bằng code nếu cần thiết.
- **Use Instruments for Profiling**: Sử dụng công cụ Instruments để phát hiện và tối ưu các vấn đề về hiệu năng như memory leaks, CPU usage, v.v.
- **Background Tasks**: Sử dụng `DispatchQueue`, `OperationQueue` để thực hiện các tác vụ nền mà không ảnh hưởng đến main thread. Hoặc cũng có thể dùng `Combine` nếu thấy cần xử lý các luồng dữ liệu bất đồng bộ và sự kiện trong ứng dụng.
- **Lazy Loading**: Tương tự Android, chỉ tải tài nguyên khi cần thiết.
- **Image Optimization**: Sử dụng các định dạng ảnh hiệu quả như `JPEG`, `PNG` và xem xét sử dụng `Core Graphics` để vẽ trực tiếp nếu cần.

### 3. **Cross-Platform (Flutter)**

- **Widget Optimization**: Tránh tạo lại widget không cần thiết, đặc biệt là trong các widget phức tạp.
- **Efficient State Management**: Sử dụng các phương pháp quản lý state như `Provider`, `Riverpod`, hoặc `Bloc` để đảm bảo việc cập nhật UI được tối ưu.
- **Reduce Rebuilds**: Sử dụng `const` constructor cho các widget không cần rebuild.
- **Lazy Loading**: Tải hình ảnh và tài nguyên khác theo yêu cầu, sử dụng `CachedNetworkImage` để caching hình ảnh từ mạng.
- **Optimize Animations**: Sử dụng `AnimatedBuilder` hoặc `CustomPainter` khi cần vẽ các animation phức tạp để tối ưu hóa.

### 4.**Cross-Platform (React Native)**

- **Optimize Component Rendering**: Sử dụng `PureComponent` hoặc `React.memo` để tránh rendering không cần thiết.
- **Use FlatList/SectionList Instead of ScrollView**: Đối với danh sách lớn, sử dụng `FlatList` hoặc `SectionList` thay vì `ScrollView` để tối ưu bộ nhớ.
- **Efficient State Management**: Sử dụng `useReducer`, `Redux`, hoặc `Zustand` để quản lý state một cách hiệu quả.
- **Optimize Images**: Sử dụng các định dạng ảnh nén như `JPEG`, `PNG`, và tích hợp các công cụ như `react-native-fast-image` để caching hình ảnh.
- **Lazy Loading**: Tải tài nguyên theo yêu cầu, đặc biệt là hình ảnh và các dữ liệu lớn.
- **Minimize Bridge Crossings**: Giảm thiểu việc gọi hàm qua cầu nối giữa JavaScript và Native để tăng tốc độ thực thi.
