## 使用nginx的必备软件
1. GCC编译器
   GCC是必须的编译工具, 如果使用C++来编写Nginx HTTP模块, 需要安装G++编译器  
   yum install -y gcc
   yum install -y gcc-c++
2. PCRE库(Perl Compatible Regular Expressions, Perl兼容正则表达式)
   nginx的HTTP模块需要用它来解析正则表达式
   yum install -y pcre pcre-devel
3. zlib库
   zlib库用于对HTTP包的内容做gzip格式的压缩, 减少网络传输量
   yum install -y zlib zlib-devel
4. OpenSSL开发库
   OpenSSL用于支持Https, 或者 MD5, SHA1等散列函数
   yum install -y openssl openssl-devel


## Nginx的命令行控制
1. 默认方式启动 
   /usr/local/nginx/sbin/nginx 使用默认路径下的配置文件

2. 另行制定配置文件的启动方式
   /usr/local/nginx/sbin/nginx -c /tmp/nginx.conf

3. 另行制定安装目录的启动方式
   /usr/local/nginx/sbin/nginx -p /usr/local/nginx

4. 另行制定全局配置项的启动方式
   /usr/local/nginx/sbin/nginx -g "pid /var/nginx/test.pid"

5. 测试配置信息是否有错误


6. 在测试阶段不输出信息


7. 显示nginx版本信息
   /usr/local/nginx/sbin/nginx -v

8. 显示编译阶段的参数
   /usr/local/nginx/sbin/nginx -V

9. 快速的停止服务


10. 优雅的停止服务


11. 使运行中的Nginx重读配置项并生效


12. 日志文件回滚


13. 平滑升级Nginx


14. 显示命令行帮助