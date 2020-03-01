### mongodb基本操作



##### 数据库操作

- 注意:MongoDB的指令都是严格区分大小写的;
- win环境下数据库路径要提前创建好，MongoDB的bin目录要加入环境变量；

```
# 开启MongoDB服务
mongod --dbpath=D:\iWorkspace\data\MongoDB\mytest\db

# 启动MongoDB数据库
mongo

# 查看所有数据库
show dbs

# 切换数据库（不存在时创建，但只有插入集合后才会显示）
use mydb

# 显示当前数据库名
db
db.getName()

# 查看帮助
help

# 退出MongoDB
exit
```



##### 集合操作

- 显示所有集合

```
# 显示所有集合
show collections

# 创建新的集合
db.createCollection("teacher")

# 删除集合
db.teacher.drop()
```



##### 文档操作

- 插入文档

```
# 插入一个文档
db.teacher.insert(
    {"name":"bill","age":60,"gender":1}
)

# 一次性插入多个文档
db.teacher.insert([
    {"name":"jobs","gender":1,"words":"stay hungry,stay foolish"},
    {"name":"jackma","gender":1,"words":"我最后悔的事情就是创建了阿里"}
])

# 没有指定文档的id时,save的功能和insert一致
db.teacher.save(
    {"name":"十三姨","gender":0,"words":"...","age":25}
)
db.teacher.save([
    {"name":"阿三","gender":1,"words":"上海的发展水平快要赶上孟买了"},
    {"name":"小四","gender":0,"words":"我堪称是当代文坛的巨人"}
])
```

- 删除文档

```
# 删除指定条件的文档
# {"justOne":1}只删除一个，为0时代表所有符合条件的全删除
db.teacher.remove({"name":"bill"},{"justOne":1})
```

- 修改文档

```
# 修改name为jackma的文档的name为杰克马
db.teacher.update(
    {"name":"jackma"},
    {$set:{"name":"杰克马"}}
)

# 修改name为杰克马的文档的age，增加10岁
db.teacher.update(
    {"name":"杰克马"},
    {$inc:{"age":10}}
)

# 年龄为0的，设置为18，作用于全部文档
db.teacher.update(
    {"age":0},
    {$set:{"age":18}},
    {"multi":1}
)
```

- 查询文档

```
# 查询所有
db.teacher.find()

# 查询性别为0的文档，显示name和gender
db.teacher.find(
    {"gender":0},
    {"name":1,"gender":1}
)

# 查询性别为0的文档，显示_id以外的所有字段
db.teacher.find(
    {"gender":0},
    {"_id":0}
)

# 查询一条性别为0的文档，显示_id以外的所有字段
db.teacher.findOne(
    {"gender":0},
    {"_id":0}
)
```

