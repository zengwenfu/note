# mogodb简记

## 概念解析
1. 集合
芒果中的集合（collection）相当于关系型数据库中的表(table)
芒果中的文档（document）(json obj)相当于关系型数据库中的行（row）
芒果中的域(column)(json obj中的属性)相当于关系型数据库中的字段(field)

## 常用命令
1. 启动服务
```
    //进入bin，当然如果bin加入了环境变量，不需要这步操作
    cd [your mongo path]/bin
    
    //启动服务
    ./mongod 
    //如果启动不了，有可能是权限问题，可以试试sudo
    sudo ./mongod
```
2. 连接
```
    //默认连接localhost
    ./mongo 
    //使用用户名和密码连接登陆到指定数据库
    mongodb://admin:123456@localhost/test
```
3. 显示数据库
```
    //显示所有
    show dbs

    //显示当前
```
4. 创建或切换数据库
```
    use mydb
```
5. 删除数据库
```
    //先切换到需要删除的数据库
    //再执行
    db.dropDatabase()
```
6. 插入数据
```
    //如果集合col不存在则创建
    db.col.insert(obj);
```
7. 更新数据
```
    //第一个参数相当于where，第二个参数相当于set，只匹配第一条满足条件的数据
    db.col.update({'name': 'zeng'}, {$set: {'pass': 'abc'}});

    //修改所有where的匹配
    db.col.update({'name': 'zeng'}, {$set: {'pass': 'abc'}}，{'muti': true});

    //save替换
    db.col.save({
        "_id" : ObjectId("56064f89ade2f21f36b03136"),
        "title" : "MongoDB",
        "description" : "MongoDB 是一个 Nosql 数据库",
        "by" : "Runoob",
        "url" : "http://www.runoob.com",
        "tags" : [
                "mongodb",
                "NoSQL"
        ],
        "likes" : 110
    })
```
8. 删除数据
```
    //删除符合条件的所有
    db.col.remove({'name': 'zeng'});

    //删除符合条件的第一条
    db.col.remove({'name': 'zeng'}, 1);

    //删除所有
    db.col.remove();

```




