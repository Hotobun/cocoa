---
title: 阿里云
date: 2019-12-04 23:35:17
tags: linux
categories: 基础
cover: /img/aliyun.png
---

## sudo找不到命令
普通用户sudo的时候 找不到命令  
centos用户程序目录一般在/usr/local/bin/  
root用户的目录在/usr/bin  
sudo 不检查/usr/local/bin  
解决：  
```
which command  # 找出用户的命令路径  假设为 pwd  
sudo ln -s pwd /usr/bin/command     # 修改pwd 和command  
```

***
## centos安装python3
方向键乱码：  
`yum install readline-devel`
找不到ssl模块  
`yum install openssl-devel`
```
yilai bao  error:
    ModuleNotFoundError: No module named '_ctypes':
    yum install libffi-devel -y
```
官网下载包后 
```
./configure  # 检测环境
make 
make install 
```
安装完成

***
## ssh scp
ssh scp出现 Permission denied (publickey,gssapi-with-mic,gssapi-keyex)  
修改目标服务器中 /etc/ssh/sshd_config 中的参数：  
一般在文件最后面  
将PasswordAuthentication no中的“no”改为yes，如果有注释，将注释去掉  
之后service sshd restart重启sshd服务就可以了。  

***
## tcp转发
阿里云对外使用公网ip   
云主机网口是私网ip  
外部只能访问公网   
所以没有设置转发 外面tcp无法连通主机端口  
那么怎么办？  
nginx你值得拥有  
centos7系统 :  
```
编辑nginx配置文件 最后加上代码  
$ vim /etc/nginx/nginx.conf    
stream{
    server{
        listen 233;                  # 公网监听端口 转发到下面的端口
        proxy_pass：127.0.0.1：2333； # 公网233端口->内网2333端口
    }
}

$ sudo nginx -t        # 检查nginx配置信息
$ sudo nginx -s reload # 重启服务生效
```

