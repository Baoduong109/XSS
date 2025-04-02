# XSS là gì?

XSS (Cross-site Scripting) là một loại lỗ hổng bảo mật khi bị chèn mã độc (thường là Javascript) vào các ứng dụng website. Khi người dùng truy cập vào trang web bị nhiễm mã độc, trình duyệt sẽ tự động thực thi mã độc đó.

Mục đích của việc này chính là ăn cắp dữ liệu nhận dạng của người dùng như session tokens, cookies và các thông tin khác. Khi đăng nhập vào được các tài khoản website, hacker có thể truy cập vào bất cứ dữ liệu nào và toàn quyền kiểm soát tất cả các chức năng và dữ liệu của ứng dụng.

Tấn công XSS là hình thức tấn công đơn giản nhưng đặc biệt nguy hiểm. Đây cũng là kỹ thuật được hacker sử dụng phổ biến nhất trong thời điểm hiện nay.

### Tác động của XSS

- Thông qua lỗ hổng XSS, kẻ tấn công có thể đánh cắp cookie phiên, qua đó kiểm soát được tài khoản người dùng hợp pháp.

- Tuy nhiên, phạm vi của XSS vượt xa việc đánh cắp cookie; nó cho phép kẻ tấn công phát tán phần mềm độc hại, phá hoại trang web, tạo ra sự hỗn loạn trên mạng xã hội, tham gia lừa đảo để lấy thông tin xác thực và thực hiện nhiều hành động độc hại khác nhau. Khi kết hợp với các kỹ thuật kỹ thuật xã hội, nó có thể dẫn đến các cuộc tấn công phá hoại hơn nữa.

- Trong trường hợp người dùng nạn nhân có quyền quản trị, hậu quả có thể rất nghiêm trọng, bao gồm cả việc thay đổi mã hoặc cơ sở dữ liệu, làm giảm thêm tính bảo mật của ứng dụng web.

- Nếu dữ liệu nhạy cảm bị lộ, hậu quả sẽ nghiêm trọng hơn vì nó bao gồm rò rỉ thông tin quan trọng như số an sinh xã hội, thông tin nhận dạng cá nhân (PII) hoặc thông tin thẻ tín dụng, cũng như các hoạt động trái phép như giao dịch ngân hàng trái phép.

### XSS hoạt động như thế nào?

Tấn công XSS nghĩa là gửi chèn lệnh và script độc hại, những mã đôc hại này thường được viết bằng các ngôn ngữ lập trình phía client như JavaScript, VBScript, Flash, HTML,… Tuy nhiên, cách tấn công này thường sử dụng JavaScript và HTML.

XSS hoạt động bằng cách thao túng một trang web dễ bị tấn công để nó trả về JavaScript độc hại cho người dùng. Khi mã độc thực thi bên trong trình duyệt của nạn nhân, kẻ tấn công hoàn toàn có thể xâm phạm tương tác của họ với ứng dụng.

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/d1456422-fd25-4ae6-806a-9e6932b7e430" />
</p>


### Các loại tấn công XSS phổ biến:
Có 3 loại tấn công lỗ hổng XSS phổ biến, gồm:

- [Reflected XSS](Reflected-XSS.md): Mã độc được chèn vào các URL, khi người dùng click vào URL đó thì mã độc sẽ được thực thi.

- [Stored XSS](Stored-XSS.md): Mã độc được lưu trữ trên máy chủ, khi người dùng truy cập vào trang web sẽ kích hoạt mã độc.

- [DOM-based XSS](DOM-Based-XSS.md): Sử dụng các kỹ thuật JavaScript để thay đổi nội dung trang web và chèn mã độc vào DOM.

### Cách thức phát hiện:

Nên xem xét phần nào của website là có thể bị tấn công XSS. Tốt hơn là liệt kê chúng trong tài liệu kiểm thử và bằng cách này, bảo đảm chúng ta sẽ không bị bỏ xót. Sau đó, lập kế hoạch cho các script nào phải được kiểm tra. Điều quan trọng là, kết quả có ý nghĩa gì, ứng dụng đó là dễ bị lỗ hổng và cần được phân tích các kết quả một cách kỹ lưỡng. Trong khi kiểm thử các cuộc tấn công có thể, điều quan trọng là kiểm tra xem nó đang được đáp ứng như thế nào với các kịch bản đã nhập và các kịch bản đó có được thực thi hay không vv.

**1. Phát hiện thủ công:**

Phương pháp này đòi hỏi người kiểm thử (pen tester) phải thực hiện việc kiểm tra các điểm đầu vào và các phản hồi của hệ thống một cách thủ công, thường xuyên bằng cách tiêm các payloads và theo dõi các kết quả. Các bước chính bao gồm:

- Kiểm tra các điểm đầu vào: Các điểm có thể bị tấn công XSS bao gồm các trường nhập liệu, URL, cookie, form, hoặc bất kỳ phần nào của ứng dụng web có thể nhận dữ liệu từ người dùng.

- Tìm kiếm các trường đầu vào không được kiểm tra đúng cách: Ví dụ: form login, bình luận, tìm kiếm, thông tin URL, headers, vv.

- Tiêm payload XSS vào các trường đầu vào: Sử dụng các payload XSS cơ bản để kiểm tra phản ứng của hệ thống, ví dụ như:
```
<script>alert('XSS');</script>
```
Hoặc các payloads tinh vi hơn như:
```
<img src="javascript:alert('XSS');" />
```

- Kiểm tra phản hồi của ứng dụng: Sau khi tiêm payload, kiểm tra xem liệu mã JavaScript có được thực thi trên trang hay không. Dấu hiệu của XSS là sự xuất hiện của các pop-up, thay đổi nội dung trang, hoặc lỗi JavaScript trên trang.

- Sử dụng Developer Tools: Các công cụ như Chrome DevTools có thể giúp kiểm tra các đầu vào, các request/response, các thay đổi DOM, v.v.

**Có thể tham khảo 1 số payload khác tại đây:** [XSS Injection](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XSS%20Injection) 


**2. Phát hiện XSS tự động:**
Các công cụ tự động giúp phát hiện lỗ hổng XSS bằng cách tự động tiêm các payload XSS vào các trường đầu vào và kiểm tra các phản ứng của hệ thống. Các công cụ tự động này giúp tiết kiệm thời gian và cải thiện khả năng phát hiện các lỗ hổng. Một số công cụ phổ biến bao gồm:

- **Burp Suite:** Burp Suite có tính năng "Scanner" mạnh mẽ giúp tự động quét và phát hiện các lỗ hổng XSS. Các công cụ như Intruder có thể tự động tiêm các payloads XSS vào các điểm đầu vào.

- **OWASP ZAP:** Đây là công cụ quét bảo mật mã nguồn mở cũng có tính năng quét XSS tự động. Nó có khả năng kiểm tra các đầu vào của ứng dụng và xác định các điểm yếu liên quan đến XSS.

- **XSSer:** Một công cụ tự động quét và khai thác các lỗ hổng XSS. XSSer có thể kiểm tra các payload XSS phổ biến và thậm chí có thể thử các kỹ thuật bypass.

- **Nikto:** Nikto là công cụ quét bảo mật mã nguồn mở, mặc dù nó không tập trung riêng vào XSS nhưng vẫn có thể phát hiện một số lỗ hổng XSS thông qua quét các đầu vào.

- **Acunetix:** Một công cụ quét bảo mật tự động giúp phát hiện các lỗ hổng XSS trong ứng dụng web thông qua việc quét các điểm đầu vào.


**3. Kết hợp cả hai phương pháp:**

Kiểm thử thủ công sẽ giúp phát hiện các lỗ hổng mà công cụ tự động có thể bỏ qua, đặc biệt là các tình huống XSS tinh vi như DOM-based XSS.
Kiểm thử tự động giúp quét nhanh chóng và phát hiện các lỗi phổ biến, tiết kiệm thời gian cho người kiểm thử.
Để đạt được kết quả tốt nhất, phương pháp tự động có thể được sử dụng để phát hiện các lỗ hổng nhanh chóng, trong khi phương pháp thủ công có thể được áp dụng để kiểm tra kỹ hơn các trường hợp đặc biệt hoặc các lỗ hổng mà công cụ tự động có thể bỏ sót.

### Các biện pháp phòng ngừa XSS:
Đây là một số ví dụ minh họa kèm theo các biện pháp phòng chống XSS phổ biến được sử dụng.

**1. Mã hóa đầu ra (Output Encoding):**

Đây là biện pháp quan trọng nhất. Mã hóa dữ liệu người dùng trước khi hiển thị trên trang web để trình duyệt hiểu đó là dữ liệu văn bản thuần túy, không phải mã lệnh.
Sử dụng các hàm mã hóa phù hợp với ngữ cảnh hiển thị (ví dụ: mã hóa HTML, URL, JavaScript).
**Ví dụ (PHP):**
```
<?php
$ten_nguoi_dung = $_GET['ten'];
echo htmlspecialchars($ten_nguoi_dung);
?>
```
Sử dụng ```htmlspecialchars()``` sẽ mã hóa các ký tự đặc biệt trong HTMl như ```<```, ```>```, ```&```, ```'```, ```"``` để không thể thực thi mã JavaScript.

**2. Sử dụng Content Security Policy (CSP)**

CSP là một cơ chế bảo mật giúp ngăn chặn việc tải các mã độc từ các nguồn không xác định, bao gồm việc ngăn ngừa XSS.
Ví dụ: Cấu hình CSP trong HTTP headers.
```
<?php
header("Content-Security-Policy: default-src 'self'; script-src 'self' https://trustedscripts.example.com;");
?>
```
Giải thích: CSP chỉ cho phép tải các script từ nguồn đáng tin cậy (trong ví dụ này là self và https://trustedscripts.example.com).

**3. Sử dụng HttpOnly và Secure Cookies**

Đảm bảo rằng các cookies nhạy cảm không thể bị truy cập từ JavaScript bằng cách đánh dấu chúng với thuộc tính HttpOnly và Secure.
Ví dụ: Cấu hình cookie trong PHP.
```
<?php
// Cài đặt cookie với HttpOnly và Secure flag
setcookie('user_session', 'session_value', [
    'httponly' => true, 
    'secure' => true, 
    'samesite' => 'Strict'
]);
?>
```
Các cookie được đánh dấu với HttpOnly sẽ không thể bị truy cập thông qua JavaScript, giúp ngăn ngừa tấn công XSS.

**4. Chặn Các Thẻ Nguy Hiểm**

Đảm bảo rằng người dùng không thể nhập vào các thẻ HTML nguy hiểm như ```<script>```, ```<img>```, v.v.
Ví dụ: Lọc các thẻ nguy hiểm bằng thư viện PHP.
```
<?php
$user_input = $_GET['comment'];
$allowed_tags = '<b><i><u>';
$safe_input = strip_tags($user_input, $allowed_tags);
echo $safe_input;
?>
```
strip_tags giúp loại bỏ các thẻ HTML không mong muốn, chỉ cho phép các thẻ được liệt kê.

**5. Sử dụng Đầu Vào và Đầu Ra Xác Thực**

Kiểm tra và xác thực tất cả đầu vào từ người dùng để đảm bảo chúng không chứa mã JavaScript hoặc các ký tự không an toàn.
Ví dụ: Xác thực địa chỉ email.
```
<?php
$email = $_POST['email'];
if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
    die("Invalid email address.");
}
?>
```
filter_var đảm bảo rằng đầu vào là một email hợp lệ, ngăn ngừa việc nhập dữ liệu không hợp lệ.

**6. Cập nhật và vá các lỗ hổng thường xuyên**

Đảm bảo rằng hệ thống và các thư viện phần mềm luôn được cập nhật để vá các lỗ hổng bảo mật, bao gồm các lỗ hổng XSS. 
Việc cập nhật phần mềm thường xuyên sẽ giúp bảo vệ ứng dụng khỏi các lỗ hổng đã được phát hiện và sửa lỗi.
