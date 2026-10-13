# Typing Master

Typing Master là web app luyện gõ chuyên nghiệp cho công việc vận chuyển. Ứng dụng dùng Vanilla HTML CSS JS không cần backend cho chế độ một người và có module Firebase Realtime Database tùy chọn cho phòng đấu online.

## Chạy local

Mở `index.html` trực tiếp bằng trình duyệt hoặc chạy một web server tĩnh

```bash
python3 -m http.server 4173
```

Sau đó mở `http://localhost:4173`

## Deploy GitHub Pages

1. Tạo repository mới trên GitHub
2. Chép toàn bộ thư mục này vào repository
3. Commit và push lên nhánh `main`
4. Mở Settings rồi Pages
5. Chọn Deploy from a branch
6. Chọn nhánh `main` và thư mục `/root`
7. Lưu lại và chờ GitHub cấp URL HTTPS

Ứng dụng là static site nên không cần build command

## Deploy Vercel

Import repository vào Vercel và chọn framework `Other` hoặc dùng Vercel CLI

```bash
vercel --prod
```

`vercel.json` đã có cấu hình header cơ bản

## Cấu hình Firebase cho đấu online

1. Vào Firebase Console và tạo project mới
2. Tạo Realtime Database ở chế độ test trong lúc phát triển
3. Thêm một Web App trong Project settings
4. Sao chép object cấu hình Firebase
5. Mở `firebase-config.js` và thay `const firebaseConfig = null` bằng object cấu hình
6. Deploy lại static site
7. Nút Đấu với bạn bè luôn hiển thị và dùng local fallback khi chưa có Firebase

Cấu trúc dữ liệu dùng dạng

```text
rooms/{roomId}/players/{playerId}
```

Mỗi người chơi lưu tên chỉ số ký tự WPM accuracy trạng thái sẵn sàng hoàn tất và thời điểm hoạt động cuối. Khi triển khai thực tế nên thêm Firebase Realtime Database Rules để giới hạn quyền ghi và thêm Cloud Function hoặc cơ chế dọn phòng quá 30 phút không hoạt động.

## Sử dụng

- Chọn chủ đề và thời gian
- Bấm Bắt đầu
- Gõ từng phím trong ô Gõ tại đây
- Backspace quay lại ký tự trước
- Xem kết quả trực tiếp khi hết giờ hoặc hoàn tất đoạn
- Bật Firebase để tạo hoặc tham gia phòng đấu bằng ID sáu ký tự

## License

MIT

## Cập nhật tính năng đo tốc độ

WPM được tính theo số từ thực tế đã gõ trong thời gian luyện thay vì lấy CPM chia cho năm. Một từ được phân tách bằng khoảng trắng. Accuracy vẫn tính theo từng ký tự để phản ánh lỗi chính xác.

## Quy trình đấu 1v1 bằng ID

1. Hai người mở cùng URL
2. Bấm Đấu với bạn bè
3. Người thứ nhất bấm Tạo phòng mới
4. Sao chép ID sáu ký tự hoặc link mời
5. Người thứ hai nhập ID phòng hoặc mở link mời
6. Khi đủ hai người bấm Sẵn sàng bắt đầu
7. Hệ thống chọn cùng một đoạn và cùng thời lượng
8. Sau đếm ngược ba giây cả hai bắt đầu cùng lúc
9. Tiến độ WPM accuracy và số ký tự được đồng bộ realtime
10. Có thể bấm lại để chơi trận mới

Khi `firebase-config.js` chưa có cấu hình hai tab cùng trình duyệt vẫn có thể dùng fallback local bằng BroadcastChannel và localStorage. Để hai thiết bị ở xa kết nối qua Internet cần điền Firebase Realtime Database config.
