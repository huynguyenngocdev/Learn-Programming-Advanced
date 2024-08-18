# Optimize actions with Debounce and Throttle

Trong lập trình ứng dụng, đặc biệt là khi xử lý các sự kiện như nhấn nút hoặc cuộn trang, việc kiểm soát tần suất các sự kiện này rất quan trọng để tránh việc xử lý quá nhiều và cải thiện hiệu suất. **`Debounce`** và **`Throttle`** đều là hai phuơng pháp dùng để điều khiển một hàm được gọi bao nhiêu lần, trong khoảng thời gian xác định. Tuy nhiên cách hoạt động có khác nhau đôi chút.

## Debounce

- **Debounce** là kỹ thuật giúp tránh việc xử lý quá nhiều sự kiện liên tiếp bằng cách chỉ thực hiện hành động sau khi không có sự kiện nào xảy ra trong một khoảng thời gian cụ thể. Nếu một sự kiện mới xảy ra trước khi khoảng thời gian này kết thúc, thì thời gian đếm lại từ đầu.

- Trường hợp sử dụng: được dùng khi bạn cần thực hiện hành động sau khi người dùng đã ngừng hành động trong một khoảng thời gian nhất định, ví dụ: tìm kiếm trong khi gõ văn bản hoặc xử lý sự kiện cuộn (scroll).

- Lợi ích: Giảm số lượng lần gọi hàm và tối ưu hóa hiệu suất khi xử lý các sự kiện liên tiếp trong thời gian ngắn.

- Ví dụ: Khi người dùng gõ văn bản vào ô tìm kiếm, bạn có thể đợi một khoảng thời gian (ví dụ: 300ms) sau khi người dùng dừng gõ để gửi yêu cầu tìm kiếm, thay vì gửi yêu cầu mỗi lần người dùng gõ một ký tự.

```swift
// In Swift
import Combine

var cancellables = Set<AnyCancellable>()
let searchTextPublisher = PassthroughSubject<String, Never>()

searchTextPublisher
    .debounce(for: .milliseconds(300), scheduler: RunLoop.main)
    .sink(receiveValue: { searchText in
        print("Search text: \(searchText)")
        // Thực hiện tìm kiếm
    })
    .store(in: &cancellables)
```

```javascript
// In JavaScript debounce can be import from `lodash`
const debounce = (callback, delayMiliSeconds) => {
    delayMiliSeconds = delayMiliSeconds || 0;
    let timerId;
    return () => {
        if (timerId) {
            clearTimeout(timerId);
            timerId = null;
        }

        timerId = setTimeout(() => {
            callback();
        }, delayMiliSeconds);
    }
}

const handleTextChange = (searchText) => {
    console.log("Search text: ", searchText);
}

const searchInput = document.querySelector('searchInput');
searchInput.addEventListener('input', debounce(handleTextChange, 300));
```

## Throttle

- **Throttle** là kỹ thuật giúp giới hạn số lần gọi hàm trong một khoảng thời gian nhất định, bất kể có bao nhiêu sự kiện xảy ra. Sau khoảng thời gian đó, hành động sẽ được thực hiện một lần nữa.

- Trường hợp sử dụng: thường dùng khi bạn cần giới hạn số lần thực hiện hành động trong một khoảng thời gian cụ thể, ví dụ: xử lý sự kiện cuộn (scroll) liên tục hoặc các sự kiện nhấn nút.

- Lợi ích: Giảm số lần gọi hàm khi có nhiều sự kiện liên tiếp, giúp duy trì hiệu suất và tránh việc thực hiện hành động quá nhiều lần.

- Ví dụ: Khi người dùng cuộn trang, bạn có thể muốn chỉ xử lý sự kiện cuộn mỗi giây một lần để giảm tải cho việc tính toán vị trí hoặc tải thêm nội dung.

```swift
// In Swift
import Combine

var cancellables = Set<AnyCancellable>()
let scrollPublisher = PassthroughSubject<Void, Never>()

scrollPublisher
    .throttle(for: .seconds(1), scheduler: RunLoop.main, latest: true)
    .sink(receiveValue: {
        print("Scroll event")
        // Xử lý sự kiện cuộn
    })
    .store(in: &cancellables)
```

```javascript
// In JavaScript throttle can be import from `lodash`
const throttle = (callback, delayMiliSeconds) => {
    delayMiliSeconds = delayMiliSeconds || 0;
    let last = 0;
    return () => {
        const now = new Date().getTime();
        if (now - last < delayMiliSeconds) {
            return;
        }
        last = now;
        callback();
    }
}

var scrollHandler = document.querySelector("scroll");
scrollHandler.addEventListener('scroll', throttle(() => {
        console.log("Scroll event");
}, 1*1000));
```
