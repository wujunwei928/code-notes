
# 简介
虚拟环境是 Python 解释器的一个私有副本,在这个环境中你可以安装私有包,而且不会影响系统中安装的全局 Python 解释器。

虚拟环境非常有用,可以在系统的 Python 解释器中避免包的混乱和版本的冲突。为每个程序单独创建虚拟环境可以保证程序只能访问虚拟环境中的包,从而保持全局解释器的干净整洁,使其只作为创建(更多)虚拟环境的源。使用虚拟环境还有个好处,那就是不需要
管理员权限。

虚拟环境使用第三方实用工具 virtualenv 创建。输入以下命令可以检查系统是否安装了virtualenv :
```bash
$ virtualenv --version
```
如果结果显示错误,你就需要安装这个工具。

Python 3.3 通过 venv 模块原生支持虚拟环境,命令为 pyvenv 。 pyvenv 可以替代 virtualenv 。  
不过要注意,在 Python 3.3 中使用 pyvenv 命令创建的虚拟环境不包含 pip ,你需要进行手动安装。    
Python 3.4 以后 改进了这一缺陷, pyvenv 完全可以代替 virtualenv

# 安装
```bash
# ubuntu 安装
sudo apt-get install python-virtualenv

# easy_install 安装
sudo easy_install virtualenv

# pip 安装
pip install virtualenv
```

# 使用
```bash
# 创建一个名叫 venv 的虚拟环境
virtualenv venv

# 激活虚拟环境
# Linux，Mac
source venv/bin/activate
# Windows
venv\Scripts\activate

# 退出虚拟环境
deactivate
```
