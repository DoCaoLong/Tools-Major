# 🛠️ Hướng dẫn cài đặt

> Yêu cầu đã cài đặt NodeJS

- Bước 1: Tải về phiên bản mới nhất của tool [tại đây ⬇️](https://github.com/DoCaoLong/Tools-Major/archive/refs/heads/master.zip)
- Bước 2: Giải nén tool
- Bước 3: Tại thư mục tool vừa giải nén (thư mục có chứa file package.json), chạy lệnh `npm install` để cài đặt các thư viện bổ trợ

## 💾 Cách thêm dữ liệu tài khoản

> Tool hỗ trợ cả `user` và `query_id` (khuyến khích dùng query_id)

> Tất cả dữ liệu mà bạn cần nhập đều nằm ở các file trong thư mục 📁 `src / data`

- [users.txt](src/data/users.txt) : chứa danh sách `user` hoặc `query_id` của các tài khoản, mỗi dòng ứng với một tài khoản
- [proxy.txt](src/data/proxy.txt) : chứa danh sách proxy, proxy ở mỗi dòng sẽ ứng với tài khoản ở dòng đó trong file users.txt phía trên, để trống nếu không dùng proxy.
- [token.json](src/data/token.json) : chứa danh sách token được tạo ra từ `user` hoặc `query_id`. Token sẽ được tự động sinh ra khi bạn chạy tool. (Không cần quan tâm đến file này)

> Định dạng proxy: <http://user:pass@ip:port>

## >\_ Các lệnh và chức năng tương ứng

| Lệnh            | Chức năng                                                                           |
| --------------- | ----------------------------------------------------------------------------------- |
| `npm run start` | Dùng để làm nhiệm vụ, điểm danh, chơi game,.... tóm lại game có gì là nó làm cái đó |

## 🕹️ Các tính năng có trong tool

- tự động điểm danh hàng ngày
- tự động làm nhiệm vụ
- tự động chơi game khi tới giờ (các game có thể chơi: Hold Coin, Roulette, Swipe Coin, Durov)
- nhận diện proxy tự động, tự động kết nối lại proxy khi bị lỗi. ae ai chạy proxy thì thêm vào file proxy.txt ở dòng ứng với dòng chứa acc muốn chạy proxy đó, acc nào không muốn chạy proxy thì để trống hoặc gõ skip vào
- đa luồng chạy bao nhiêu acc cũng được, không bị block lẫn nhau, lặp lại khi tới thời gian chơi game
- hiển thị đếm ngược tới lần chạy tiếp theo, có thể tìm biến `IS_SHOW_COUNTDOWN = true` đổi thành `false` để tắt cho đỡ lag

> [!WARNING]
>
> - Game Durov có combo trả lời đổi mỗi ngày nên tool sẽ bắt đầu chạy task này từ 9h sáng thay vì 7h sáng để có đủ thời gian cập nhật combo mới
> - Có nhiều nhiệm vụ yêu cầu phải làm thủ công, không claim láo được nên đừng thắc mắc sao còn nhiều nhiệm vụ chưa làm thế.
> - Nếu gặp lỗi 5xx khi chơi game thì kệ nó, điểm vẫn được tính, do server lỏ thôi
> - Vì server nó hay lỗi vặt nên đừng bất ngờ khi thấy các lỗi 5xx nhé

## ♾ Cài đặt đa luồng

- Mặc định tool sẽ chạy đa luồng ứng với số tài khoản bạn nhập vào, không cần cài đặt thêm gì cả.
- Mặc định ở vòng lặp đầu tiên mỗi tài khoản (luồng) sẽ chạy cách nhau 30s để tránh spam request, có thể tìm biến `DELAY_ACC = 30` trong file [index.js](src/run/index.js) để điều chỉnh cho phù hợp

## ❌ Chế độ thử lại khi lỗi

- Đỗi với lỗi kết nối proxy, hệ thống sẽ cố thử lại sau mỗi 30s, bạn có thể cài đặt giới hạn số lần thử lại bằng cách tìm biến `MAX_RETRY_PROXY = 20` trong file [index.js](src/run/index.js) để điều chỉnh cho phù hợp (mặc định là 20). Khi quá số lần thử kết nối lại hệ thống sẽ dừng auto tài khoản đó và nghi nhận lỗi vào file [log.error.txt](src/data/log.error.txt)
- Đỗi với lỗi đăng nhập thất bại, hệ thống sẽ cố thử lại sau mỗi 60s, bạn có thể cài đặt giới hạn số lần thử lại bằng cách tìm biến `MAX_RETRY_LOGIN = 20` trong file [index.js](src/run/index.js) để điều chỉnh cho phù hợp (mặc định là 20). Khi quá số lần thử đăng nhập lại hệ thống sẽ dừng auto tài khoản đó và nghi nhận lỗi vào file [log.error.txt](src/data/log.error.txt)

## 🔄 Lịch sử cập nhật

> Khi cập nhật phiên bản mới chỉ cần copy thư mục 📁 [data](src/data) của bản cũ ghi đè lại ở bản mới là có thể chạy được mà không cần lấy lại data

> Phiên bản mới nhất: `v0.0.6`

<details>
<summary>v0.0.6 - 📅 30/09/2024</summary>
  
- Thêm thử đăng nhập lại khi lỗi
- Thêm delay 1s cho mỗi request, bạn sẽ thấy tool chạy chậm hơn nhưng nó đảm bảo tool ổn định hơn

</details>
<details>
<summary>v0.0.5 - 📅 29/09/2024</summary>
  
- Fix lỗi đăng nhập

</details>
<details>
<summary>v0.0.4 - 📅 14/09/2024</summary>
  
- Thêm làm task xem video youtube nhập code
- Thêm thông báo từ hệ thống và kiểm tra version

</details>
<details>
<summary>v0.0.3 - 📅 13/09/2024</summary>
  
- Sửa lỗi spam request server github

</details>
<details>
<summary>v0.0.2 - 📅 12/09/2024</summary>
  
- Thêm tự động lấy dữ liệu từ server mỗi 20-40 phút mà không cần chạy lại tool

</details>
<details>
<summary>v0.0.1 - 📅 12/09/2024</summary>
  
- Chia sẽ tool đến cộng đồng

</details>
