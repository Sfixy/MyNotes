# MongoDB

## 概念

| sql术语/概念 | MongoDB术语/概念 |              解释/说明               |
| :----------: | :--------------: | :----------------------------------: |
|   database   |     database     |                数据库                |
|    table     |    collection    |            数据库表/集合             |
|     row      |     document     |           数据记录行/文档            |
|    column    |      field       |             数据字段/域              |
|    index     |      index       |                 索引                 |
| table joins  |                  |           表连接，嵌入文档           |
| primary key  |   primary key    | 主键，MongoDB自动将_id字段设置为主键 |

### 查看数据库

```mongodb
> show dbs # 查看所有数据库
admin   0.000GB
config  0.000GB
local   0.000GB
runoob  0.000GB
test    0.000GB


> db  # 查看当前使用的数据库
test
```

### 连接数据库

```mongodb
> use test # 连接到一个指定的数据库
switched to db test
```

### 文档

文档是一组键值对（key-value）对（即BSON）。

1. 文档中的键/值对是有序的。
2. 文档中的值不仅可以是在双引号里面的字符串，还可以是其他几种数据类型（甚至可以是整个嵌入的文档)。
3. MongoDB区分类型和大小写。
4. MongoDB的文档不能有重复的键。
5. 文档的键是字符串。除了少数例外情况，键可以使用任意UTF-8字符。

文档键命名规范：

- 键不能含有\0 (空字符)。这个字符用来表示键的结尾。
- .和$有特别的意义，只有在特定环境下才能使用。
- 以下划线"_"开头的键是保留的(不是严格要求的)。

### 集合

集合是MongoDB的文档组，类似于sql的表。可以将不同数据类型的文档插入到集合里面。

### 元数据

数据库的信息是存储在集合中。它们使用了系统的命名空间

### MongoDB数据类型

| 数据类型           | 描述                                                         |
| :----------------- | :----------------------------------------------------------- |
| String             | 字符串。存储数据常用的数据类型。在 MongoDB 中，UTF-8 编码的字符串才是合法的。 |
| Integer            | 整型数值。用于存储数值。根据你所采用的服务器，可分为 32 位或 64 位。 |
| Boolean            | 布尔值。用于存储布尔值（真/假）。                            |
| Double             | 双精度浮点值。用于存储浮点值。                               |
| Min/Max keys       | 将一个值与 BSON（二进制的 JSON）元素的最低值和最高值相对比。 |
| Array              | 用于将数组或列表或多个值存储为一个键。                       |
| Timestamp          | 时间戳。记录文档修改或添加的具体时间。                       |
| Object             | 用于内嵌文档。                                               |
| Null               | 用于创建空值。                                               |
| Symbol             | 符号。该数据类型基本上等同于字符串类型，但不同的是，它一般用于采用特殊符号类型的语言。 |
| Date               | 日期时间。用 UNIX 时间格式来存储当前日期或时间。你可以指定自己的日期时间：创建 Date 对象，传入年月日信息。 |
| Object ID          | 对象 ID。用于创建文档的 ID。                                 |
| Binary Data        | 二进制数据。用于存储二进制数据。                             |
| Code               | 代码类型。用于在文档中存储 JavaScript 代码。                 |
| Regular expression | 正则表达式类型。用于存储正则表达式。                         |

#### ObjectId

唯一主键，含有时间戳

```mongodb
> var newObject = ObjectId()  # 文档创建时间
> newObject.getTimestamp()
ISODate("2020-11-16T03:15:20Z")

> newObject.str  # 转成字符串
5fb1eec8e9e6827ed801232e
```

#### 字符串

BSON字符串都是UTF-8编码

#### 日期

日期有符号，负数代表1970年之前的日期

```mongodb
> var mydate1 = new Date()  //格林尼治时间
> mydate1
ISODate("2020-11-16T03:19:23.028Z")
> var mydate2 = new ISODate()  //格林尼治时间
> var mydate2
> mydate2
ISODate("2020-11-16T03:20:09.609Z")
> typeof mydate1
object
> typeof mydate2
object
```

上述为日期类型

JS中的Date类型方法，返回一个时间事件类型的字符串

```mongodb
> var mydate1str = mydate1.toString()
> mydate1str
Mon Nov 16 2020 11:19:23 GMT+0800
> typeof mydate1str
string

or

> Date()
Mon Nov 16 2020 11:23:58 GMT+0800
```



## MongoDB连接

```mongodb
net start mongodb    //启动mongodb服务
net stop mongodb     //停止mongodb服务

mongo //启动mongodb
```

## MongoDB创建数据库

语法：

```mongodb
use DATABASE_NAME
```

数据库不存在，创建数据库，否则指向数据库

```mongodb
> use runoob
switched to db runoob
> db
runoob
> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
runoob  0.000GB
test    0.000GB
```

## MongoDB删除数据库

语法：

```mongodb
db.dropDatabase()
```

删除当前数据库。

```mongodb
> use runoob
switched to db runoob
> db.runoob.find().pretty()
> db
runoob
> db.dropDatabase()
{ "dropped" : "runoob", "ok" : 1 }
> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
test    0.000GB
```

### 删除集合

语法：

```mongodb
db.collection.drop()
```

删除集合site

```mongodb
> use runoob
switched to db runoob
> db.createCollection("site")  //创建集合，类似于表
{ "ok" : 1 }
> show tables
site
> db.runoob.drop()
false
> db.site.drop()
true
> show tables
```

## MongoDB创建集合

用法：

```mongodb
db.createCollection(name,options)
```

```mongodb
> use test
switched to db test
> db.createCollection("runoob") #创建集合
{ "ok" : 1 }

> db.createCollection("mycol",{capped:true,autoIndexId:true,size:6142800,max:10000})

        "note" : "The autoIndexId option is deprecated and will be removed in a future release",
        "ok" : 1
}

> db.mycol2.insert({"name":"菜鸟教程"})  # 没有集合自动创建
WriteResult({ "nInserted" : 1 })
```

## MongoDB删除集合

用法：

```mongo
db.collection.drop()
```

成功删除返回true，失败返回false

```mongodb
> db               
test               
> show collections 
col                
mycol              
mycol2             
runoob             
> db.mycol2.drop() # 删除集合
true               
> show collections 
col                
mycol              
runoob             
```

## MongoDB插入文档

语法：

```mongodb
db.collection_name.insert(document)  # 只能插入数据
or
db.collection_name.save(document)  # 主键存在更新数据，不存在插入数据
```

```mongodb
> db.col.insert({title:'MongoDB教程',
...     description:'MongoDB是一个Nosql数据库',
...     by:'菜鸟教程',
...     url:'http://www.runoob.com',
...     tags:['mongodb','database','NoSql'],
...     likes:100
... })
WriteResult({ "nInserted" : 1 })
> db.col.find()
{ "_id" : ObjectId("5fb1e4c2e9e6827ed801232d"), "title" : "MonogoDB", "descriptionL" : "MongoDB 是一个Nosql数据库", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "mongodb",
"database", "NoSQL" ], "likes" : 100 }
{ "_id" : ObjectId("5fb23c1173fe909033373bcf"), "title" : "MongoDB教程", "description" : "MongoDB是一个Nosql数据库", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "mongodb",
 "database", "NoSql" ], "likes" : 100 }
> document=({
...     title:'MongoDB教程',
...     description:'MnogoDB是一个NOsql数据库',
...     by:'菜鸟教程',
...     url:'http://www.runoob.com',
...     tags:['mongodb','database','NoSql'],
...     likes:100
... })

        "title" : "MongoDB教程",
        "description" : "MnogoDB是一个NOsql数据库",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "mongodb",
                "database",
                "NoSql"
        ],
        "likes" : 100
}
> db.col.insert(document)
WriteResult({ "nInserted" : 1 })
```

## MongoDB更新文档

update()和save()

语法：

```mongodb
db.collection.update(
	<query>,
	<update>,
	{
		upsert:<boolean>,
		multi:<boolean>,
		writeConcern:<document>
	}
)
```

```mongodb
> db.col.insert({title:'MongoDB教程',
...     description:'MongoDB是一个Nosql数据库',
...     by:'菜鸟教程',
...     url:'http://www.runoob.com',
...     tags:['mongodb','database','NoSql'],
...     likes:100
... })
WriteResult({ "nInserted" : 1 })
```

## MongoDB删除文档

语法：

```mongodb
db.collection.remove(
	<qurey>,
	<justone>
)

2.5之后
db.collection.remove(
   <query>,
   {
     justOne: <boolean>,
     writeConcern: <document>
   }
)
```

```mongodb
> db.col.find()
{ "_id" : ObjectId("5fb4bbb0861868f75fa09362"), "title" : "MongoDB教程", "description" : "MongoDB是一个Nosql数据库
", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "monogdb", "database", "NoSql" ], "likes" : 100
}
{ "_id" : ObjectId("5fb4bbb6861868f75fa09363"), "title" : "MongoDB教程", "description" : "MongoDB是一个Nosql数据库
", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "monogdb", "database", "NoSql" ], "likes" : 100
}
> db.col.remove({'title':'MongoDB教程'})
WriteResult({ "nRemoved" : 2 }) //删除两条记录
> db.col.find()                       
```

justOne设为1,删除一条找到记录

```monogdb
db.COLLECTION_NAME.remove(DELETION_CRITERIA,1)
```

清空 数据：

```mongodb
>db.col.remove({})
>db.col.find()
```

**remove（）函数不会清空磁盘空间，需要进行如下操作回收磁盘空间**

```mongodb
db.repairDatabase()
```

**目前采用deleteOne()和deleteMany()删除并释放空间**

```mongodb
> db.col.deleteMany({title:'MongoDB'})  # 删除所有title为MongoDB的文档
{ "acknowledged" : true, "deletedCount" : 1 }
> db.col.find()
{ "_id" : ObjectId("5fb4bf0c861868f75fa09364"), "title" : "MongoDB教程", "description" : "MongoDB是一个Nosql数据库
", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "monogdb", "database", "NoSql" ], "likes" : 100
}
{ "_id" : ObjectId("5fb4bf0e861868f75fa09365"), "title" : "MongoDB教程", "description" : "MongoDB是一个Nosql数据库
", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "monogdb", "database", "NoSql" ], "likes" : 100
}
{ "_id" : ObjectId("5fb4bf2c861868f75fa09366"), "title" : "MongoDB教程", "description" : "MongoDB是一个Nosql数据库
", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "monogdb", "database", "NoSql" ], "likes" : 100
}


> db.col.delectMany({})  # 删除所有文档
uncaught exception: TypeError: db.col.delectMany is not a function :
@(shell):1:1
> db.col.deleteMany({})
{ "acknowledged" : true, "deletedCount" : 3 }
> db.col.find()
```

## MonogoDB查询文档

find()方法查询文档，非结构化的方式显示

语法：

```mongodb
db.collection.find(query,projection)

db.collection.find().pretty() //格式化显示文档
```

```mongodb
> db.col.find().pretty()                             
                                                     
 )      "_id" : ObjectId("5fb4c0f5861868f75fa09368"),
        "title" : "MongoDB教程",                       
        "description" : "MongoDB是一个Nosql数据库",        
        "by" : "菜鸟教程",                               
        "url" : "http://www.runoob.com",             
        "tags" : [                                   
                "monogdb",                           
                "database",                          
                "NoSql"                              
        ],                                           
        "likes" : 100                                
}                                                    
```

| 操作       | 格式                     | 范例                                        | RDBMS中的类似语句       |
| :--------- | :----------------------- | :------------------------------------------ | :---------------------- |
| 等于       | `{<key>:<value>`}        | `db.col.find({"by":"菜鸟教程"}).pretty()`   | `where by = '菜鸟教程'` |
| 小于       | `{<key>:{$lt:<value>}}`  | `db.col.find({"likes":{$lt:50}}).pretty()`  | `where likes < 50`      |
| 小于或等于 | `{<key>:{$lte:<value>}}` | `db.col.find({"likes":{$lte:50}}).pretty()` | `where likes <= 50`     |
| 大于       | `{<key>:{$gt:<value>}}`  | `db.col.find({"likes":{$gt:50}}).pretty()`  | `where likes > 50`      |
| 大于或等于 | `{<key>:{$gte:<value>}}` | `db.col.find({"likes":{$gte:50}}).pretty()` | `where likes >= 50`     |
| 不等于     | `{<key>:{$ne:<value>}}`  | `db.col.find({"likes":{$ne:50}}).pretty()`  | `where likes != 50`     |

### mongoDB AND 条件

```mongodb
db.collection.find({key1:value1,key2:value2}).pretty()
```

示例：

```mongodb
>db.col.find({title:'MongoDB教程',by:'菜鸟教程'}).pretty()

        "_id" : ObjectId("5fb4c0f5861868f75fa09368"),
        "title" : "MongoDB教程",
        "description" : "MongoDB是一个Nosql数据库",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "monogdb",
                "database",
                "NoSql"
        ],
        "likes" : 100
}
```

类似于WHERE语句：WHERE by='菜鸟教程' AND title='MongoDB教程'

### MongoDB OR条件

```mongodb
>db.col.find(
   {
      $or: [
         {key1: value1}, {key2:value2}
      ]
   }
).pretty()
```

示例：查询键By为菜鸟教程或者title值为MongoDB教程的文档

```mongodb'
 db.col.find(
...     {
...         $or:
...         [
...             {
...                 by:'菜鸟教程'
...             }
...             ,
...             {
...                 title:'MongoDB教程'
...             }
...         ]
...     }
... ).pretty()

        "_id" : ObjectId("5fb4c0f5861868f75fa09368"),
        "title" : "MongoDB教程",
        "description" : "MongoDB是一个Nosql数据库",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "monogdb",
                "database",
                "NoSql"
        ],
        "likes" : 100
}
```

### AND和OR联合使用

```mongodb
db.col.find(
        {
            likes:{$gt:50},  //AND操作
            $or://OR
            [
                {
                    'by':'菜鸟教程'
                }
                ,
                {
                    'title':'MongoDB教程'
                }
            ]
        }
).pretty()
```

类似于sql:where likes>50 AND (by='菜鸟教程' OR title='MongoDB教程')

### projection参数指定是否要显示的键

显示：

```mongodb
db.col.find(
    {
        title:'MongoDB教程'
    }
    ,
    {
        title:1,
        by:1
    }
).pretty()  // inclusion模式 指定返回的键，不返回其他键（1）


        "_id" : ObjectId("5fb4c0f5861868f75fa09368"),
        "title" : "MongoDB教程",
        "by" : "菜鸟教程"
}
```

不显示：

```mongodb
> db.col.find(
...     {
...         likes:{$gt:50}
...     }
...     ,
...     {
...         title:0,
...         by:0
...     }
... ).pretty()  // exclusion模式 指定不返回的键,返回其他键（0）

        "_id" : ObjectId("5fb4c0f5861868f75fa09368"),
        "description" : "MongoDB是一个Nosql数据库",
        "url" : "http://www.runoob.com",
        "tags" : [
                "monogdb",
                "database",
                "NoSql"
        ],
        "likes" : 100
```

**主键默认返回，需要主动指定才能隐藏,inclusion模式时可以指定_id为0**

```mongodb
> db.col.find(
...     {
...         title:'MongoDB教程'
...     }
...     ,
...     {
...         _id:0,
...         title:1,
...         by:1
...     }
... ).pretty()
{ "title" : "MongoDB教程", "by" : "菜鸟教程" }
```

**两种模式不能混用**

```mongodb
db.col.find(
    {
        likes:{$gt:50}
    }
    ,
    {
        title:0,
        by:1
    }
).pretty()
//报错
Error: error: {
        "ok" : 0,
        "errmsg" : "Cannot do inclusion on field by in exclusion projection",
        "code" : 31253,
        "codeName" : "Location31253"
```

**不想指定query可以用 {}代替，但是要指定projection参数**

```mongodb
> db.col.find(
...     {},
...     {
...         _id:0,
...         title:1
...     }
... )
{ "title" : "MongoDB教程" }
```

likes大于50小于120查询条件

```mongodb
> db.col.find(
...     {
...         likes:{$gt:50, $lt:120}
...     },
...     {
...         likes:1
...     }
... )
{ "_id" : ObjectId("5fb4c0f5861868f75fa09368"), "likes" : 100 }
```

## MongoDB条件操作符

