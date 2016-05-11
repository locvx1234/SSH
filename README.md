# SSH
ghi chép về SSH

## 1. SSH là gì ?

**SSH** (Secure shell) là một giao thức mạng để thiết lập kết nối bảo mật. 

SSH hoạt động ở tầng Application trong mô hình TCP/IP. SSH tương tác giữa máy khách và máy chủ có sử dụng cơ chế mã hóa mạnh, ngăn chặn nghe trộm, đánh cắp thông tin.

Những chương trình như Telnet, rlogin không sử dụng mã hóa, rất có thể bị lộ dữ liệu trên đường truyền. Sử dụng SSH để đảm bảo bảo mật khi truyền tin trên mạng.

## 2. Hoạt động 
SSH hoạt động theo 3 bước :

- Định danh host (xác định định danh hệ thống tham gia)
- Mã hóa (thiết lập kênh truyền có mã hóa)
- Xác thực (xác thực người sử dụng có quyền đăng nhập)

#### Định danh host 

SSH sử dụng một khóa định danh duy nhất. Khóa này có 2 thành phần : public key và private key

Dữ liệu được mã hóa bằng public key và chỉ được giải mã bằng private key 

Khi có sự thay đổi cấu hình ở server, khóa định danh cũng sẽ thay đổi và những người sử dụng SSH cũng được biết về sự thay đổi này

Bắt đầu phiên làm việc, server public key cho client, client sinh ra một session key và mã hóa bằng public key của server và gửi về server. Server giải mã bằng private key và nhận được session key. Session key được sử dụng để trao đổi dữ liệu giữa hai máy. 

#### Mã hóa (Encryption)

Sau khi thiết lập phiên làm việc bảo mật, dữ liệu trao đổi qua đường truyền được mã hóa và giải mã theo cơ chế đã thỏa thuận giữa client-server trước đó, thường do client quyết định.

Một số cơ chế mã hóa : 3DES, IDEA và Blowfish 

#### Chứng thực (Authentication ) 
Việc chứng thực bằng username/password là một cách thông dụng để định danh người sử dụng 

Bên cạnh đó có một vài cách khác : chứng thực RSA, sử dụng ssh-keygen và ssh-agent 



## .Tham khảo

https://vi.wikipedia.org/wiki/SSH



