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

- (>) 大于 - $gt

- (<) 小于 - $lt

- (>=) 大于等于 - $gte

- (<= ) 小于等于 - $lte

- $ne ----------- not equal  !=

  $eq  --------  equal  =

### $gt操作符（大于）

likes大于100

```mongodb
db.col.find(
    {
        likes:{$gt:100}
    }
).pretty()


        "_id" : ObjectId("5fbb1ed02f3b3d8945cf2c71"),
        "title" : "PHP教程",
        "description" : "PHP是一种创建动态交互性站点的强有力的服务器脚本语言",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "php"
        ],
        "likes" : 200
}

        "_id" : ObjectId("5fbb1eee2f3b3d8945cf2c72"),
        "title" : "Java 教程",
        "description" : "Java 是由Sun Microsystems公司于1995年5月推出的高级程序设计语言。",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "java"
        ],
        "likes" : 150
}
```

### $gte操作符

大于等于100的集合

```mongodb
 db.col.find(
...     {
...         likes:{$gte:100}
...     }
... ).pretty()

        "_id" : ObjectId("5fbb1ed02f3b3d8945cf2c71"),
        "title" : "PHP教程",
        "description" : "PHP是一种创建动态交互性站点的强有力的服务器脚本语言",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "php"
        ],
        "likes" : 200
}

        "_id" : ObjectId("5fbb1eee2f3b3d8945cf2c72"),
        "title" : "Java 教程",
        "description" : "Java 是由Sun Microsystems公司于1995年5月推出的高级程序设计语言。",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "java"
        ],
        "likes" : 150
}

        "_id" : ObjectId("5fbb1efc2f3b3d8945cf2c73"),
        "title" : "MongoDB 教程",
        "description" : "MongoDB 是一个 Nosql 数据库",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "mongodb"
        ],
        "likes" : 100
}
```

### $lt小于操作符

小于150的记录

```mongodb
db.col.find(
...     {
...         likes:{$lt:150}
...     }
... ).pretty()

        "_id" : ObjectId("5fbb1efc2f3b3d8945cf2c73"),
        "title" : "MongoDB 教程",
        "description" : "MongoDB 是一个 Nosql 数据库",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "mongodb"
        ],
        "likes" : 100
}
```

### $lte小于等于操作符

小于等于150的记录

```mongodb
db.col.find(
...     {
...         likes:{$lte:150}
...     }
... ).pretty()

        "_id" : ObjectId("5fbb1eee2f3b3d8945cf2c72"),
        "title" : "Java 教程",
        "description" : "Java 是由Sun Microsystems公司于1995年5月推出的高级程序设计语言。",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "java"
        ],
        "likes" : 150
}

        "_id" : ObjectId("5fbb1efc2f3b3d8945cf2c73"),
        "title" : "MongoDB 教程",
        "description" : "MongoDB 是一个 Nosql 数据库",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "mongodb"
        ],
        "likes" : 100
}
```

### gt和lt一起使用

大于100，小于200

```mongodb
> db.col.find(                                                                
...     {                                                                     
...         likes:{$gt:100,$lt:200}                                           
...     }                                                                     
... ).pretty()                                                                
                                                                              
        "_id" : ObjectId("5fbb1eee2f3b3d8945cf2c72"),                         
        "title" : "Java 教程",                                                  
        "description" : "Java 是由Sun Microsystems公司于1995年5月推出的高级程序设计语言。",      
        "by" : "菜鸟教程",                                                        
        "url" : "http://www.runoob.com",                                      
        "tags" : [                                                            
                "java"                                                        
        ],                                                                    
        "likes" : 150                                                         
}                                                                     
```

查询 title 包含"教"字的文档：

```
db.col.find({title:/教/})
```

查询 title 字段以"教"字开头的文档：

```
db.col.find({title:/^教/})
```

查询 titl e字段以"教"字结尾的文档：

```
db.col.find({title:/教$/})
```

## MongoDB操作符-$type实例

如果想获取 "col" 集合中 title 为 String 的数据

```mongodb
> db.col.find({title:{$type:2}})
{ "_id" : ObjectId("5fbb1ed02f3b3d8945cf2c71"), "title" : "PHP教程", "description" : "PHP是一种创建动态交互性站点
的强有力的服务器脚本语言", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "php" ], "likes" : 200 }

{ "_id" : ObjectId("5fbb1eee2f3b3d8945cf2c72"), "title" : "Java 教程", "description" : "Java 是由Sun Microsystems
公司于1995年5月推出的高级程序设计语言。", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "java" ],
 "likes" : 150 }
{ "_id" : ObjectId("5fbb1efc2f3b3d8945cf2c73"), "title" : "MongoDB 教程", "description" : "MongoDB 是一个 Nosql 数
据库", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "mongodb" ], "likes" : 100 }

或

> db.col.find({title:{$type:'string'}})
{ "_id" : ObjectId("5fbb1ed02f3b3d8945cf2c71"), "title" : "PHP教程", "description" : "PHP是一种创建动态交互性站点
的强有力的服务器脚本语言", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "php" ], "likes" : 200 }

{ "_id" : ObjectId("5fbb1eee2f3b3d8945cf2c72"), "title" : "Java 教程", "description" : "Java 是由Sun Microsystems
公司于1995年5月推出的高级程序设计语言。", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "java" ],
 "likes" : 150 }
{ "_id" : ObjectId("5fbb1efc2f3b3d8945cf2c73"), "title" : "MongoDB 教程", "description" : "MongoDB 是一个 Nosql 数
据库", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "mongodb" ], "likes" : 100 }
```

## MongoDB Limit与Skip方法

### Limit方法

指定查询数据的数量

语法：

```mongodb
db.COLLECTION_NAME.find().limit(NUMBER)
```

查询文档中的两条记录

```mongodb
> db.col.find({},{title:1,_id:0}).limit(2)
{ "title" : "PHP教程" }
{ "title" : "Java 教程" }
```

**注：没有指定limit参数，默认返回所有记录**

### Skip方法

跳过指定数量的数据

语法：

```
db.COLLECTION_NAME.find().limit(NUMBER).skip(NUMBER)
```

跳过第一条记录

```mongodb
db.col.find({},{"title":1,_id:0}).limit(1).skip(1)
{ "title" : "Java 教程" }
```

**注：默认参数是0，一般不使用skip因为效率低下（一条条数数据）**

读取10条数据后的100条数据（跳过前10条，返回后100条）

```
db.COLLECTION_NAME.find().skip(10).limit(100)
```

**skip和limit执行顺序和所在位置无关**

```mongodb
> var arr = [];
>
> for(var i=1 ; i<=20000 ; i++){
...     arr.push({num:i});
... }
20000
>
> db.numbers.insert(arr);
BulkWriteResult({
        "writeErrors" : [ ],
        "writeConcernErrors" : [ ],
        "nInserted" : 20000,
        "nUpserted" : 0,
        "nMatched" : 0,
        "nModified" : 0,
        "nRemoved" : 0,
        "upserted" : [ ]
})
num大于45小于60
> db.numbers.find({$and:[{"num":{$lt:60}},{"num":{$gt:45}}]}).limit(7).skip(5);
{ "_id" : ObjectId("5fbb2b862f3b3d8945cf2ca6"), "num" : 51 }
{ "_id" : ObjectId("5fbb2b862f3b3d8945cf2ca7"), "num" : 52 }
{ "_id" : ObjectId("5fbb2b862f3b3d8945cf2ca8"), "num" : 53 }
{ "_id" : ObjectId("5fbb2b862f3b3d8945cf2ca9"), "num" : 54 }
{ "_id" : ObjectId("5fbb2b862f3b3d8945cf2caa"), "num" : 55 }
{ "_id" : ObjectId("5fbb2b862f3b3d8945cf2cab"), "num" : 56 }
{ "_id" : ObjectId("5fbb2b862f3b3d8945cf2cac"), "num" : 57 }

> db.numbers.find(
...     {
...         "num":{$gt:45,$lt:60}
...     }
... ).skip(5).limit(7)
{ "_id" : ObjectId("5fbb2b862f3b3d8945cf2ca6"), "num" : 51 }
{ "_id" : ObjectId("5fbb2b862f3b3d8945cf2ca7"), "num" : 52 }
{ "_id" : ObjectId("5fbb2b862f3b3d8945cf2ca8"), "num" : 53 }
{ "_id" : ObjectId("5fbb2b862f3b3d8945cf2ca9"), "num" : 54 }
{ "_id" : ObjectId("5fbb2b862f3b3d8945cf2caa"), "num" : 55 }
{ "_id" : ObjectId("5fbb2b862f3b3d8945cf2cab"), "num" : 56 }
{ "_id" : ObjectId("5fbb2b862f3b3d8945cf2cac"), "num" : 57 }
```

## MongoDB排序

### sort方法

在 MongoDB 中使用 sort() 方法对数据进行排序，sort() 方法可以通过参数指定排序的字段，并使用 1 和 -1 来指定排序的方式，其中 1 为升序排列，而 -1 是用于降序排列。

语法：

```mongodb
db.COLLECTION_NAME.find().sort({KEY:1})
```

col 集合中的数据按字段 likes 的降序排列：

```mongodb
> db.col.find({},{title:1,_id:0}).sort({likes:-1})
{ "title" : "PHP教程" }
{ "title" : "Java 教程" }
{ "title" : "MongoDB 教程" }
```

col 集合中的数据按字段 likes 的升序排列：

```mongodb
> db.col.find({},{title:1,_id:0}).sort({likes:1})
{ "title" : "MongoDB 教程" }
{ "title" : "Java 教程" }
{ "title" : "PHP教程" }
```

**skip、limit、sort执行顺序：先 sort(), 然后是 skip()，最后是显示的 limit()**

## MongoDB索引

**索引通常能够极大的提高查询的效率**，如果没有索引，MongoDB在读取数据时必须扫描集合中的每个文件并选取那些符合查询条件的记录。

这种扫描全集合的查询效率是非常低的，特别在处理大量的数据时，查询可以要花费几十秒甚至几分钟，这对网站的性能是非常致命的。

**索引是特殊的数据结构**，索引存储在一个易于遍历读取的数据集合中，索引是对数据库表中一列或多列的值进行排序的一种结构

### createIndex()方法

语法：

```mongodb
db.collection.createIndex(keys, options)
```

key创建索引字段，1升序排列，-1降序排列

```mongodb
> db.col.createIndex({"title":1})

        "createdCollectionAutomatically" : false,
        "numIndexesBefore" : 1,
        "numIndexesAfter" : 2,
        "ok" : 1
}
```

复合索引

```mongodb
> db.col.createIndex({"title":1,"description":-1})

        "createdCollectionAutomatically" : false,
        "numIndexesBefore" : 2,
        "numIndexesAfter" : 3,
        "ok" : 1
}
```

查看集合索引

```mongodb
> db.col.getIndexes()

        {
                "v" : 2,
                "key" : {
                        "_id" : 1
                },
                "name" : "_id_"
        },
        {
                "v" : 2,
                "key" : {
                        "title" : 1
                },
                "name" : "title_1"
        },
        {
                "v" : 2,
                "key" : {
                        "title" : 1,
                        "description" : -1
                },
                "name" : "title_1_description_-1"
        }
]
```

查看集合索引大小

```mongodb
> db.col.totalIndexSize()
77824
```

删除集合指定索引

```mongodb
db.col.dropIndex("索引名称")
```

```mongodb
> db.col.dropIndex("title_1")
{ "nIndexesWas" : 3, "ok" : 1 }
> db.col.getIndexes()

        {
                "v" : 2,
                "key" : {
                        "_id" : 1
                },
                "name" : "_id_"
        },
        {
                "v" : 2,
                "key" : {
                        "title" : 1,
                        "description" : -1
                },
                "name" : "title_1_description_-1"
        }
]
```

### MOngoDB聚合

处理数据（平均值，求和）

语法：

```mongodb
db.COLLECTION_NAME.aggregate(AGGREGATE_OPERATION)
```

```mongodb
db.col.aggregate(
    [{
        $group:{
            _id:'by_user',num_tutorial:{$sum:1}
        }
    }]
)

{ "_id" : "runoob.com", "num_tutorial" : 3 }
```

**聚合表达式**

| 表达式    | 描述                                           | 实例                                                         |
| :-------- | :--------------------------------------------- | :----------------------------------------------------------- |
| $sum      | 计算总和。                                     | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : "$likes"}}}]) |
| $avg      | 计算平均值                                     | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$avg : "$likes"}}}]) |
| $min      | 获取集合中所有文档对应值得最小值。             | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$min : "$likes"}}}]) |
| $max      | 获取集合中所有文档对应值得最大值。             | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$max : "$likes"}}}]) |
| $push     | 在结果文档中插入值到一个数组中。               | db.mycol.aggregate([{$group : {_id : "$by_user", url : {$push: "$url"}}}]) |
| $addToSet | 在结果文档中插入值到一个数组中，但不创建副本。 | db.mycol.aggregate([{$group : {_id : "$by_user", url : {$addToSet : "$url"}}}]) |
| $first    | 根据资源文档的排序获取第一个文档数据。         | db.mycol.aggregate([{$group : {_id : "$by_user", first_url : {$first : "$url"}}}]) |
| $last     | 根据资源文档的排序获取最后一个文档数据         | db.mycol.aggregate([{$group : {_id : "$by_user", last_url : {$last : "$url"}}}]) |

**管道：**

一个操作（管道）处理完 一条记录传递给下一个操作（管道）处理

$project示例：查询指定字段，id默认显示，也可以设置0取消id的显示 

```mongodb
db.col.aggregate(
...     {
...         $project:
...         {
...             title:1,
...             by_user:1
...         }
...     }
... )
{ "_id" : ObjectId("5fc7307f7ae3859efca8f295"), "title" : "MongoDB Overview", "by_user" : "runoob.com" }
{ "_id" : ObjectId("5fc730c57ae3859efca8f296"), "title" : "NoSQL Overview", "by_user" : "runoob.com" }
{ "_id" : ObjectId("5fc731137ae3859efca8f297"), "title" : "Neo4j Overview", "by_user" : "runoob.com" }
{ "_id" : ObjectId("5fc732a97ae3859efca8f298"), "title" : "Neo4j Overview", "by_user" : "neo4j" }
```

$match示例：比较数字大小，选取指定值。match处理完传递给group处理

```mongodb
db.col.aggregate(
...     [
...         {$match:{score:{$gt:10,$lt:750}}},
...         {$group:{_id:null,count:{$sum:1}}}
...     ]
... )
```

