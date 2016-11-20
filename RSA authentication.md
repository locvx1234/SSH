Việc chứng thực bằng password của ssh có một vấn đề là trong phiên kết nối đầu tiên với server, kẻ tấn công có thể giả mạo server để tạo kết nối tới chính client.

Do đó, ở lần kết nối đầu tiên, ta luôn nhận được một cảnh báo 

<img src="http://i.imgur.com/JSIfL0S.png">

Các lần kết nối sau, key của server sẽ được cache lại, cảnh báo sẽ không xuất hiện nữa. 

Một cách chứng thực khác cho phép chúng ta không phải nhập password mỗi khi bắt đầu phiên kết nối, đó là sử dụng key.

`private key` nằm ở, `public key` nằm ở server.

Cách tạo key có thể thực hiện ở server hoặc client. Thông thường, ta sử dụng client tạo cặp key và gửi public cho server, giữ lại thành phần private key.



 

