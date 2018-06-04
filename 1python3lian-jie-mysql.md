#### 1.下载并引入MySQL模块

```
pip install PyMySQL
import pymysql
```

2.测试数据库连接

```py
# -*- coding:utf-8 -*-
import pymysql
# 打开数据库连接
db = pymysql.connect(host,"songyaofeng","@#93529#@","demo" )
# 使用 cursor() 方法创建一个游标对象 cursor
cursor = db.cursor()

# 使用 execute()  方法执行 SQL 查询
sql = 'show databases'
cursor.execute(sql)

# 使用 fetchone() 方法获取单条数据.
databases = cursor.fetchall()

for database in databases:
    print('dbname: %s'%database)

# 关闭数据库连接
db.close()
```



