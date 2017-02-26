
# Redis
Redis全称: REmote DIctonary Server

redis-server  Redis服务器  
redis-cli  Redis命令行客户端  
redis-benchmark Redis性能测试工具  
redis-check-aof AOF 文件修复工具  
redis-check-dump RDB文件检查工具  
redis-sentinel 哨兵服务器(2.8以后)  

redis默认端口 6379  

启动redis服务器  
redis-server /path/to/redis.conf --port 6380 --loglevel waring  

Redis提供了一个配置文件模板redis.conf,在源码的根目录中  
Redis在运行时可以通过CONFIG  SET命令在不重新启动Redis的情况下动态修改部分redis配置  
使用CONFIG GET命令获取配置信息

Redis默认支持16个数据库, 可以通过配置参数databases来修改这一数字,
客户端与Redis连接后会自动选择0号数据库,不过随时使用SELECT命令更换数据库  

停止Redis: 
redis-cli SHUTDOWN  
或者 kill Redis的PID



redis远程连接: redis-cli -h host -p port -a password

Redis支持五种数据类型：string（字符串），hash（哈希），list（列表），set（集合）及zset(sorted set：有序集合)。

TTL: Time To Live redis缓存生存时间

```bash
# redis常用命令
keys 获取符合规则的键名列表
exists 判断一个键名是否存在
del 删除键
type 获取键值的数据类型

incr key_name
incrby key_name
incrbyfloat key_name
```

## 6: Lua脚本
redis.call()


## 7: 持久化
### RDB方式
RDB方式的持久化是通过快照(snapshotting)完成的,当符合一定条件时Redi会在以下几种情况下对数据进行快照
1. 根据配置规则进行自动快照
2. 用户执行save或bgsave命令
3. 执行flushall命令
4. 执行复制(replication)时.



### AOF方式

