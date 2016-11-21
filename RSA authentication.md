Việc chứng thực bằng password của ssh có một vấn đề là trong phiên kết nối đầu tiên với server, kẻ tấn công có thể giả mạo server để tạo kết nối tới chính client.

Do đó, ở lần kết nối đầu tiên, ta luôn nhận được một cảnh báo 

<img src="http://i.imgur.com/JSIfL0S.png">

Các lần kết nối sau, key của server sẽ được cache lại, cảnh báo sẽ không xuất hiện nữa. 

Một cách chứng thực khác cho phép chúng ta không phải nhập password mỗi khi bắt đầu phiên kết nối, đó là sử dụng key.

`private key` nằm ở, `public key` nằm ở server.

Cách tạo key có thể thực hiện ở server hoặc client. Thông thường, ta sử dụng client tạo cặp key và gửi public cho server, giữ lại thành phần private key.

## Linux 

Gen key:

	# ssh-keygen –t rsa –b 1024

Sử dụng đường dẫn mặc định để tạo file. Nếu bạn muốn bảo mật hơn, hãy nhập passphrase còn không thì enter.

<img src="http://i.imgur.com/ob1mG0R.png">

Cặp key sẽ được tạo trong thư mục /root/.ssh :

<img src="http://i.imgur.com/gJOKLDG.png">

Private-key là `id_rsa` và public-key là `id_rsa.pub`

Để bảo mật cho key, ta chuyển `id_rsa` vào 	`/home/username/.ssh/id_rsa`

<img src="http://i.imgur.com/TkeHrK9.png">

Đồng thời sửa file ssh_config : 

	# vi /etc/ssh/ssh_config
	
Đổi đường dẫn của IdentityFile cho đúng

<img src="http://i.imgur.com/by4KYb6.png">

Đẩy public key cho server

	# ssh usersvr@ip_server cat < /path/to/id_rsa.pub ">" /home/usersvr/.ssh/authorized_keys

Thay đổi permission như sau : 

	# chmod 700 ~/.ssh
	# chmod 600 ~/.ssh/authorized_keys
	# chown $USER:$USER ~/.ssh -R
	
	
Cấu hình server

	# vi /etc/ssh/sshd_config
	
	PubkeyAuthentication yes
	AuthorizedKeysFile .ssh/authorized_keys
	
Sau đó restart lại sshd

	# systemctl restart sshd


Chứng thực thành công :

<img src="http://i.imgur.com/Hpu7iNx.png">
	

## Windows 

Sử dụng một phần mềm có tên Putty Key Generator (PuTTYgen) để tạo và sử dụng key.

<img src="http://i.imgur.com/EXpnelx.png"> 

Chọn `Generate` và rê chuột lòng vòng trên cửa sổ phần mềm để tạo key.

Lưu file public-key dưới tên `authorized_keys` và copy sang server theo đường dẫn `.ssh/authorized_keys` 

Chú ý : File public-key khi dùng PuTTYgen có dạng : 

	---- BEGIN SSH2 PUBLIC KEY ----
	Comment: "rsa-key-20161121"
	AAAAB3NzaC1yc2EAAAABJQAAAQEAuA84TJosM/Pqj7LaonMcjjJl3h/Zhk5LxO/r
	Z9+B/XiWWrR8cBL0f4iOgzDh/a3rSrpI5rjpGV8ep/I0PShc0qK3ko3mC86N0vPz
	MSHpuCB1O+yqqNwimS1GThRt6qV405pwIA7Tdqk/84a5thTmBD5bKXcSVWSfYOn7
	0kK2oTN0wJn9cJA5SQlWd9lWKNHnUqvwJMVW1l2k2pExbpM/0YyWewjW6htyQ3Yy
	Ahvy9W6SUxj3ktwRVPEvh8SgVnEF7eUefthuWucPgdGssTTYhK42AeZu0HkWypxc
	BLNBe2A7lRkT0glzzd2WbRryogREnJoht9Gx1twNjNVp1zJirQ==
	---- END SSH2 PUBLIC KEY ----
	
Chúng ta sẽ phải sửa lại về dạng `ssh-rsa` + key trên cùng 1 dòng

	ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAuA84TJosM/Pqj7LaonMcjjJl3h/Zhk5LxO/rZ9+B/XiWWrR8cBL0f4iOgzDh/a3rSrpI5rjpGV8ep/I0PShc0qK3ko3mC86N0vPzMSHpuCB1O+yqqNwimS1GThRt6qV405pwIA7Tdqk/84a5thTmBD5bKXcSVWSfYOn70kK2oTN0wJn9cJA5SQlWd9lWKNHnUqvwJMVW1l2k2pExbpM/0YyWewjW6htyQ3YyAhvy9W6SUxj3ktwRVPEvh8SgVnEF7eUefthuWucPgdGssTTYhK42AeZu0HkWypxcBLNBe2A7lRkT0glzzd2WbRryogREnJoht9Gx1twNjNVp1zJirQ==

Trên server :

Thay đổi permission như sau : 

	# chmod 700 ~/.ssh
	# chmod 600 ~/.ssh/authorized_keys
	# chown $USER:$USER ~/.ssh -R
	
Sửa file cấu hình

	# vi /etc/ssh/sshd_config
	
	PubkeyAuthentication yes
	AuthorizedKeysFile .ssh/authorized_keys

Truy cập từ Windows vào server ta dùng PuTTY
	
Ta dùng PuTTY để ssh vào server,

Connection/SSH/Auth và Browse tới file Private-key vừa tạo. Ở đây là pri.ppk

<img src="http://i.imgur.com/kxoMSWD.png">

Sau đó vào Session và điền hostname để kết nối 

<img src="http://i.imgur.com/GtSc3Rl.png">

