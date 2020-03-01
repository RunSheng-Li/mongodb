### Python与MongoDB的交互



##### 安装并引入依赖

- Python与MongoDB的交互可以通过第三方类库pymongo实现；
- pymongo的安装及引入：

```
pip3 install pymongo
```

```
import pymongo
```



##### 一般访问流程

- 建立Python到MongoDB的连接；
- 指定要访问的数据库和集合；
- 通过集合执行MongoDB指令；
- 结果的二次处理与输出；
- 断开连接；



##### 添加数据

```

# 连接MongoDB数据库
conn = pymongo.MongoClient(
    # 配置主机和端口
    host="localhost", port=27017
)

# 指定要操作的数据库名
db = conn.mydb
# 指定要操作的集合名
collection = db.student

# 插入一个数据文档
collection.insert(
    {"name": "sirouyang", "age": 18, "gender": 1, "address": "广州市", "isDelete": 0}
)
# 插入多个数据文档
collection.insert([
    {"name": "小马哥", "age": 50, "gender": 1, "address": "大深圳", "isDelete": 0},
    {"name": "jackma", "age": 55, "gender": 1, "address": "杭州市", "isDelete": 0}
])
print("插入成功！")

# 关闭连接
conn.close()

```



##### 查询数据

```

# 创建连接
conn = pymongo.MongoClient(
    host="127.0.0.1", port=27017
)

# 指定要操作的数据库与集合
db = conn.mydb
collection = db.student

# 查询文档个数
ret = collection.find().count()
print(ret)

# 查询全部
ret = collection.find()

# 查询年龄大于18的数据
ret = collection.find(
    {"age": {"$gt": 18}}
)

# 查询年龄大于18且家住北京的数据
ret = collection.find(
    {
        "age": {"$gt": 18},
        "address": "北京"
    }
)

# 查询年龄大于40的，或30以下的硅谷人士
ret = collection.find(
    {
        "$or": [
            {"age": {"$gt": 40}},
            {"age": {"$lt": 30}, "address": "硅谷"}
        ]
    }
)

# 查询结果按姓名降序排列
ret = collection.find().sort("name", pymongo.ASCENDING)

# 取前5个文档
ret = collection.find().limit(5)

# 查询第二页的三个文档
ret = collection.find().skip(3).limit(3)
for item in ret:
    print(type(item), item)

# 断开连接
conn.close()


```



##### 修改数据

```

# 建立数据库连接
conn = pymongo.MongoClient(
    host="127.0.0.1", port=27017
)

# 指定数据库与集合
db = conn.mydb
collection = db.student

# 执行更新：查询姓名为jobs的文档，姓名修改为"Steve Jobs"，年龄减小20岁
ret = collection.update(
    {"name": "jobs"},
    {
        "$set": {"name": "Steve Jobs"},
        "$inc": {"age": -20}
    }
)
print(ret)

# 断开连接
conn.close()


```



##### 删除数据

```

# 建立与MongoDB的连接
conn = pymongo.MongoClient(
    host="127.0.0.1", port=27017
)

# 指定数据库与集合
db = conn.mydb
collection = db.student

# 移除文档：移除年龄在55以上的文档数据
ret = collection.remove(
    {"age": {"$gt": 55}}
)
print(ret)

# 断开连接
conn.close()


```

