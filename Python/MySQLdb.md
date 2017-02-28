
```python
import MySQLdb
import MySQLdb.cursors
import pandas
from pandas import DataFrame,Series

# 获取数据库连接, 
# 设置 cursorclass = MySQLdb.cursors.DictCursor 是使查询的每行结果是字典格式, 否则每行的查询结果是tuple格式, 只能用数字 0, 1, 2...获取元素
mysql_conn = MySQLdb.connect(host='localhost', user='root', passwd='root', db='blog', cursorclass = MySQLdb.cursors.DictCursor)
mysql_cursor = mysql_conn.cursor()
mysql_cursor.execute('select * from article')
article_results = mysql_cursor.fetchall()
# article_results_df = DataFrame(list(article_results))    # fetchall()获取的查询结果是tuple, 需要先转成list, 转成DataFrame
article_list = dict(map(lambda x : (x['id'], x['name']), article_results))
```