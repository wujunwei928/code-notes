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