/*----------------------*/
CENTOS IP: 192.168.1.13
#INSTALL
	yum install vsftpd ftp -y
#Configure vsftpd
	vi /etc/vsftpd/vsftpd.conf
	/*------------*/
	## Disable anonymous login ##
	anonymous_enable=NO
	## Uncomment - Enter your Welcome message - This is optional ##
	ftpd_banner=Welcome to FTP
	## Enable the userlist 
	userlist_enable=YES
	## Configure the userlist to act as a whitelist (only allow users who are listed there)
	userlist_deny=NO
	## Allow the local users to login to the FTP (if they're in the userlist)
	local_enable=YES
	## Set Dictory Home
	local_root= /home/terdy/www/cnet
	/*------------*/
#Configure user list login
	vi /etc/vsftpd/user_list
#Enable and start the vsftpd service
	systemctl enable vsftpd
	systemctl start vsftpd
#Allow the ftp service and port 21 via firewall
	firewall-cmd --permanent --add-port=21/tcp
	firewall-cmd --permanent --add-service=ftp
#Restart firewall
	firewall-cmd --reload
#Update the SELinux boolean values for FTP service
	setsebool -P tftp_home_dir on
#TEST
