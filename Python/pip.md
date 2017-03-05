
### 安装 pip
wget https://bootstrap.pypa.io/get-pip.py -O - | python

### 设置pip的pypi镜像地址
因为大天朝墙的原因, 官方默认的pypi源速度比较慢, 可以设置国内的pypi源地址, 提高安装python包时的速度。

下面以设置清华大学的pypi源地址为例说明: 
1. 临时使用
```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
# 注意，simple 不能少, 是 https 而不是 http
```
2. 设为默认
修改 ~/.pip/pip.conf (没有就创建一个)， 修改 index-url至tuna，例如
```bash
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```

