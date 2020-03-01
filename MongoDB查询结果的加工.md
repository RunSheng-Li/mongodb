### MongoDB查询结果的加工



##### 格式化地显示数据

```
# 查询结果“漂亮”显示
db.teacher.find().pretty()
```



##### 更多查询结果的加工

```
# 查询结果按年龄降序排列（1为升序）
db.teacher.find().sort({"age":-1})

# 查询结果统计条数
db.teacher.find().count()

# 查询结果取前三个数据
db.teacher.find().limit(3)

# 查询结果跳过前三个
db.teacher.find().skip(3)
```



##### 获取分页数据

```
# 查询结果跳过前三个取三个
# 每页3个数据，取第二页数据
# db.teacher.find().skip(3).limit(3)
db.teacher.find().skip(3).limit(3).pretty()
```

