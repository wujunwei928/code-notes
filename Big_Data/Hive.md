
```sql
add file a.py;
-- 系统默认的python,有可能有时没有安装你需要的模块, 可以自己使用add archive 命令上传一个python环境, 然后用下列方式使用你上传的自定义的python环境, 使用.tar.gz压缩文件失败, 改用.zip格式文件成功
add archive python.zip;
select transform(topic_id) using 'python.zip/miniconda2/bin/python a.py' as (topic_id) from test1;
```



