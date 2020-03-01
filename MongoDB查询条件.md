### MongoDB查询条件



##### 比较运算

- MongoDB中的比较运算包括： 大于`$gt`,大于等于`$gte`，小于`$lt`，小于等于`$lte`，等于`$eq`，不等于`$ne`；

```
# 查询年龄大于10的文档
db.teacher.find(
    {"age":{$gt:10}}
)
# 查询年龄大于等于10的文档
db.teacher.find(
    {"age":{$gte:10}}
)

# 查询年龄小于10的文档
db.teacher.find(
    {"age":{$lt:10}}
)
# 查询年龄小于等于10的文档
db.teacher.find(
    {"age":{$lte:10}}
)

# 查询年龄等于10的文档
db.teacher.find(
    {"age":{$eq:10}}
)
# 查询年龄不等于10的文档
db.teacher.find(
    {"age":{$ne:10}}
)
```



##### 条件与，条件或

```
# 18以上成年男子文档（条件与）
db.teacher.find(
    {"age":{$gte:18},"gender":1}
)

# 年龄在30到50之间的文档
db.teacher.find(
    {   "age":{'$gt':30,'$lt':50}    }
)

# 60以上或10岁以下文档（条件或）
db.teacher.find(
    {$or:[
        {"age":{$gte:60}},
        {"age":{$lte:10}}
    ]}
)

# 查询成年男子或老幼（与或结合使用）
db.teacher.find(
    {$or:[
        {"age":{$gte:18},"gender":1},
        {$or:[{"age":{$gte:60}},{"age":{$lte:10}}]}
    ]}
)
```

