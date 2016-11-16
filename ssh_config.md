## Cài đặt :
Mặc định trên CentOS 7 và các distro khác đã cung cấp các gói cần thiết cho ssh. Nếu không có ta có thể cài đặt thêm :

	# yum install openssh openssh-server openssh-clients openssl-libs

##Cấu hình : 

File cấu hình mặc định của `sshd` ở đường dẫn `/etc/ssh/sshd_config`

Khuyến cáo : Nên tạo ra 1 bản copy file cấu hình để khôi phục khi cần 

	# cp /etc/ssh/sshd_config /etc/ssh/sshd_config.orig

Để view file cấu hình, ta sử dụng một editor như `vi`

	# vi /etc/ssh/sshd_config
	
Việc đầu tiên bạn cần làm là thay đổi số cổng của dịch vụ ssh. Theo mặc đinh, SSH lắng nghe ở cổng 22. Để an toàn hơn, bạn có thể thay đổi thành một con số khác. 

	# Port 22 
	
bỏ dấu comment # và sửa số port thành 

	Port 2016

Số port bạn chọn không được trùng với các dịch vụ đang chạy khác trên máy. 

Sau đó lưu và đóng file và restart lại SSH để cập nhật thay đổi :

	# systemctl restart sshd.service
	
Để đảm bảo an ninh hơn nữa, chúng ta nên sử dụng xác thực dựa trên `key-based`. Xác thực khóa cho phép bạn kết nối với máy chủ mà không sử dụng mật khẩu của user trong hệ thống. Thay vào đó sẽ cần key để sử dụng. Về chi tiết mình sẽ update sau.

Giao thức SSH cho phép các hoạt động khác như copy file giữa 2 máy theo hình thức mã hóa an toàn. Bạn có thể sử dụng `scp` hay `sftp`.