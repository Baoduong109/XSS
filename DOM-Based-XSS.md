# DOM là gì?

DOM là tên gọi viết tắt của (Document Object Model – tạm dịch Mô hình Các Đối tượng Tài liệu). Là một chuẩn được định nghĩa bởi W3C (Tổ Chức Web Toàn Cầu – World Wide Web Consortium). DOM được dùng để truy xuất và thao tác trên các tài liệu có cấu trúc dạng HTML hay XML bằng các ngôn ngữ lập trình thông dụng như Javascript, PHP…



<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/5a9c9ea4-3e40-46f1-a15f-901678faff56" />
</p>

### Cấu trúc DOM

**Node**

Đối với HTML DOM, mọi thành phần đều được xem là một node (nút), được biểu diễn trên 1 cây cấu trúc dạng cây gọi là DOM Tree. Các phần tử khác nhau sẽ được phân loại node khác nhau nhưng quan trọng nhất là 3 loại: node gốc (document node), node phần tử (element node), node văn bản (text node).

- Node gốc: chính là tài liệu HTML, thường được biểu diễn bởi thẻ ```<html>```.
- Node phần tử: biểu diễn cho 1 phần tử HTML.
- Node văn bản: mỗi đoạn kí tự trong tài liệu HTML, bên trong 1 thẻ HTML đều là 1 node văn bản. Đó có thể là tên trang web trong thẻ ```<title>```, tên đề mục trong thẻ ```<h1>```, hay một đoạn văn trong thẻ ```<p>```.
- Ngoài ra còn có node thuộc tính (attribute node) và node chú thích (comment node).

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/84352d49-1fe0-42f0-a358-6af3f7b15ab5" />
</p>

### Các loại DOM trong Javascript

Javascript cung cấp cho chúng ta nhiều loại DOM để xử lí HTML và CSS dễ dàng hơn.

- DOM document: lưu trữ toàn bộ các thành phần trong documents của website.
- DOM element: truy xuất tới thẻ HTML nào đó thông qua các thuộc tính như tên class, id, name của thẻ HTML.
- DOM HTML: thay đổi giá trị nội dung và giá trị thuộc tính của các thẻ HTML.
- DOM CSS: thay đổi các định dạng CSS của thẻ HTML.
- DOM Event: gán các sự kiện như onclick(), onload() vào các thẻ HTML.
- DOM Listener: lắng nghe các sự kiện tác động lên thẻ HTML.
- DOM Navigation dùng để quản lý, thao tác với các thẻ HTML, thể hiện mối quan hệ cha – con của các thẻ HTML
- DOM Node, Nodelist: thao tác với HTML thông qua đối tượng (Object).

Thao tác với DOM

Mọi nội dung đều có thể được cập nhật động thông qua các thuộc tính và phương thức của DOM. Từ thay đổi định dạng chữ, nội dung chữ đến thay đổi cấu trúc các node và cả thêm node mới. Bạn cần hiểu rõ cách thao tác DOM và ý nghĩa của từng thuộc tính, phương thức.

### Các Thuộc tính và Phương thức thường gặp

**Thuộc tính:**

- **id:** Định danh – là duy nhất cho mỗi phần tử nên thường được dùng để truy xuất DOM trực tiếp và nhanh chóng.
- **className:** Tên lớp – Cũng dùng để truy xuất trực tiếp như id, nhưng 1 className có thể dùng cho nhiều phần tử.
- **tagName:** Tên thẻ HTML.
- **innerHTML:** Trả về mã HTML bên trong phần tử hiện tại. Đoạn mã HTML này là chuỗi kí tự chứa tất cả phần tử bên trong, bao gồm các node phần tử và node văn bản.
- **outerHTML:** Trả về mã HTML của phần tử hiện tại. Nói cách khác, outerHTML = tagName + innerHTML.
- **textContent:** Trả về 1 chuỗi kí tự chứa nội dung của tất cả node văn bản bên trong phần tử hiện tại.
- **attributes:** Tập các thuộc tính như id, name, class, href, title…
- **style:** Tập các định dạng của phần tử hiện tại
value: Lấy giá trị của thành phần được chọn thành một biến.


**Phương thức:**

- **getElementById(id):** Tham chiếu đến 1 node duy nhất có thuộc tính id giống với id cần tìm.
- **getElementsByTagName(tagname):** Tham chiếu đến tất cả các node có thuộc tính tagName giống với tên thẻ cần tìm, hay hiểu đơn giản hơn là tìm tất cả các phần tử DOM mang thẻ HTML cùng loại. Nếu muốn truy xuất đến toàn bộ thẻ trong tài liệu HTML thì hãy sử dụng document.getElementsByTagName('*').
- **getElementsByName(name):** Tham chiếu đến tất cả các node có thuộc tính name cần tìm.
- **getAttribute(attributeName):** Lấy giá trị của thuộc tính.
- **setAttribute(attributeName, value):** Sửa giá trị của thuộc tính.
- **appendChild(node):** Thêm 1 node con vào node hiện tại.
- **removeChild(node):** Xóa 1 node con khỏi node hiện tại.

Mặt khác, các phần tử DOM đều là các node trên cây cấu trúc DOM. Chúng sở hữu thêm các thuộc tính quan hệ để biểu diễn sự phụ thuộc giữa các node với nhau. Nhờ các thuộc tính quan hệ này, chúng ta có thể truy xuất DOM gián tiếp dựa trên quan hệ và vị trí của các phần tử:

**Thuộc tính quan hệ:**

- **parentNode:** node cha
- **childNodes:** Các node con
- **firstChild:** node con đầu tiên
- **lastChild:** node con cuối cùng
- **nextSibling:** node anh em liền kề sau
- **previousSibling:** node anh em liền kề trước

## Tóm lại:

DOM (Document Object Model) là một mô hình đối tượng cho phép các ngôn ngữ lập trình, đặc biệt là JavaScript, tương tác với các phần tử và cấu trúc của một trang web. Nó mô phỏng cấu trúc của tài liệu HTML hoặc XML dưới dạng một cây đối tượng, nơi mỗi phần tử HTML (như thẻ ```<div>```, ```<p>```, ```<a>```, v.v.) là một nút (node) trong cây này.

DOM cung cấp các phương thức và thuộc tính để bạn có thể:

1. Truy cập và thay đổi nội dung của trang web.
2. Thêm, sửa hoặc xóa các phần tử HTML.
3. Lắng nghe và xử lý các sự kiện (như click, nhập liệu, v.v.).

DOM là cầu nối giữa HTML và các hành động mà người dùng thực hiện trên trang web, và giúp tạo ra các trang web động, tương tác.


# DOM-Based XSS

DOM XSS là kiểu tấn công XSS trong đó payload không được gửi đến server hoặc phản hồi từ server, mà thay vào đó được thực thi khi JavaScript phía client đọc và xử lý dữ liệu từ môi trường trình duyệt (DOM), và chèn nó vào trang một cách không an toàn.

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/b308f574-d0b0-48cb-b606-8643876abfaa" />
</p>

Tấn công DOM-based XSS (Cross-Site Scripting) xảy ra khi mã độc được chèn vào trang web thông qua cách thức xử lý dữ liệu của JavaScript mà không cần phải gửi yêu cầu tới máy chủ. Điều này có nghĩa là, thay vì lợi dụng các lỗ hổng trên server để chèn mã độc vào trang, kẻ tấn công lợi dụng cách mà trang web xử lý dữ liệu từ phía client (trình duyệt).

### Cách thức tấn công DOM-based XSS:

**Xác định các điểm tiềm ẩn trong DOM:**

Kẻ tấn công tìm các điểm mà dữ liệu từ người dùng hoặc các nguồn bên ngoài (như URL, cookie, hoặc địa chỉ IP) được đưa vào mà không được kiểm tra hoặc mã hóa đúng cách.
Các điểm này có thể là các tham số trong URL, các giá trị trong cookie, hoặc các đầu vào mà trang web lấy từ người dùng (như document.location, document.cookie, document.referrer).
Tiêm mã độc vào dữ liệu đầu vào:
Kẻ tấn công chèn mã JavaScript độc hại vào các tham số trong URL hoặc bất kỳ nơi nào mà trang web sử dụng mà không kiểm tra kỹ. Ví dụ, sử dụng URL như:
```http://example.com/?user=<script>alert('XSS')</script>```

**JavaScript xử lý và thực thi mã độc:**

Trang web sau đó sử dụng JavaScript để xử lý dữ liệu mà không thực hiện kiểm tra hoặc mã hóa (sanitize) đúng cách. Ví dụ, nếu mã JavaScript nhận tham số user từ URL và sau đó trực tiếp gắn nó vào DOM mà không kiểm tra, điều này có thể dẫn đến việc thực thi mã JavaScript mà kẻ tấn công đã tiêm vào.

**Một ví dụ về mã JavaScript dễ bị tấn công:**

```
var user = document.location.search.split('=')[1];
document.getElementById("user-name").innerHTML = user;
```
Kết quả là mã độc được thực thi trong trình duyệt của người dùng:
Khi người dùng mở trang web này, mã độc được tiêm sẽ chạy trong ngữ cảnh của trang web, có thể đánh cắp thông tin người dùng (cookie, session, v.v.), thay đổi nội dung trang, hoặc thực hiện các hành động có hại khác.

### Sink và Source trong tập lệnh dựa trên DOM

Mỗi lỗ hổng XSS dựa trên DOM đều có hai thành phần: nguồn đầu vào của người dùng và mục tiêu nơi đầu vào của người dùng này được viết, được gọi là sink. Các nguồn phổ biến mà kẻ tấn công có thể thao túng là ```document.URL```, ```document.documentURI```, ```location.href```, ```location.search```, ```location.*```, ```window.name```, và ```document.referrer```. Các sink phổ biến là ```document.write```, ```(element).innerHTML```, ```eval```, ```setTimeout```, ```setInterval```, và ```execScript```. Lưu ý rằng danh sách này không đầy đủ và còn nhiều nguồn và sink khác nữa.

Để mã JavaScript dễ bị tấn công XSS dựa trên DOM, mã này phải lấy thông tin từ một nguồn mà kẻ tấn công có thể kiểm soát, sau đó chuyển thông tin này đến bộ thu.

### Ví dụ về kịch bản chéo trang dựa trên DOM

### Hậu quả của các cuộc tấn công dựa trên DOM

Các lỗ hổng cross-site scripting dựa trên DOM không phổ biến lắm nhưng hậu quả của một cuộc tấn công thành công có thể thảm khốc như các cuộc tấn công Reflected XSS khác . Sau đây là một số hành động mà một hacker mũ đen có thể thực hiện dựa trên ví dụ đơn giản được trình bày trước đó:

- Họ có thể tạo một chiến dịch lừa đảo và gửi hàng triệu email chứa liên kết độc hại với nội dung chuyển hướng người dùng đến một trang lừa đảo được thiết kế để bắt chước ứng dụng web của bạn. Kết quả là, hàng triệu người dùng có khả năng bị đánh cắp thông tin đăng nhập và đổ lỗi cho ứng dụng web của bạn, điều này sẽ gây tổn hại nghiêm trọng đến danh tiếng của bạn.

- Họ có thể tạo một tải trọng gửi người dùng đến một trang độc hại bắt chước trang đăng nhập của ứng dụng của bạn. Sau đó, họ có thể gửi URL độc hại này đến người dùng nội bộ của bạn, thậm chí là CEO của bạn. Nếu ngay cả một trong những người dùng của bạn mắc bẫy, kẻ tấn công sẽ lấy được thông tin đăng nhập của họ để leo thang cuộc tấn công. Cuối cùng, điều này có thể cho phép những kẻ tấn công độc hại truy cập vào các hệ thống máy tính khác trong tổ chức của bạn.


### Cách phát hiện lỗ hổng DOM-Based XSS

Do bản chất độc đáo của lỗ hổng XSS dựa trên DOM, nhiều công cụ bảo mật ứng dụng web không phát hiện ra chúng. Đây là trường hợp của các công cụ tập trung vào mã phía máy chủ và phân tích các yêu cầu HTTP nhưng không thể quét các tập lệnh được thực thi trong trình duyệt. Ví dụ, hầu hết các công cụ SAST và IAST được tạo ra để quét các ngôn ngữ phía máy chủ cụ thể và bỏ qua mã JavaScript. 
