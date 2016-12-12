
### 参考资料
官方网站: http://www.fabfile.org/
Github:   https://github.com/fabric/fabric


### 安装fabric
pip install fabric
easy_install fabric


### fab命令的常用参数
* **-l** 显示定义好的任务函数名;
* **-f** 指定fab入口文件, 默认入口文件名为fabfile.py;
* **-g** 指定网关(中转)设备, 比如堡垒机环境, 填写堡垒机IP即可;
* **-H** 指定目标主机, 多台主机用 逗号 , 分隔;
* **-P** 以异步并行方式运行多主机任务, 默认为串行运行;
* **-R** 指定role(角色), 以角色名区分不同业务组设备;
* **-t** 设置设备连接超时时间(秒);
* **-T** 设置远程主机命令执行超时时间(秒);
* **-w** 当命令执行失败, 发出告警, 而非默认中止任务.


### 全局属性设定
* **env.hosts**
* **env.exclude_hosts** 排除指定主机, 如: env.exclude_hosts=['192.168.1.22']
* **env.user** 定义用户名, 如: env.user="root"
* **env.port** 定义目标主机端口, 默认为22, 如: env.port="22"
* **env.password** 定义密码, 如: env.password="123456"
* **env.passwords** 与password功能一样, 区别在于不同主机不同密码的应用场景, 需要注意的是, 配置passwords时需要配置用户, 主机, 端口等信息, 如:
```python
env.passwords = {
    'root@192.168.1.21:22' : '123456',
    'root@192.168.1.22:22' : '654321',
    'root@192.168.1.23:22' : '321654',
}
```
* **env.gateway** 定义网关(中转, 堡垒机)IP, 如 env.gateway = '192.168.1.23'
* **env.deploy_release_dir** 自定义全局变量, 格式: env.+'变量名称', 如: env.deploy_release_dir, env.age, env.sex等
* **env.roledefs** 定义角色分组, 比如web组与db组主机区分开来, 定义如下:
```python
env.roledefs = {
    'webservers' : ['192.168.1.21','192.168.1.22','192.168.1.23'],
    'dbservers'  : ['192.168.1.24','192.168.1.25','192.168.1.26']
}
```
引用时使用Python修饰符的形式进行, 如:
```python
@roles('webservers')
def webtask():
    run('/etc/init.d/nginx start')

@roles('webservers','dbservers')
def publictask():
    run('uptime')
```


### 常用API
* **local** 执行本地命令, 如: local('uname -s');\
* **lcd** 切换本地目录, 如: lcd('/home');
* **cd** 切换远程目录, 如: cd('/data/logs')
* **run** 执行远程命令, 如: run('free -m');
* **sudo** sudo方式执行远程命令, 如: sudo('/etc/init.d/httpd start');
* **put** 上传本地文件到远程主机, 如: put('/home/user.info', '/data/user.info');
* **get** 从远程主机下载文件到本地, 如: get('/data/user.info', '/home/root.info');
* **prompt** 获得用户输入信息, 如: prompt('please input user password');
* **confirm** 获得提示信息确认, 如: confirm('Tests failed. Continue[Y/N]?');
* **reboot** 重启远程主机, 如: reboot();
* **@task** 函数修饰符, 标示的函数为fab可调用的, 非标记对fab不可见, 纯业务逻辑;
* **@runs_once** 函数修饰符, 标示的函数只会执行一次, 不受多台主机影响.