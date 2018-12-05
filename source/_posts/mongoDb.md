---
title: mongoDb
date: 2018-12-05 19:11:41
tags:
categories: mogondb
---

### update

**类型**

| Type                    | Number | Alias                 |               Notes |
| :---------------------- | :----: | :-------------------- | ------------------: |
| Double                  |   1    | “double”              |                     |
| String                  |   2    | “string”              |                     |
| Object                  |   3    | “object”              |                     |
| Array                   |   4    | “array”               |                     |
| Binary data             |   5    | “binData”             |                     |
| Undefined               |   6    | “undefined”           |         Deprecated. |
| ObjectId                |   7    | “objectId”            |                     |
| Boolean                 |   8    | “bool”                |                     |
| Date                    |   9    | “date”                |                     |
| Null                    |   10   | “null”                |                     |
| Regular Expression      |   11   | “regex”               |                     |
| DBPointer               |   12   | “dbPointer”           |         Deprecated. |
| JavaScript              |   13   | “javascript”          |                     |
| Symbol                  |   14   | “symbol”              |         Deprecated. |
| JavaScript (with scope) |   15   | “javascriptWithScope” |                     |
| 32-bit integer          |   16   | “int”                 |                     |
| Timestamp               |   17   | “timestamp”           |                     |
| 64-bit integer          |   18   | “long”                |                     |
| Decimal128              |   19   | “decimal”             | New in version 3.4. |
| Min key                 |   -1   | “minKey”              |                     |
| Max key                 |  127   | “maxKey”              |                     |

**更新操作**

id 字段，一旦设定，你不能更新id字段,你也不能用有不同 id字段值的替换文档来替换已经存在的文档。并且id字段始终是文档中的第一个字段

> `db.collection.updateOne()` : 即使可能有==多个文档==通过过滤条件匹配到，但是也最多也==只更新一个==文档

> `db.collection.updateMany()`: 更新所有==通过==过滤条件匹配的文档

> `db.collection.update()`:即使可能有多个文档通过过滤条件匹配到，但是也最多也只==更新==或者==替换==一个文档。默认只更新一个文档。要更新多个文档，请使用 **multi**选项。

> `db.collection.save()`: 如果集合内部已经存在一个相同的id的记录，则会替换已经存在的那条记录。如果不存在，则会插入文档

```
db.users.update(
   { "favorites.artist": "Pisanello" },
   {
     $set: { "favorites.food": "pizza", type: 0,  },
     $currentDate: { lastModified: true }
   },
   { multi: true }
)
```

`db.collection.update(criteria,objNew,upsert,multi)`

```
criretia:查询条件
objNew:update对象和一些更新操作符
upsert：默认是false.如果不存在update的记录，时候插入objNew这个新的文档，true为插入。
multi:默认是false.只更新找到的第一条记录。如果为true,把按条件查询出来的记录全部更新
```

| 更新操作符                   | 作用描述                                                     |
| ---------------------------- | ------------------------------------------------------------ |
| $inc   {$incl:{field:value}} | 对一个数字字段的某个field增加value                           |
| $set {$set: {field:value } } | 将文档中的某个字段field的值设为value                         |
| $unset  {$unset:{field:1}}   | 删除某个字段                                                 |
| $push {$push:{field:value}}  | 将value追加到field(数组)里,不存在则会插入$p                  |
| $pushAll                     | 追加多个值到一个数组字段中                                   |
| $addToset                    | 加一个值到数组内，而且只有当这个值在数组中不存在时才增加     |
| {$pop:{field:1(-1)}}         | 删除数组内的一个值，-1表示删除数组内的第一个值，1表示最后一个值 |
| {${pull:{field:value}}}      | 从数组中删除一个等于value的值                                |
| $pushAll                     | 一次删除数组中的多个值                                       |
| {$rename:{old:new}}          | 对字段进行重命名                                             |

 **文档替换**   `db.collection.replaceOne`

需要传递一个全新的文档(除id 字段外：id字段是不变的，不能修改，如果包含了id字段，它的值必须与当前的值相同)

```java
db.users.replaceOne(
    {name:"abc"},
    { name: "amy", age: 34, type: 2, status: "P", favorites: { "artist": "Dali", food: "donuts" } }
)
    
db.users.update(
   { name: "xyz" },
   { name: "mee", age: 25, type: 1, status: "A", favorites: { "artist": "Matisse", food: "mango" } }
)
```

