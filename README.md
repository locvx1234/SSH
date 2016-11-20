# SSH
ghi chép về SSH

## Mục lục 

[1. SSH là gì ?](#what)

[2. Hoạt động](#active)

[3. Một số thuật toán sử dụng trong SSH](#algorithm)

[4. Cài đặt và cấu hình](#install)

[5. Sử dụng](#use)

[6. Bắt gói tin SSH](#wireshark)

[7. Tham khảo](#reference)

<a name=""></a>
## 1. SSH là gì ?

**SSH** (Secure shell) là một giao thức mạng để thiết lập kết nối bảo mật. 

SSH hoạt động ở tầng Application trong mô hình TCP/IP. SSH tương tác giữa máy khách và máy chủ có sử dụng cơ chế mã hóa mạnh, ngăn chặn nghe trộm, đánh cắp thông tin.

Những chương trình như Telnet, rlogin không sử dụng mã hóa, rất có thể bị lộ dữ liệu trên đường truyền. Sử dụng SSH để đảm bảo bảo mật khi truyền tin trên mạng.

<a name="active"></a>
## 2. Hoạt động 
SSH hoạt động theo 3 bước :

- Định danh host (xác định định danh hệ thống tham gia)
- Mã hóa (thiết lập kênh truyền có mã hóa)
- Xác thực (xác thực người sử dụng có quyền đăng nhập)

#### Định danh host 

SSH sử dụng một khóa định danh duy nhất. Khóa này có 2 thành phần : public key và private key

Dữ liệu được mã hóa bằng public key và chỉ được giải mã bằng private key 

Khi có sự thay đổi cấu hình ở server, khóa định danh cũng sẽ thay đổi và những người sử dụng SSH cũng được biết về sự thay đổi này

Bắt đầu phiên làm việc, server gửi public key cho client, client sinh ra một session key và mã hóa bằng public key của server và gửi về server. Server giải mã bằng private key và nhận được session key. Session key được sử dụng để trao đổi dữ liệu giữa hai máy. 

#### Mã hóa (Encryption)

Sau khi thiết lập phiên làm việc bảo mật, dữ liệu trao đổi qua đường truyền được mã hóa và giải mã theo cơ chế đã thỏa thuận giữa client-server trước đó, thường do client quyết định.

Một số cơ chế mã hóa : 3DES, IDEA và Blowfish 

#### Chứng thực (Authentication ) 
Việc chứng thực bằng username/password là một cách thông dụng để định danh người sử dụng 

Bên cạnh đó có một vài cách khác : chứng thực rhosts (kiểm tra máy trạm được liệt kê trong file rhosts), chứng thực RSA (sử dụng ssh-keygen, ssh-agent)

<a name="algorithm"></a>
## 3. Một số thuật toán sử dụng trong SSH 
#### Những thuật toán sử dụng cho Public key

- **RSA**: tính toán không đối xứng, bắt nguồn từ sự phân tích thành thừa số của nhiều số nguyên là tích của 2 số nguyên tố gần bằng nhau
- **DSA**: thuật toán chữ ký số, dựa vào tính toán riêng rẽ các logarit trong một trường có giới hạn
- **Diffie-Hellman**: thuật toán thỏa thuận khóa, cũng dựa vào sự rời rạc của bài toán logarit 

#### Những thuật toán sử dụng cho Private key

- **IDEA**: thuật toán mã hóa dữ liệu bí mật quốc tế 
- **AES**: chuẩn mã tiên tiến 
- **DES**: chuẩn mã dữ liệu
- **3DES**: là dạng khác của DES để tăng tính bảo mật bằng việc tăng chiều dài khóa 
- **RC4**: dùng cho bảo mật dữ liệu RSA, mã hóa nhanh nhưng không bảo mật bằng những thuật toán khác
- **Blowfish**: từng bước thay thế DES, nhanh hơn DES và IDEA nhưng không bằng RC4

#### Những hàm băm 

- **CRC-32**: hàm băm không mã hoá đối với việc dò tìm lỗi thay đổi dữ liệu
- **MD5**: Message Digest algorithm number 5, thuật toán băm 128 bit
- **SHA-1**: Secure Hash Algorithm 1, thuật toán băm 160 bit. SSH-2 sử dụng SHA-1 để băm MAC, SSH-1 sử dụng MD5 
- **RIPEMD-160**: là một bản khác của MD4,được dùng trong các bản bổ sung của OpenSSH

<a name="install"></a>
## 4. Cài đặt và cấu hình 

Trên hệ thống linux đã cài đặt sẵn OpenSSH và cấu hình để xác thực theo password.

Nếu hệ thống chưa có xem thêm [tại đây](https://github.com/locvx1234/SSH/blob/master/ssh_config.md) 

<a name="use"></a>
## 5. Sử dụng 

Với người dùng linux có thể sử dụng Terminal để ssh tới máy khác :

	# ssh username@ip_server

Với người dùng Windows, ta sử dụng [PuTTY](http://www.putty.org/)

<img src="http://i.imgur.com/QfLTwyL.png">

Nhập `hostname` và `Open`, lưu ý là `Connection type` là `SSH`

<a name="wireshark"></a>
## 6. Bắt gói tin SSH

Sử dụng Wireshark bắt gói tin

<img src="http://i.imgur.com/2IbhL7x.png">

Một gói tin SSHv2 

<img src="http://i.imgur.com/NaJNJWn.png">

Luồng TCP bị mã hóa

<img src="http://i.imgur.com/Y5q6sgj.png">

<a name="reference"></a>
## 7. Tham khảo

https://vi.wikipedia.org/wiki/SSH

http://sinhvienit.net/forum/chuyen-de-tim-hieu-ssh.10058.html


