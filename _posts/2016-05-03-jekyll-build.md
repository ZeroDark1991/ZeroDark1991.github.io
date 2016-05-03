---
layout: post
title: 日常技巧笔记
description: 常用到的一些知识或技巧的笔记...
---

## #加速Github

    185.31.16.184 github.global.ssl.fastly.net
    写入 /etc/hosts 文件
    
# Node----    
## #npm 淘宝镜像
    --registry=http://registry.npm.taobao.org
    
飞一般的感觉
## #nvm--Node版本管理


**安装nvm**

dir为安装的路径

	$ cd dir
	$ git clone https://github.com/cnpm/nvm.git

.zshrc中添加

	source ~/dir/nvm/nvm.sh
	
**安装任意版本的node**

	$ nvm install 4.0.0
	
**使用**

	$ nvm use v4.0.0

# SSH----
--参考了阮一峰老师的文章

查看ssh目录

	$ whereis ssh


Mac系统中需要在系统设置中打开远程登录，步骤如下：

打开系统偏好设置 —— 共享，选中远程登录

## #ssh命令连接远程主机
	ssh user@host
	例：root@192.168.0.0
	
第一次连接


	$ ssh user@host
	The authenticity of host 'host (12.18.429.21)' can't be established.
	RSA key fingerprint is 98:2e:d7:e0:de:9f:ac:67:28:c2:42:2d:37:16:58:4d.
	Are you sure you want to continue connecting (yes/no)?　　

输入yes，然后是密码

	Are you sure you want to continue connecting (yes/no)? yes
	Password: (enter password)
		
## #公钥登录
省去每次连接输入密码的环节。

	$ ssh-keygen
		

运行上面的命令以后，一路回车。其中有一个问题是，要不要对私钥设置口令（passphrase），如果担心私钥的安全，这里可以设置一个。

运行结束以后，在$HOME/.ssh/目录下，会新生成两个文件：id_rsa.pub和id_rsa。前者是你的公钥，后者是你的私钥。
这时再输入下面的命令，将公钥传送到远程主机host上面：
	
	$ ssh-copy-id user@host

Mac系统下需要安装ssh-copy-id

	brew install ssh-copy-id
			

如果还是不行，就打开远程主机的/etc/ssh/sshd_config这个文件，检查下面几行前面"#"注释是否取掉。
	
	　　RSAAuthentication yes
	　　PubkeyAuthentication yes
	　　AuthorizedKeysFile .ssh/authorized_keys	　　	　　

要查看当前有多少个处于登录状态的用户，可以使用who命令查看。

## #scp				
scp命令可以在本地主机和远程主机之间传输文件
简单使用如下：

	$ scp fileName user@host:/Users/dir/