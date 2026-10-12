# Hướng dẫn cấu hình lời chúc bằng Google Form

Trang thiệp không tự lưu lời chúc của khách được. Vì vậy lời chúc đi theo đường này:

**Khách bấm "Viết lời chúc" → điền Google Form → lời chúc vào Google Sheet của bạn → bạn duyệt rồi đưa lên thiệp để mọi người cùng thấy.**

---

## Bước 1. Tạo Google Form

1. Vào https://forms.google.com và bấm **Trống** (Blank form).
2. Đặt tiêu đề: `Gửi lời chúc đến Việt Hoàn & Thu Hà`.
3. Thêm 2 câu hỏi:
   - **Tên của bạn**: loại *Câu trả lời ngắn*, bật *Bắt buộc*.
   - **Lời chúc của bạn**: loại *Đoạn văn*, bật *Bắt buộc*.
4. Mở **Cài đặt** (Settings) của Form và kiểm tra:
   - **Không** bật "Yêu cầu đăng nhập" / "Giới hạn 1 phản hồi", để khách không cần tài khoản Google.
   - **Không** bật "Thu thập địa chỉ email".
5. Ở mục **Bản trình bày** (Presentation), sửa "Tin nhắn xác nhận" thành: `Cảm ơn bạn đã gửi lời chúc!`.

## Bước 2. Nối Form với Google Sheet

1. Trong Form, mở tab **Câu trả lời** (Responses).
2. Bấm biểu tượng **Liên kết với Trang tính** (Link to Sheets), chọn **Tạo bảng tính mới**.
3. Từ giờ mỗi lời chúc sẽ hiện thành một dòng trong Sheet, gồm cột thời gian, tên và lời chúc.

Muốn có file Excel: mở Sheet, chọn **Tệp > Tải xuống > Microsoft Excel (.xlsx)**.
Muốn có file txt: chọn **Tệp > Tải xuống > Giá trị phân tách bằng tab (.tsv)**.

> Giữ Sheet ở chế độ **riêng tư** (chỉ bạn xem). Đừng chia sẻ công khai để tránh lộ thông tin khách.

## Bước 3. Lấy link Form gửi cho khách

1. Trong Form, bấm nút **Gửi** (Send) ở góc trên bên phải.
2. Chọn biểu tượng **liên kết** (link), bật **Rút ngắn URL**, rồi bấm **Sao chép**.
3. Bạn sẽ có link dạng `https://forms.gle/xxxxxxxx`.

## Bước 4. Dán link vào thiệp

Có 2 cách:

- **Nhờ Claude (dễ nhất):** nhắn "Dán link Form này vào thiệp: https://forms.gle/xxxxxxxx".
- **Tự sửa file:** mở `thiep-cuoi.html` bằng Notepad hoặc trình soạn code, tìm dòng đầu tiên trong phần `<script>`:

  ```js
  var FORM_URL='';
  ```

  rồi dán link vào giữa hai dấu nháy:

  ```js
  var FORM_URL='https://forms.gle/xxxxxxxx';
  ```

Khi `FORM_URL` có link, mục "Sổ lưu bút" sẽ hiện nút **Viết lời chúc** mở Form trong tab mới. Khi `FORM_URL` để trống, thiệp dùng ô nhập tạm lưu trên máy của từng khách (không chia sẻ cho người khác).

## Bước 5. Đưa lời chúc lên thiệp cho mọi người cùng xem

Nên đọc qua Sheet và chỉ đưa lên những lời chúc phù hợp.

- **Nhờ Claude:** nhắn "Cập nhật lời chúc từ Google Sheet" và gửi tên/link Sheet. Claude đọc Sheet (qua Google Drive đã kết nối) rồi cập nhật thiệp.
- **Tự sửa file:** trong `thiep-cuoi.html`, thêm từng lời chúc vào mảng `WISHES`:

  ```js
  var WISHES=[
    {n:'Nguyễn Văn A',m:'Chúc hai bạn trăm năm hạnh phúc!'},
    {n:'Lê Thị B',m:'Mãi bên nhau nhé, chúc mừng hai bạn!'},
  ];
  ```

  Lưu ý: mỗi lời chúc nằm trong dấu `{ }`, có dấu phẩy cuối dòng. Nếu lời chúc có dấu nháy đơn `'`, đổi thành `\'` hoặc bỏ dấu nháy đó, nếu không trang sẽ lỗi.

## Lỗi thường gặp

| Hiện tượng | Cách xử lý |
|---|---|
| Bấm "Viết lời chúc" nhưng Form đòi đăng nhập | Vào Cài đặt của Form, tắt "Yêu cầu đăng nhập" và "Giới hạn 1 phản hồi". |
| Thiệp vẫn hiện ô nhập thay vì nút | `FORM_URL` đang trống hoặc dán sai chỗ. Kiểm tra lại dấu nháy. |
| Trang trắng sau khi sửa file | Có thể thiếu dấu phẩy hoặc dấu nháy trong mảng `WISHES`. Kiểm tra lại từng dòng. |
| Lời chúc mới không hiện lên thiệp | Lời chúc chỉ hiện sau khi bạn làm Bước 5, vì thiệp không tự đọc Sheet. |
