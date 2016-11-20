Chứng thực bằng username và password là cách phổ biến nhất để định danh người dùng. Mặc định cấu hình đã cho phép chứng thực bằng password, tuy nhiên ta có thể cấu hình thêm các tùy chọn khác bằng cách chỉnh sửa file cấu hình.

	# vi /etc/ssh/sshd_config 
	
Cổng truy cập 

	Port 22
	
Bật/tắt cho phép root đăng nhập (yes/no)

	PermitRootLogin yes
	
Không chấp nhận tài khoản có password để trống 

	PermitEmptyPassword no

Phải nhập password xác thực

	PasswordAuthentication yes

Cấm nhóm người dùng

	DenyGroups g1 g2
	
Cho phép nhóm người dùng
	
	AllowGroups g1 g2
	
Cho phép người dùng

	AllowUsers u1 u2 
	
Sau khi sửa file cấu hình, ta phải restart lại dịch vụ 

	# systemctl restart sshd


	