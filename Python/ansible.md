# Ansible
---
Ansible一般使用ssh秘钥来连接远程服务器，但是有时可能不方便设置ssh私钥  
可以设置服务器用户名，密码登陆，但是需要先安装sshpass, 配置格式如下: 
[test] 
192.168.1.101 ansible_ssh_user=root ansible_ssh_pass=root_pwd


--- 
### 参考资料
[运维之路 - Ansible的安装](http://www.361way.com/ansible-install/4371.html)
[Ansible结合跳板机控制远程服务器](https://ouyang.me/blog/2015/08/31/using-ansible-with-a-bastion-host/)
[灿哥的Blog](http://www.shencan.net/)
