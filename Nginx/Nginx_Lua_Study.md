nginx lua模块官方文档 : https://www.nginx.com/resources/wiki/modules/lua/    
nginx lua模块Github地址 : https://github.com/openresty/lua-nginx-module  
OpenResty - 中文官方站 : http://openresty.org/cn/  
OpenResty最佳实践 : http://xuewb.com/index.html  
LuaJIT下载地址 :  http://luajit.org/download.html     
Lua简明教程 : http://coolshell.cn/articles/10739.html     
开涛Nginx+Lua开发教程 : http://jinnianshilongnian.iteye.com/category/333854      
Nginx中Lua内存共享字典变量 : http://blog.csdn.net/weiyuefei/article/details/38487475      

# 一.Nginx+Lua开发一站式解决方案OpenResty
如果本地电脑进行nginx + lua 开发测试的时候, 推荐使用OpenResty, 它将开发所需的lua和相关的lua包(比如cjson)进行了整合, 开箱即用  
中文官网: http://openresty.org/cn/


# 二.Nginx整合LuaJIT
如果你们的线上环境已经安装过nginx, 并且有自己开发的nginx模块, 那就不适合使用OpenResty, 可以通过整合
LuaJIT的功能使Nginx支持Lua开发,
如果需要lua的其他包, 如cjson等时, 需要额外安装 
### 1: 下载并安装配置LuaJIT
```bash
# 下载 LuaJIT
wget http://luajit.org/download/LuaJIT-2.0.4.tar.gz
tar -zxvf LuaJIT-2.0.4.tar.gz
cd LuaJIT-2.0.4
make install PREFIX=/usr/local/luajit
echo "/usr/local/luajit/lib" > /etc/ld.so.conf.d/usr_local_luajit_lib.conf
ldconfig
# 注意设置LuaJIT的环境变量!
export LUAJIT_LIB=/usr/local/luajit/lib
export LUAJIT_INC=/usr/local/luajit/include/luajit-2.0
```

### 2: 下载nginx_lua模块
```bash
# 下载nginx_lua模块
wget https://github.com/openresty/lua-nginx-module/archive/v0.10.6.tar.gz
tar -zxvf v0.10.6.tar.gz
# 下载NDK
# NDK(Nginx Development Kit)模块是一个拓展Nginx服务器核心功能的模块
# 第三方模块开发可以基于它来快速实现
# NDK提供函数和宏处理一些基本任务，减轻第三方模块开发的代码量。
wget https://github.com/simpl/ngx_devel_kit/archive/v0.3.0.tar.gz
tar -zxvf v0.3.0.tar.gz
```

### 3: 下载并安装编译nginx, 包含nginx lua模块
```bash
wget http://nginx.org/download/nginx-1.9.15.tar.gz
tar -zxvf nginx-1.9.15.tar.gz
cd nginx-1.9.15
./configure --add-module=/path/to/ngx_devel_kit-0.3.0/ --add-module=/path/to/lua-nginx-module-0.10.6/
make
make install
```


### 4: 测试nginx lua安装
```bash
# 添加nginx解析lua的相关配置
location = /lua-version { 
    content_by_lua ' 
        if jit then 
            ngx.say(jit.version) 
        else 
            ngx.say(_VERSION) 
        end 
    '; 
}


# 访问接口测试
curl http://127.0.0.1/lua-version
LuaJIT 2.0.2
```


### 5: nginx lua请求计数器相关配置
设置lua共享内存字典
```bash
# 定义到http模块内, 不知道能不能定义到request模块, 待验证
http {
    include       mime.types;
    default_type  application/octet-stream;

    # ngx_lua模块中的共享内存字典项API, 设置一个共享内存字典dogs, 供下面调用
    lua_shared_dict dogs 10m;

```

```bash
location = /test1 {
       content_by_lua_file conf/lua/hello.lua;
}

location = /test2 {
    # 自定义nginx变量
    set $param_one 'name';

    # 通过lua定义nginx变量
    set_by_lua $param_two 'return 2';
    set_by_lua $param_three '
        -- 这里要用lua注释, 获取上面定义的 nginx_lua 共享内存字典 dogs
        local dogs = ngx.shared.dogs
        local totalNum = dogs:get("totalNum");
        -- 如果变量未定义, 设置为1, 为了防止int超出lua的int范围, 当累积到一定值的时候, 重新从1开始计算
        if not totalNum or totalNum >= 8 then
                totalNum = 1
        else                    
                totalNum = totalNum + 1;
        end     
        dogs:set("totalNum", totalNum);
        -- 当能被4整除的时候, 返回false, 否则返回true
        if totalNum % 4 == 0 then return "false" else return "true" end;
    ';
    
    default_type application/json;
    expires 5m;        return 200 '{"param_one":"$param_one","param_two":$param_two,"param_three":$param_three}';
}

```


### 6: LuaJIT安装cjson
```bash
# 1: 下载lua的cjson模块
wget https://www.kyne.com.au/~mark/software/download/lua-cjson-2.1.0.tar.gz
tar -zxvf lua-cjson-2.1.0.tar.gz 
cd lua-cjson-2.1.0

# 2: 根据安装的LuaJIT地址, 修改Makefile中的LUA_INCLUDE_DIR参数
#    cjson的Makefile中有默认变量PREFIX=/usr/local
#    如果你的LuaJIT安装路径有/usr/local, 可以用$(PREFIX)代替, 如下
vi Makefile
LUA_INCLUDE_DIR = $(PREFIX)/luajit/include/luajit-2.0
LUA_INCLUDE_DIR = /usr/local/luajit/include/luajit-2.0

# 3: 编译
make
make install

# 执行完上面的步奏, LuaJIT即可支持cjson
```

### 7: 开发环境关闭lua程序缓存, 方便调试
使用nginx + lua 开发的时候,每次修改文件之后都需要重启nginx, 非常不爽(* ￣︿￣)
网上搜索可以通过设置 lua_code_cache 实现
lua_code_cache参数一般放在nginx.conf的http模块里面，设置lua程序是否缓存，默认是开启的，开发模式关闭即可：**lua_code_cache off;**



ubuntu下安装报错， 原因待查找

checking for md5 in system md library ... not found
checking for md5 in system md5 library ... not found
checking for md5 in system OpenSSL crypto library ... found
checking for sha1 in system md library ... not found