> mongo中的一条记录称作一个文档，所以增加是增加文档。文档是增加到集合（相当于表）中的。一个集合中包含了多条文档。

# 数据库操作

```sql
//创建数据库test
use test;
//展示所有库 此时是看不到test这个库的，因为test里面没有任何数据
show dbs
//插入数据
db.book.insertOne({"title":"Stand by Me"})
//展示所有库 数据库列表中出现了test库
show dbs
```

`use`的作用：如果数据库不存在，则创建数据库，否则切换到指定数据库。

新创建的数据库不会再数据库的列表中出现，要显示它，需要向数据库test插入一些数据。

> **注意:** *在 MongoDB 中，集合只有在内容插入后才会创建! 就是说，创建集合(数据表)后要再插入一个文档(记录)，集合才会真正创建。*

```sql
//创建集合
db.createCollection("user")
//展示集合
show collections
//删除集合
db.user.drop()
//删除数据库
db.dropDatabase()
```



# 增

```sql
//插入单个文档，会自动生成_id
db.movies.insertOne({"title":"Stand by Me"})

// 删除movies集合
db.movies.drop()

//插入多条记录
db.movies.insertMany([{"title":"Ghostbusters"},{"title":"E.T."},{"title":"Blade Runner"}])

//查找数据
db.movies.find()

// 按照顺序插入，则第三个开始往后的都无法插入
db.movies.insertMany([{"_id":0,"title":"Top Gun"},{"_id":1,"title":"Back to the Future"},{"_id":1,"title":"Gremlins"},{"_id":2,"title":"Aliens"}],{"ordered":true})

// 不按照顺序插入，则只有第三个因为_id重复了无法插入，其他文档都会成功插入
db.movies.insertMany([{"_id":0,"title":"Top Gun"},{"_id":1,"title":"Back to the Future"},{"_id":1,"title":"Gremlins"},{"_id":2,"title":"Aliens"}],{"ordered":false})
```



# 删

```sql
//删除一条文档
db.movies.deleteOne({"_id":2})
//按照条件删除
db.movies.deleteMany({"opt-out":true})
//删除所有文档
db.movies.deleteMany({})
//清空整个集合
db.movies.drop()
```



# 改

```sql
db.movies.insertOne({"url":"example-domain","pageviews":52})
//更新 pageviews加1
db.movies.updateOne({"url":"example-domain"},{"$inc":{"pageviews":1}})

db.users.insertOne({"name":"joe","age":30,"sex":"male","location":"Wisconsin"})
//增加或修改字段 favourite book
db.users.updateOne({"_id":ObjectId("637605cbd0a86e4a63277d67")},{"$set":{"favourite book":"War and Peace"}})
//修改键的类型
db.users.updateOne({"name":"joe"},{"$set":{"favourite book":["Cat's Cradle","Foundation Trilogy","Ender's Game"]}})
//删除键
db.users.updateOne({"name":"joe"},{"$unset":{"favourite book":1}})
```

> 除了$unset，还有递增和递减操作：$inc，$inc可以接受正数和负数，接收的是负数相当于减。

修改内嵌文档

```sql
> db.blog.posts.findOne()
{
    "_id" : ObjectId("4b253b067525f35f94b60a31"),
    "title" : "A Blog Post",
    "content" : "...",
    "author" : {
        "name" : "joe",
        "email" : "joe@example.com"
    }
}
> db.blog.posts.updateOne({"author.name" : "joe"},
... {"$set" : {"author.name" : "joe schmoe"}})

> db.blog.posts.findOne()
{
    "_id" : ObjectId("4b253b067525f35f94b60a31"),
    "title" : "A Blog Post",
    "content" : "...",
    "author" : {
        "name" : "joe schmoe",
        "email" : "joe@example.com"
    }
}
```



# 查

```sql

```

