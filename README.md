# FTP服务的安装和配置

- ## 安装vsftpd服务组件

1. 打开终端，键入如下命令：

   ```
   apt-get install vsftpd
   ```

   ![image](https://github.com/xqcwjx/FTPInstallAndConfig/blob/master/image/1.jpg)

2. 安装完成后，会自动创建一个ftp用户，可以使用“passwd ftp”修改密码

   ```
   passwd ftp
   ```

   ![image](https://github.com/xqcwjx/FTPInstallAndConfig/blob/master/image/2.jpg)

3. 安装完成后，会自动创建“/srv/ftp”目录，可修改该目录操作权限方便之后操作

   ```
   chmod 777 /srv/ftp
   ```

- ## FTP文件配置

  1. 打开“/etc/vsftpd.conf”文件

     ```
     vim /etc/vsftpd.conf
     ```

  2. 查看文件内容，修改如下几项配置

     ```
     anonymous_enable=NO	#不允许匿名登陆
     local_enable=YES	#允许本地用户登陆
     write_enable=YES	#写权限（上传文件权限）
     chroot_local_user=YES	#将用户限制在主目录
     chroot_list_enable=YES	#启用限制用户名单       chroot_list_file=/etc/vsftpd.chroot_list	#限制用户名单
     pam_service_name=vsftpd
     ```

  3. 在“/etc/vsftpd.chroot_list”中添加限制用户

     ```
     vim /etc/vsftp.chroot_list
     ```

     ![image](https://github.com/xqcwjx/FTPInstallAndConfig/blob/master/image/3.jpg)

  4. 修改“/etc/pam.d/vsftp”

     ```
     vim /etc/pam.d/vsftpd
     ```

     注释掉“auth   required        pam_shells.so”，保存退出

     ![image](https://github.com/xqcwjx/FTPInstallAndConfig/blob/master/image/4.jpg)

- ## 启动FTP服务

  1. 键入如下命令，启动FTP服务

     ```
     service vsftpd start
     ```

     注：重启与关闭FTP服务命令如下

     ```
     service vsftpd start	#启动（开始）FTP服务
     service vsftpd restart	#重启FTP服务
     service vsftpd stop		#关闭FTP服务
     ```

  2. 查看进程

     ```
     ps -e | grep vsftpd
     ```

     ![image](https://github.com/xqcwjx/FTPInstallAndConfig/blob/master/image/5.jpg)

  3. 测试连接使用的是filezill，可以使用其他工具xftp、8uftp等等......

     ![image](https://github.com/xqcwjx/FTPInstallAndConfig/blob/master/image/6.jpg)

