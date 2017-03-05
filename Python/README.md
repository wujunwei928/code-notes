
# 教程
Python 3 Module of the Week: https://pymotw.com/3/
Python 2 Module of the Week: https://pymotw.com/2/
Ansible 中文权威指南：http://www.ansible.com.cn/
Scrapy 0.24中文文档：http://scrapy-chs.readthedocs.io/zh_CN/0.24/
Tornado 中文文档： http://demo.pythoner.com/itt2zh/
requests库学习文档: http://cn.python-requests.org/zh_CN/latest/index.html

# 大牛博客
董伟明 - <python web开发实战>作者: http://www.dongwm.com/blog/archives/


# 相关文章
pexpect模块使用说明: http://www.jianshu.com/p/cfd163200d12
supervisor 初体验: http://www.jianshu.com/p/9abffc905645
python多版本管理工具pyenv:  https://github.com/yyuu/pyenv/
安装pyenv依赖项: https://github.com/yyuu/pyenv/wiki/Common-build-problems
linux下Python多版本管理(pyenv): http://my.oschina.net/lionets/blog/267469


安装用户自定义python的最简便方法, 使用使用一站安装包Anaconda: 
Anaconda官网:  https://www.continuum.io/downloads
虽然上面介绍了可以自定义python package安装路径, 可以在用户自己家用pyenv安装多版本python
但是这些有一个前提, 就是需要gcc, zlib-devel bzip2 bzip2-devel 等许多依赖项
但是有时, 我们只是服务器上的一个普通用户, 没有超级用户权限, 无法安装相关依赖项, 
比如说我想在公司跳板机上使用python的自动化运维工具包fabric, 安装过程会超级麻烦
这是Anaconda就派上用场了, 它把所有的依赖管理都帮你处理好了, 安装完之后有了一个用户级别的python环境
这时再安装fabric就非常简单了,  pip install fabric


# Jupyter
jupyter支持的编程语言kennel列表: https://github.com/ipython/ipython/wiki/IPython-kernels-for-other-languages
jupyter同时支持python2 和 python3: https://ipython.readthedocs.io/en/latest/install/kernel_install.html