```python
# 创建es连接
es = Elasticsearch([
    {'host': '127.0.0.1'},
])

# 添加es文档
doc = {
    'author': 'kimchy',
    'text': 'Elasticsearch: cool. bonsai cool.',
    'timestamp': datetime.now(),
}
res = es.index(index="stat-gid-group", doc_type='gidGroup', id=1, body=doc)
print(res['created'])

# 更新文档(添加或更新字段age, 将之设置为18)
res = es.update(
    index = "stat-gid-group",
    doc_type = "gidGroup",
    id = es_id,
    body = {"script" : 'ctx._source.age = 18'}
);

# 删除文档
res = es.delete(
    index = "stat-gid-group",
    doc_type = "gidGroup",
    id = 1,
);
```