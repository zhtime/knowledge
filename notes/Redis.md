# Redis知识

## Redis基础

**环境：Windows**

## 简介

### **问题现象**

- 海量用户
- 高并发



### **关系型数据库(罪魁祸首)**

- 性能瓶颈：磁盘IO性能低下
- 扩展瓶颈：数据关系复杂，扩展性差，不便于大规模集群



### **解决思路**

- 降低磁盘IO次数，越低越好
- 去除数据间的关系，越简单越好



## Nosql(Not-Only-Sql)

泛指非关系型数据库，作为关系型数据库的**补充**。

一般的数据还是要存到关系型数据库中(硬盘中)，而nosql是将数据存入到内存中。



作用：应用与海量用户和海量数据前提下的数据处理问题

特征：

- 可扩容，可伸缩
- 大数据下高性能
- 灵活的数据模型（应对多种类型数据）
- 高可用



### 常见的Nosql数据库：

- Redis
- MongoDB
- HBase



应用场景：

**解决方案一(电商场景)**

![image-20210713132608790](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210713132608790.png)



概念：Redis（Remote Dictionary Server）**高性能键值对(key -value)数据库**

特征：

- 数据间没有必然的关联关系
- 内部采用单线程机制进行工作
- 高性能
- 多数据类型支持
  - String类型
  - 数组类型List
  - 集合类型Set
  - 散列类型  hash表
  - 有序集合类型 sortedSet
- 持久化支持(**和java中将对象序列化相似，将对象存到硬盘中**)，进行数据灾难**(断电无法工作**)恢复



应用：

- **任务队列**（秒杀，抢购等）
- **时效性信息控制**(手机验证码时效性)
- 为热点数据加速查询
- 即时信息查询（排行榜信息，车来了公交信息，在线人数）
- 分布式数据共享
- 消息队列
- 分布式锁



## 基本操作

### **信息添加**

- 功能：设置key、value数据

- 命令

  ```linux
  set key  value
  ```

- 范例

  ```
  set name  zhang
  ```



### **信息查询**

- 功能:根据key查询对应的value，如果不存在，返回空(nil)

- 命令

  ```
  get key
  ```

- 范例

  ```
  get name
  ```

### **清屏**

- 命令

  ```
  ctrl L
  ```

### 帮助

- 功能： 获取帮助, 可以使用Tab键来切换 

  ```
  help 命令名称
  help @组名
  ```

![image-20210713135006738](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210713135006738.png)

### 退出

- 命令

  ```
  quit
  exit
  ```



## 数据类型

业务数据的特殊性

**作为缓存使用**

1. 原始业务功能设计
   - 秒杀
   - 618活动
   - 排队购票
2. 运行平台监控到突发的高频访问数据
   - 突发时事新闻
3. 高频，复杂的统计数据
   - 在线人数（直播）

**附加功能**

系统功能优化或升级

- 单服务器升级集群
- Session管理
- Token管理



### 常见数据类型

- string      String    
- hash       HashMap
- list            LinkedList
- set           HashSet
- sortedSet      TreeSet





redis自身是一个Map，按照key-value的形式存储数据。

数据类型指的是存储的数据类型，value中的数据类型，而key中的类型永远是String。

![image-20210713140204985](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210713140204985.png)

#### String类型

**基本操作**

```java
//设置String
set key value
//设置多个String
mset key1 value1 key2 value2...
//设置生命周期
setex key seconds value 

//得到String
get key 
//得到多个String
mget key1 key2...

//删除String
del key

//获取String的长度
strlen  key


//向字符串的后面追加字符，如果有就补在后面，如果没有就新建
append key value
```

 

![image-20210713141820575](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210713141820575.png)

小闹钟：发送和返回时间。

大闹钟：存储的时间。

使用单个set和单mset，最终所需时间如上图显示，在发送同等数据的情况下，使用mset更加的高效。



**扩展操作**

String作为**数值**操作

```java
//增长指令，只有当value为数字时才能增长
incr key  
incrby key increment   比如： incrby num 10 增加10
 
 //操作小数
incrbyfloat key increment  比如 ：incrbyfloat num 1.2

//减少指令，有当value为数字时才能减少
decr key  

//操作小数
decrby key increment

注意：increment可以为正数也可以为负数
```



- String在redis中默认是字符串类型，当遇到**incr**和**decr**操作时，会转换成数值进行计算。(**前提是存入的是数值类型的String**)

- redis所有的操作都是原子性的，采用单线程处理所有的业务，命令是一个一个执行，因此不需要考虑并发带来的影响。

  

**tips1：**

- redis用于控制数据库表主键id，为数据库表主键**提供生成策略**，保障数据库表的主键**唯一性**
- 此方案适用于所有数据库，且支持数据库集群



**业务场景：投票时间的限制**

```java
//设置数据的生命周期，单位 秒
setex key seconds value
//设置数据的生命周期，单位 毫秒
psetex key milliseconds value
```

 

**tips2**

- redis 控制数据的生命周期，通过数据是否失效控制业务行为，适用于所有具有时效性限定控制的操作



注意事项

![image-20210713144113836](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210713144113836.png)

key的设置约定

![image-20210713144710848](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210713144710848.png)

**tips3**

- redis运用于各种结构性和非结构型高热度数据访问加速



#### Hash类型

![image-20210713145212428](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210713145212428.png)

**基本操作**

```java
//插入（如果已存在同名的field，会被覆盖）
hset key field value
hmset key field1 value1 field2 value2...
//插入（如果已存在同名的field，不会被覆盖）
hsetnx key field value

//取出
hget key field
hgetall key

//获取多个数据
hmget key field1 field2


//删除
hdel key field1 field2...

//获取field数量
hlen key

//查看是否存在
hexists key field
```

**扩展操作**

```java
//获取哈希表中所有的字段名或字段值 
hkeys key
hvals key

//设置指定字段的数值数据增加指定范围的值 
hincrby key field increment 
hdecrby key field increment
```



**注意事项**

- hash类型下的value**只能存储字符串**，不允许存储其他数据类型，**不存在嵌套现象**。如果数据未获取到， 对应的值为（nil）
- 每个 hash 可以存储 2^32 - 1 个键值
- hash类型十分贴近对象的数据存储形式，并且可以灵活添加删除对象属性。但hash设计初衷不是为了存储大量对象而设计的，**切记不可滥用**，**更不可以将hash作为对象列表使用**
- hgetall 操作可以获取全部属性，如果内部field过多，遍历整体**数据效率就很会低**，有可能成为数据访问瓶颈 



 **应用场景**

电商网站购物车设计

![image-20210715130900678](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210715130900678.png)

```java
127.0.0.1:6379> hmset shop1 sp 10 sp2 1
OK
127.0.0.1:6379> hmset shop2 sp 1  sp 2
OK
127.0.0.1:6379> hgetall shop1
1) "sp"
2) "10"
3) "sp2"
4) "1"
127.0.0.1:6379> hgetall shop2
1) "sp"
2) "2"
```



![image-20210715132115181](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210715132115181.png)

```java
127.0.0.1:6379> hmset shop3 sp:name 101 sp:info {.....}
OK
127.0.0.1:6379> hgetall shop3
1) "sp:nums" //商品编号:数量
2) "101"    //数量
3) "sp:info"  //商品：信息
4) "{.....}"
```





#### List类型

- 数据存储需求：存储多个数据，并对数据进入存储空间的顺序进行区分
- 需要的存储结构：一个存储空间保存多个数据，且通过数据可以体现进入顺序
- list类型：保存多个数据，底层使用双向链表存储结构实现
- **元素有序，且可重**

![image-20210715133439471](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210715133439471.png)

![image-20210715133622532](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210715133622532.png)

```java
//添加修改数据,lpush为从左边添加，rpush为从右边添加
lpush key value1 value2 value3...
rpush key value1 value2 value3...

//查看数据, 从左边开始向右查看. 如果不知道list有多少个元素，end的值可以为-1,代表倒数第一个元素
//lpush先进的元素放在最后,rpush先进的元素放在最前面
lrange key start end
//得到长度
llen key
//取出对应索引的元素
lindex key index

//获取并移除元素（从list左边或者右边移除）
lpop key
rpop key
```



**扩展操作**

```java
//规定时间内获取并移除数据,b=block,给定一个时间，如果在指定时间内放入了元素，就移除
//key1,key2 :若干个列表
//timeout：单位：s
blpop key1 key2... timeout
brpop key1 key2... timeout

```



**业务场景**

 微信朋友圈点赞，按照点赞顺序显示点赞好友信息

操作具有先后的数据控制

```java
//移除指定元素 count:移除的个数 value:移除的值。 移除多个相同元素时，从左边开始移除
lrem key count value
```

```java
127.0.0.1:6379> rpush 01 a b c d e
(integer) 5
127.0.0.1:6379> lrange 01 0 -1
1) "a"
2) "b"
3) "c"
4) "d"
5) "e"
127.0.0.1:6379> lrem 01 1 a
(integer) 1
127.0.0.1:6379> lrange 01 0 -1
1) "b"
2) "c"
3) "d"
4) "e"
127.0.0.1:6379>
```



**注意事项**

- list中保存的数据都是string类型的，数据总容量是有限的，最多2^32 - 1 个元素 (4294967295)。
- list具有索引的概念，但是操作数据时通常以**队列**的形式进行入队出队(rpush, lpop)操作，或以**栈**的形式进行入栈出栈(lpush, lpop)操作
- 获取全部数据操作结束索引设置为-1 (倒数第一个元素)
- list可以对数据进行分页操作，通常第一页的信息来自于list，第2页及更多的信息通过数据库的形式加载

 

**日志的存储**

使用redis中List类型来完成。

队列的形式或者栈的形式完成顺序的存储。



#### Set类型

- 新的存储要求：存储大量的数据，在查询方面提供更高的效率
- 需要的存储结构：能够保存大量的数据，高效的内部存储机制，便于查询
- set类型：**与hash存储结构完成相同，不同之处在于key用来存值，而value不存值（nil）**，并且值是不允许重复的。

![image-20210715141512836](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210715141512836.png)

![image-20210715141528531](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210715141528531.png)

**基本操作**

```java
//添加元素
sadd key member1 member2...

//查看元素
smembers key

//移除元素
srem key member

//查看元素个数
scard key

//查看某个元素是否存在
sismember key member
```

​	

**扩展操作**

```java
//从set中任意选出count个元素.原set集合数量不变
srandmember key count

//从set中任意选出count个元素并移除，原set集合发生改变
spop key count
```



**业务场景**

![image-20210715142243834](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210715142243834.png)

```java
127.0.0.1:6379> srandmember users 3
1) "sh"
2) "js"
127.0.0.1:6379> srandmember users 1
1) "js"
127.0.0.1:6379> spop users
"js"
127.0.0.1:6379> srandmember users 2
1) "sh"
```

**应用于随机推荐类信息检索**，例如：热点歌单推荐。



![image-20210715143054724](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210715143054724.png)

```java
//求两个集合的交集、并集、差集
//交集
sinter key1 key2...
//并集
sunion key1 key2...
//差集
sdiff key1 key2...

//求两个set的交集、并集、差集，并放入另一个set中
sinterstore destination key1 key2...
sunionstore destination key1 key2...
sdiffstore destination key1 key2...

//求指定元素从原集合放入目标集合中
smove source destination key
```



**应用于同类信息的关联搜索，二度关联搜索，深度关联搜索**

一度搜索：显示共同好友、关注，

二度搜索：用户A发出，获取到好友用户B的游戏充值列表



统计网站的访问量(PV),独立访客(uv)，独立IP（ip）

建立string类型，利用incrby统计日访问量

建立Set类型，记录不同cookie数量

建立Set类型，统计不同IP数量

**应用于同类型数据的快速去重**





**注意事项**

- set类型不允许重复数据，已经存在的数据，不会允许后续相同数据加入进来。
- set与hash的存储结构相同，但是无法启用hash中存储值的空间。

  

#### Sortd_Set类型

- **不重但有序（score）**
- 新的存储需求：数据排序有利于数据的有效展示，需要提供一种可以根据自身特征进行**排序**的方式
- 需要的存储结构：新的存储模型，可以保存**可排序**的数据
- sorted_set类型：在set的存储结构基础上添加可排序字段

![image-20210716142345635](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210716142345635.png)

score关键字是**用来排序，并不是数据**



**基本操作**

```java
//插入元素, 需要指定score(用于排序)
zadd key score1 member1 score2 member2

//查看元素(score升序), 当末尾添加withscore时，会将元素的score一起打印出来
zrange key start end (withscore)
//查看元素(score降序), 当末尾添加withscore时，会将元素的score一起打印出来
zrevrange key start end (withscore)

//移除元素
zrem key member1 member2...
```

```java
127.0.0.1:6379> zadd scores 94 zs
(integer) 1
127.0.0.1:6379> zadd scores 80 ls
(integer) 1
127.0.0.1:6379> zadd scores 79 ww
(integer) 1
127.0.0.1:6379> zadd scores 22 zl
(integer) 1
127.0.0.1:6379> zrange scores 0 -1  withscores
1) "zl"
2) "22"
3) "ww"
4) "79"
5) "ls"
6) "80"
7) "zs"
8) "94"
127.0.0.1:6379> zrevrange scores 0 -1 withscores
1) "zs"
2) "94"
3) "ls"
4) "80"
5) "ww"
6) "79"
7) "zl"
8) "22"
127.0.0.1:6379> zrem socres zl
(integer) 0
127.0.0.1:6379> zrevrange scores 0 -1 withscores
1) "zs"
2) "94"
3) "ls"
4) "80"
5) "ww"
6) "79"
7) "zl"
8) "22"
```



```java
//按条件获取数据, 其中offset为索引开始位置，count为获取的数目
zrangebyscore key min max [withscore] [limit offset count]
zrevrangebyscore key max min [withscore] [limit offset count]

//按条件移除元素
zremrangebyrank key start stop
zremrangebysocre key min max

   注意：min于max用于限定搜索查询的条件
    	start与stop用于限定查询范围，作用于索引，表示开始和结束索引
    	offset于count用于限定查询范围，作用于查询结果，表示开始位置和数据总量
    
    
//按照从大到小的顺序移除count个值
zpopmax key [count]
//按照从小到大的顺序移除count个值
zpopmin key [count]
```



```java

//获得元素个数
zcard key

//获得元素在范围内的个数
zcount key min max

//求交集、并集放入destination中, 其中numkeys为交集或并集集合的数目,key1，key2代表要集合,它们会将集合中相同元素的值相加。
zinterstore destination numkeys key1 key2...
zunionstore destination numkeys key1 key2...
```

```java
127.0.0.1:6379> zcard scores
(integer) 2
127.0.0.1:6379> zcount scores 20 100
(integer) 2
127.0.0.1:6379> zadd s1 100 a 50 b 30c
(error) ERR syntax error
127.0.0.1:6379> zadd s1 100 a 20 b 30 c
(integer) 3
127.0.0.1:6379> zadd s2 90 a 80 b 10 c
(integer) 3
127.0.0.1:6379> zadd s3 70 a 40 b  20 c
(integer) 3
127.0.0.1:6379> zinterstore ss 3 s1 s2 s3
(integer) 3
127.0.0.1:6379> zrange ss 0 -1 withscores
1) "c"
2) "60"
3) "b"
4) "140"
5) "a"
6) "260"
127.0.0.1:6379> zrange s1 0 -1 withscores
1) "b"
2) "20"
3) "c"
4) "30"
5) "a"
6) "100"
```



**扩展操作**

做数据的排序

比如：电影排行

```java
//查看某个元素的索引(排名)
zrank key member
zrevrank key member

//查看某个元素索引的值
zscore key member
//增加某个元素索引的值
zincrby key increment member
```

```java
127.0.0.1:6379> zadd movies 111 a1 222 a2 333 a3
(integer) 3
127.0.0.1:6379> zrank movies a1
(integer) 0
127.0.0.1:6379> zrevrank movies a1
(integer) 2
127.0.0.1:6379> zscore movies a1
"111"
127.0.0.1:6379> zscore movies a2
"222"
127.0.0.1:6379> zincrby movies 10 a1
"121"
```



**注意事项**

- score保存的数据存储空间是64位，如果是整数范围是-9007199254740992~9007199254740992
- score保存的数据也可以是一个双精度的double值，基于双精度浮点数的特征，**可能会丢失精度**，使用时候要**慎重**
- sorted_set 底层存储还是**基于set**结构的，因此数据**不能重复**，如果重复添加相同的数据，score值将被反复覆盖，**保留最后一次**修改的结果

  

**业务场景**

观看影视会员到期需要处理的任务，通过sorted_set设施时间处理任务。

```java
127.0.0.1:6379> zadd hy 172826 uid:1
(integer) 1
127.0.0.1:6379> zadd hy 37459239 uid:2
(integer) 1
127.0.0.1:6379> zadd hy 47389 uid:3
(integer) 1
127.0.0.1:6379> zrange hy 0 -1
1) "uid:3"
2) "uid:1"
3) "uid:2"
127.0.0.1:6379> zrange hy 0 -1 withscores
1) "uid:3"
2) "47389"
3) "uid:1"
4) "172826"
5) "uid:2"
6) "37459239"
```

```
//获取当前系统时间
time
```

**应用于定时任务执行顺序管理或任务过期管理**



**任务/消息权重设定应用**

​	当任务或着消息待处理，形成了任务队列或消息队列时，对于高优先级的任务要保障对其优先处理，如何实现任务权重管理。

```java
127.0.0.1:6379> zadd tasks 4 orderid:1
(integer) 1
127.0.0.1:6379> zadd tasks  6 orderid:2
(integer) 1
127.0.0.1:6379> zadd tasks 10 orderid:2
(integer) 0
127.0.0.1:6379> zrange tasks 0 -1  withscores
1) "orderid:1"
2) "4"
3) "orderid:2"
4) "10"
127.0.0.1:6379> zadd tasks 19 orderid:3
(integer) 1
127.0.0.1:6379> zrevrange tasks 0 -1 withscores
1) "orderid:3"
2) "19"
3) "orderid:2"
4) "10"
5) "orderid:1"
6) "4"
```

   ![image-20210716154022557](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210716154022557.png)

```java
127.0.0.1:6379> zadd tt 102004 order:id:1
(integer) 1
127.0.0.1:6379> zadd tt 101008 order:id:2
(integer) 1
127.0.0.1:6379> zrange tt 0 -1 withscores
1) "order:id:2"
2) "101008"
3) "order:id:1"
4) "102004"
```



#### 类型数据实践案列

![image-20210717132642264](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210717132642264.png)

```java
//String类型 
127.0.0.1:6379> get 415
(nil)
127.0.0.1:6379> setex 415 60  1
OK
127.0.0.1:6379> get 415
"1"
127.0.0.1:6379> incr 415
(integer) 2
127.0.0.1:6379> incr 415
(integer) 3
127.0.0.1:6379> get 415
(nil)
```

![image-20210717133159098](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210717133159098.png)

```java
127.0.0.1:6379> get 415
(nil)
127.0.0.1:6379> setex 415 60 9223372036854775797
OK
127.0.0.1:6379> get 415
"9223372036854775797"
127.0.0.1:6379> incr 415
(integer) 9223372036854775798
127.0.0.1:6379> incr 415
(integer) 9223372036854775799
127.0.0.1:6379> incr 415
(integer) 9223372036854775800
127.0.0.1:6379> incr 415
(integer) 9223372036854775801
127.0.0.1:6379> incr 415
(integer) 9223372036854775802
127.0.0.1:6379> incr 415
(integer) 9223372036854775803
127.0.0.1:6379> incr 415
(integer) 9223372036854775804
127.0.0.1:6379> incr 415
(integer) 9223372036854775805
   //超出时常，如果在60s内，输入的次数超出限制，会抛出异常
127.0.0.1:6379> incr 415
(integer) 1
127.0.0.1:6379> incr 415
(integer) 2
127.0.0.1:6379> get 415
"2"
```



模拟微信消息发送时间排序

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210901144928816.png" alt="image-20210901144928816" style="zoom: 67%;" />



set用来存放置顶的消息

此时 300 用户向100 用户发送消息，需要判断是普通消息还是置顶消息

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210901145117114.png" alt="image-20210901145117114" style="zoom: 50%;" />

接下来400，发消息，在100用户中400用户是置顶消息，因此400的消息放到置顶list中

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210901145351183.png" alt="image-20210901145351183" style="zoom:50%;" />

200用户连续发送两次消息，都是普通消息，200第一次消息放入普通list，第二次消息放入list前会把之前的200消息去除，再放入，

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210901145653669.png" alt="image-20210901145653669" style="zoom:50%;" />

最后300用户又发了一次信息，发现原本list中有300信息，将其去除在加入到list中，放在200之后。

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210901145848845.png" alt="image-20210901145848845" style="zoom:50%;" />

最后100拿起手机查看消息，400为置顶位于最前，300消息最近在200之前

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210717134415007.png" alt="image-20210717134415007" style="zoom:50%;" />

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210717134434609.png" alt="image-20210717134434609" style="zoom:50%;" />

```java
//List类型
127.0.0.1:6379> lpush 100 200
(integer) 1
127.0.0.1:6379> lrem 100 1 300
(integer) 0
127.0.0.1:6379> lpush 100 300
(integer) 2
127.0.0.1:6379> lrem 100 1 400
(integer) 0
127.0.0.1:6379> lpush 100 400
(integer) 3
127.0.0.1:6379> lrem 100 1 200
(integer) 1
127.0.0.1:6379> lpush 100 200
(integer) 3
127.0.0.1:6379> lrem 100 1 300
(integer) 1
127.0.0.1:6379> lpush 100 300
(integer) 3
127.0.0.1:6379> lrange 100 0 -1
1) "300"
2) "200"
3) "400"
```



## Key通用命令

#### key通用操作

特征：

- key是一个**字符串**，通过key获取redis中保存的数据



**基本操作**

```java
//查看key是否存在
exists key

//删除key
del key

//查看key的类型
type key
```

```java
127.0.0.1:6379> set str str
OK
127.0.0.1:6379> hset hash hash1 1
(integer) 1
127.0.0.1:6379> lpush list1 1
(integer) 2
127.0.0.1:6379> sadd set 1
(integer) 1
127.0.0.1:6379> zadd zset 1 zset1 2 zset2
(integer) 2
127.0.0.1:6379> type str
string
127.0.0.1:6379> type hash
hash
127.0.0.1:6379> type list1
list
127.0.0.1:6379> type set
set
127.0.0.1:6379> type zset
zset
```



**扩展操作（时效性操作）**

```java
//设置生命周期
expire key seconds（秒）
pexpire key milliseconds（毫秒）
expire key timestamp   (时间戳)
pexpire key milliseconds-timestamp

//获取key的有效时间, 如果有有效时间则返回剩余有效时间, 如果为永久有效，则返回-1, 如果Key不存在则返回-2
ttl key
pttl key

//将有时限的数据设置为永久有效
persist key
```

```java
127.0.0.1:6379> set str str
OK
127.0.0.1:6379> get str
"str"
127.0.0.1:6379> expire str 3
(integer) 1
127.0.0.1:6379> get str
"str"
127.0.0.1:6379> get str
(nil)
127.0.0.1:6379> expire str 30
(integer) 0
127.0.0.1:6379> ttl str
(integer) -2
127.0.0.1:6379> get str
(nil)
127.0.0.1:6379> set str str
OK
127.0.0.1:6379> expire str 30
(integer) 1
127.0.0.1:6379> ttl str
(integer) 26
127.0.0.1:6379> pttl str
(integer) 20303
127.0.0.1:6379> ttl str
(integer) 17
127.0.0.1:6379> persist str
(integer) 1
127.0.0.1:6379> ttl str
(integer) -1
```



(**查询模式**)

```java
//根据key查询符合条件的数据
keys pattern
```

查询模式规则

![image-20210717141459800](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210717141459800.png)

（**其他操作**）

```java
//重命名key，为了避免覆盖已有数据，尽量少去修改已有key的名字，如果要使用最好使用renamenx
rename key newKey
renamenx key newKey

//对有所key排序,不会改变原数据
sort

//查看所有关于key的操作, 可以使用Tab快速切换
help @generic
```



## 数据库通用指令

**数据库**

![image-20210717143740151](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210717143740151.png)

**解决方案**

- Redis为每个服务提供有16个数据库，编号从0到15
- 每个数据库之间的数据相互独立



**Database 基本操作**

```java
//切换数据库 0~15
select index

//其他操作
quit
    //测试服务器
ping
echo massage
```



**扩展操作**

```java
//移动数据, 必须保证目的数据库中没有该数据
mov key db
    
//数据清除
//刷掉当前的数据
flushdb
//删除所有数据
flushall


//查看该库中数据总量
dbsize
```



## Jedis

### Jedis简介

**编程语言与redis**

- **java语言连接redis服务**

  Jedis

  SpringData Redis

  Lettuce

- C、c++、c#、Erlang等等



### **HelloWorld（Jedis）**

**Java操作引入Maven依赖**

```java
        <dependency>
            <groupId>redis.clients</groupId>
            <artifactId>jedis</artifactId>
            <version>2.9.0</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
```



**Java操作redis的步骤**

1. 连接redis
2. 操作redis
3. 关闭连接

```java
    //1.连接redis，ip和端口号
    Jedis jedis =  new Jedis("127.0.0.1",6379);
    //2.操作redis,jedis中对数据操作的指令和redis中的指令是一样的。
    jedis.set("小白","hello");
    //3.关闭连接
    jedis.close();
```


获取数据

```java
        //获取数据
        String str = jedis.get("小白");
        System.out.println(str);
//结果：hello
```



### Jedis读写redis数据

**案例要求**

![image-20210718131202763](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210718131202763.png)

```java
//这里按照s来测试
package Jedis;

import redis.clients.jedis.Jedis;
import redis.clients.jedis.exceptions.JedisDataException;

import static java.lang.Math.*;

public class Service {
    private String id;
    private int nums;
    public  Service(String id,int nums){
        this.id = id;
        this.nums = nums;
    }

    //控制单元
    public void service(){
        Jedis jedis =  new Jedis("127.0.0.1",6379);
        String value =  jedis.get("compid:"+id);
        //判断该值是否存在
        try {
            if (value == null){
                //不存在，创建该值并设置生命周期
                //设定允许10s内调用nums次
                jedis.setex("compid:"+id,10,Long.MAX_VALUE - nums+"");
            }else {
                //存在，自增，调用业务

                long nums1 =  jedis.incr("compid:"+id);

                business(nums-(Long.MAX_VALUE-nums1),id);
            }
        } catch (JedisDataException e){
            System.out.println("调用次数已经到达上限，请升级会员");
            return;
        }finally {
            jedis.close();
        }


    }
    //业务操作
    public void business(Long nums, String id){
        System.out.println("用户:"+id+" 业务操作执行"+nums);
    }
}

class MyThread extends Thread{
    Service sc ;
    public MyThread(String name,int nums){
        sc = new Service(name,nums);
    }

    @Override
    public void run() {
        while (true){
            sc.service();
            try {
                Thread.sleep((long) (500L + abs(random())));
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

class Main{
    public static void main(String[] args) {
        MyThread myThread = new MyThread("初级用户",10);
        MyThread myThread1 = new MyThread("高级用户",20);
        myThread.start();
        myThread1.start();
    }
}
```



### Jedis简易工具类开发

**基于连接池获取链接**

![image-20210718140311964](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210718140311964.png)

配置文件

```java
//全局配置
redis.host = 127.0.0.1
redis.port = 6379
redis.maxTotal = 30
redis.maxIdle = 10
```



简易工具类

```java
public class JedisUtils {
    private static String host;
    private static Integer port;
    private static Integer maxTotal;
    private static Integer maxIdle;

    private static  JedisPool jedisPool = null;

    //静态代码块在类加载时，只加载一次
    static {
        //加载配置文件
        ResourceBundle rb = ResourceBundle.getBundle("redis");
        //服务地址
        host = rb.getString("redis.host");
        //端口号
        port = Integer.valueOf(rb.getString("redis.port"));
        //最大连接数
        maxTotal = Integer.valueOf(rb.getString("redis.maxTotal"));
        //最大活动连接数
        maxIdle = Integer.valueOf(rb.getString("redis.maxIdle"));

        JedisPoolConfig jpc = new JedisPoolConfig();
        jpc.setMaxTotal(maxTotal);
        jpc.setMaxIdle(maxIdle);
        jedisPool = new JedisPool(jpc,host,port);

    }


    public static Jedis getJedis(){
       return jedisPool.getResource();

    }
}
```





### 可视化客户端

[Redis可视化工具](https://gitee.com/qishibo/AnotherRedisDesktopManager?utm_source=alading&utm_campaign=repo#https://github.com/qishibo/AnotherRedisDesktopManager/releases) 

[下载](https://github.com/qishibo/AnotherRedisDesktopManager/releases)

![image-20210718143009622](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210718143009622.png)

![image-20210718143018947](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210718143018947.png)





## Redis高级

**环境：Linux**

### **安装**

```nginx
//下载
wget http://download.redis.io/releases/redis-4.0.0.tar.gz

//解压
tar -xvf redis-4.0.0.tar.gz 

//安装
make install

//进入到src目录下
cd src/

//启动
redis-server

//进入redis
redis-cli
```



**Redis服务启动**

**默认配置启动**

```
redis-server
redis-server  --port 6380
```



设置配置信息

```java
//将redis目录下的redis.conf文件拷贝一份到 redis-6379.conf中
cat redis.conf  | grep -v "#" | grep -v "^$" > redis-6379.conf

//redis-6379.conf
port 6379
//守护进程方式启动，使用本启动方式，redis将以服务的形式存在，日志不在打印到命令窗口中
daemonize yes
logfile "6379.log"
 //当前服务文件保存位置
dir /usr/local/redis/redis-4.0.0/data

//加载配置文件    
/usr/local/bin/redis-server redis-6379.conf 
    
//查看redis进程
ps -ef | grep redis

root     28553     1  0 12:54 ?        00:00:00 /usr/local/bin/redis-server *:6379
root     28645 27223  0 12:55 pts/2    00:00:00 grep redis
    
   
//连接
/usr/local/bin/redis-cli
127.0.0.1:6379> 
```



**指定配置文件启动**

```
redis-server redis-6379.conf 
```



**Redis客户端连接**

**默认连接**

```
redis-cli
```

**连接指定服务器**

```
redis-cli -p 6379
redis-cli -h 127.0.0.1
redis-cli -h 127.0.0.1 -p 6379
```





### 持久化

使用永久性的存储介质保存数据，可以将数据进行回复

防止数据意外丢失，确保数据的安全性。



**方式**

- 以数据为重点，将数据以二进制形式保存，快照的形式，存储格式简单。**(RDB)**
- 记录操作数据的过程，日志的形式，存储格式复杂，关注的重点在数据的操作过程。**(AOF)**

![img](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//20200608142523.png)

#### RDB

**命令**

```
save
//手动执行一次保存
```



**配置相关命令**

- dbfilename dump.rdb
  - 说明：设置本地数据库文件名，默认值为 dump.rdb
  - 经验：通常设置为dump-端口号.rdb
- dir
  - 说明：设置存储.rdb文件的路径
  - 经验：通常设置成存储空间较大的目录中，目录名称data
- rdbcompression yes
  - 说明：设置存储至本地数据库时是否压缩数据，默认为 yes，采用 LZF 压缩
  - 经验：通常默认为开启状态，如果设置为no，可以节省 CPU 运行时间，但会使存储的文件变大（巨大）
- rdbchecksum yes
  - 说明：设置是否进行RDB文件格式校验，该校验过程在写文件和读文件过程均进行
  - 经验：通常默认为开启状态，如果设置为no，可以节约读写性过程约10%时间消耗，但是存储一定的数据损坏风险



**save指令工作原理**

![image-20210719133407507](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210719133407507.png)



当数据量过大，单线程执行会造成执行效率低下。



命令

```
bgsave(background save)
//手动启动后台保存操作，但不是立即执行
```



**bgsave指令工作原理**

![image-20210719133917825](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210719133917825.png)

**bgsave命令**是针对save阻塞问题做的**优化**。Redis内部所有涉及到RDB操作都采用bgsave的方式，save命令可以放弃使用，推荐使用bgsave。



**自动执行保存**

配置

```
save second changes
```

- 作用

  满足**限定时间**范围内**key**的变化数量达到**指定数量**即进行持久化

- 参数

  - second：监控时间范围
  - changes：监控key的变化量

- 配置位置

  在**conf文件**中进行配置



**工作原理**

![image-20210719140822364](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210719140822364.png)

**注意**：

- save配置要根据实际业务情况进行设置，频度过高或过低都会出现性能问题，结果可能是灾难性的
- save配置中对于second与changes设置通常具有**互补对应**关系（一个大一个小），尽量不要设置成包含性关系
- save配置启动后执行的是**bgsave操作**



**二种方法的对比**

![image-20210719140943100](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210719140943100.png)

**RDB优缺点**

- 优点
  - RDB是一个紧凑压缩的二进制文件，**存储效率较高**
  - RDB内部存储的是redis在某个时间点的数据快照，非常适合用于**数据备份，全量复制**等场景
  - RDB恢复数据的**速度**要比AOF**快**很多
  - 应用：服务器中每X小时执行bgsave备份，并将RDB文件拷贝到远程机器中，**用于灾难恢复**
- 缺点
  - RDB方式无论是执行指令还是利用配置，**无法做到实时持久化**，具有较大的可能性丢失数据
  - bgsave指令每次运行要执行fork操作**创建子进程**，要**牺牲**掉一些**性能**
  - Redis的众多版本中未进行RDB文件格式的版本统一，有可能出现各版本服务之间数据格式**无法兼容**现象





#### AOF(append only file)

**概念**

- AOF(append only file)持久化：以独立日志的方式记录**每次**写命令，重启时再重新执行AOF文件中命令，以达到恢复数据的目的。与RDB相比可以简单描述为记录数据产生的过程
- AOF的主要作用是解决了数据持久化的实时性，目前已经是Redis持久化的**主流**方式



**AOF写数据过程**

![image-20210719142015170](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210719142015170.png)

**三种策略**

- always（每次）
  - 每次写入操作均同步到AOF文件中，数据零误差，**性能较低**,**不建议使用**
- everysec（每秒）
  - 每秒将缓冲区中的指令同步到AOF文件中，数据准确性较高，**性能较高** ，**建议使用**，也是默认配置
  - 在系统突然宕机的情况下丢失1秒内的数据
- no（系统控制）
  - 由操作系统控制每次同步到AOF文件的周期，整体过程**不可控**



**功能开启**

- 配置

  ```
  appendonly yes|noCopy
  ```

  -  作用
    - 是否开启AOF持久化功能，**默认为不开启状态**

- 配置

  ```
  appendfsync always|everysec|noCopy
  ```

  - 作用
    - AOF写数据策略



**AOF重写**

**作用**

- 降低磁盘占用量，提高磁盘利用率
- 提高持久化效率，降低持久化写时间，提高IO性能
- 降低数据恢复用时，提高数据恢复效率

**规则**

- 进程内已超时的数据不再写入文件

- 忽略无效指令，重写时使用进程内数据直接生成，这样新的AOF文件只保留最终数据的写入命令

  - 如del key1、 hdel key2、srem key3、set key4 111、set key4 222等

- 对同一数据的多条写命令合并为一条命令

  - 如lpush list1 a、lpush list1 b、 lpush list1 c 可以转化为：lpush list1 a b c
  - 为防止数据量过大造成客户端缓冲区溢出，对list、set、hash、zset等类型，每条指令最多写入64个元素



**重写方式**

- 手动重写

  ```
  bgrewriteaof
  ```

- 自动重写

  ```
  auto-aof-rewrite-min-size size 
  auto-aof-rewrite-percentage percentage
  ```



配置

```java
//redis-6379.conf
port 6379
//守护进程方式启动，使用本启动方式，redis将以服务的形式存在，日志不在打印到命令窗口中
daemonize yes
logfile "6379.log"
 //当前服务文件保存位置
dir /usr/local/redis/redis-4.0.0/data
rdbcompression yes
rdbchecksum yes
save 10 2
//是否开启AOF持久化功能，**默认为不开启状态**
appendonly yes
//AOF写数据策略
appendfsync always
appendfilename appendonly-6379.aof
```

手动命令

```java
bgrewriteaof

//原来的appendonly-6379.aof文件大小变小了
```



**手动重写（bgrewriteaof）原理**

![img](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//20200608142657.png)



**工作原理**

基于always策略AOF 执行写入指令时，没有对aof文件进行重写

基于everysec策略AOF执行写入指令，相比于always策略多出了aof缓冲区

![img](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//20200608142755.png)

当everysec开启重写时，在子进程中除了有aof缓冲区，还有一个aof重写缓冲区，在执行重写指令时，根据aof重写缓冲区中的数据进行aof文件重写，将重写完的aof文件替换原来的aof文件

![img](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//20200608142814.png)



**AOF自动重写**

- 自动重写触发条件设置

  ```java
  //触发重写的最小大小
  auto-aof-rewrite-min-size size 
  //触发重写须达到的最小百分比
  auto-aof-rewrite-percentage percentCopy
  ```

- 自动重写触发比对参数（ 运行指令info Persistence获取具体信息 ）

  ```java
  //当前.aof的文件大小
  aof_current_size 
  //基础文件大小
  aof_base_size
  ```

- 自动重写触发条件

  ![img](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//20200608142715.png)







#### RDB与AOF区别

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//20200608142837.png" alt="img" style="zoom: 67%;" />



**RDB与AOF的选择之惑**

- 对数据非常敏感，建议使用默认的AOF持久化方案
  - AOF持久化策略使用**everysecond**，每秒钟fsync一次。该策略redis仍可以保持很好的处理性能，当出现问题时，最多丢失0-1秒内的数据。
  - 注意：由于AOF文件**存储体积较大**，且**恢复速度较慢**
- 数据呈现阶段有效性，建议使用RDB持久化方案
  - 数据可以良好的做到阶段内无丢失（该阶段是开发者或运维人员手工维护的），且**恢复速度较快**，阶段 点数据恢复通常采用RDB方案
  - 注意：利用RDB实现紧凑的数据持久化会使Redis降的很低
- 综合比对
  - RDB与AOF的选择实际上是在做一种权衡，每种都有利有弊
  - 如不能承受数分钟以内的数据丢失，对业务数据非常**敏感**，选用**AOF**
  - 如能承受数分钟以内的数据丢失，且追求大数据集的**恢复速度**，选用**RDB**
  - **灾难恢复选用RDB**
  - 双保险策略，同时开启 RDB 和 AOF，重启后，Redis优先使用 AOF 来恢复数据，降低丢失数据



#### 持久化应用场景

适合优惠券、限购券、激活码的抢购

 最新消息展示

具有操作先后顺序的数据控制



### 事务

redis事务就是一个命令执行的队列，将一系列预定义命令**包装成一个整体**（一个队列）。当执行时，**一次性按照添加顺序依次执行**，中间不会被打断或者干扰



#### 基本操作

- 开启事务

  ```
  multi
  ```

  - 作用
    - 作设定事务的开启位置，此指令执行后，后续的所有指令均加入到事务中

- 执行事务

  ```
  exec
  ```

  - 作用
    - 设定事务的结束位置，同时执行事务。**与multi成对出现**，成对使用

**注意:**加入事务的命令暂时进入到任务队列中，并没有立即执行，只有执行exec命令才开始执行。

```java
127.0.0.1:6379> multi
OK
127.0.0.1:6379> set age 30
QUEUED
127.0.0.1:6379> get age
QUEUED
127.0.0.1:6379> set age 31
QUEUED
127.0.0.1:6379> get age
QUEUED
127.0.0.1:6379> exec
1) OK
2) "30"
3) OK
4) "31"
```



- 取消事务

  ```
  discard
  ```

  - 作用
    - 终止当前事务的定义，发生在multi之后，exec之前



**工作流程**

![image-20210720150212121](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210720150212121.png)



**注意事项**

- **定义事务的过程中，命令格式输入错误怎么办？**

  - 语法错误
    - 指命令书写格式有误 例如执行了一条不存在的指令
  - 处理结果
    - 如果定义的事务中所包含的命令存在语法错误，整体事务中**所有命令均不会执行**。包括那些语法正确的命令

  **定义事务的过程中，命令执行出现错误怎么办？**

  - 运行错误
    - 指命令**格式正确**，但是**无法正确的执行**。例如对list进行incr操作
  - 处理结果
    - 能够正确运行的命令会执行，运行错误的命令不会被执行

  **注意**：已经执行完毕的命令对应的数据**不会自动回滚**，需要程序员自己在代码中实现回滚。

**手动进行事务回滚**

记录操作过程中被影响的数据之前的状态

设置指令回复所有的被修改的项



#### 锁

**基于特定条件的事务执行**

- 对 key 添加监视锁，在执行exec前如果key发生了变化，终止事务执行

  ```
  watch key1, key2....
  ```

- 取消对**所有**key的监视

  ```
  unwatch
  ```

用于场景：例如四个补货员进行补货，如果补货员一已经进行补货了，那么剩下的补货员不能在进行补货了。需要对货物的数量进行监控。



#### **分布式锁**

**基于特定条件的事务执行**

- 使用 setnx 设置一个公共锁，这个公共锁共大家共同使用(**公共厕所的例子**)

  ```
  //上锁
  setnx lock-key value
  //释放锁
  del lock-keyCopy
  ```

  - 利用setnx命令的返回值特征，有值（被上锁了）则返回设置失败，无值（没被上锁）则返回设置成功
    - 对于返回设置成功，拥有控制权，进行下一步的具体业务操作
    - 对于返回设置失败，不具有控制权，排队或等待
  - 操作完毕通过del操作释放锁

**注意**：上述解决方案是一种**设计概念**，依赖规范保障，具有风险性

应用情景：超卖问题，库存中最后一件商品同时被3个顾客购买，只能满足其中一个。





场景：当前客户拿到锁之后进行操作，突然出现了问题，导致当前锁无法释放，会导致后续的进行

**分布式锁改良**

- 使用 expire 为锁key添加**时间限定**，到时不释放，放弃锁

  ```
  expire lock-key seconds
  pexpire lock-key milliseconds
  ```

- 由于操作通常都是微秒或毫秒级，因此该锁定时间**不宜设置过大**。具体时间需要业务测试后确认。
  - 例如：持有锁的操作最长执行时间127ms，最短执行时间7ms。
  - 测试百万次最长执行时间对应命令的最大耗时，测试百万次网络延迟平均耗时
  - 锁时间设定推荐：最大耗时 * 120%+平均网络延迟 * 110%
  - 如果业务最大耗时<<网络平均延迟，通常为2个数量级，取其中单个耗时较长即可



### 删除策略

#### 过期数据

![image-20210721143113932](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210721143113932.png)



#### 数据删除策略

- **定时删除**
- **惰性删除**
- **定期删除**

![image-20210721143621331](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210721143621331.png)

expires空间存放数据的时间：数据地址  ---->  过期时间



**数据删除策略的目标**

在内存占用与CPU占用之间寻找一种**平衡**，顾此失彼都会造成整体redis性能的下降，甚至引发服务器宕机或内存泄露



**定时删除**

- 创建一个定时器，当key设置有过期时间，且过期时间到达时，由定时器任务**立即执行**对键的删除操作
- 优点：**节约内存**，到时就删除，快速释放掉不必要的内存占用
- 缺点：**CPU压力很大**，无论CPU此时负载量多高，均占用CPU，会影响redis服务器响应时间和指令吞吐量
- 总结： 用处理器性能换取存储空间 （**拿时间换空间**）



**惰性删除**

- 数据到达过期时间，不做处理。等下次访问该数据时
  - 如果未过期，返回数据
  - 发现已过期，删除，返回不存在
- 优点：**节约CPU性能**，发现必须删除的时候才删除
- 缺点：**内存压力很大**，出现长期占用内存的数据
- 总结：用存储空间换取处理器性能 （**拿空间换时间**）



**定期删除**

![image-20210721150201947](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210721150201947.png)

serverCron():表明每秒执行**server.hz**次的**定期删除操作**

databasesCron():每次定期操作时逐个检查Redis中**15**个时效性存储结构，每个库中都有各自的有效性存储。

activeExpireVCycle():**随机抽取**检查每个**数据的时效性**

- 周期性轮询redis库中的时效性数据，采用**随机抽取的策略**，利用过期数据占比的方式控制删除频度
- 特点1：CPU性能占用设置有峰值，检测频度可自定义设置
- 特点2：内存压力不是很大，长期占用内存的冷数据会被持续清理
- 总结：周期性抽查存储空间 （随机抽查，重点抽查）



**删除策略对比**

| 定时删除     | 节约内存，无占用     | 不分时段占用cpu资源               | 拿时间换空间     |
| ------------ | -------------------- | --------------------------------- | ---------------- |
| **惰性删除** | **内存占用严重**     | **延时执行、cpu利用率高**         | **拿空间换时间** |
| **定时删除** | **内存定期随机清理** | **每秒花费固定的cpu资源维护内存** | **随机抽查**     |





#### 逐出算法

当redis中存储的数据都是长期有效的或者没有设置有效时长，而删除策略针对的时效性的数据。

- Redis使用内存存储数据，在执行每一个命令前，会调用**freeMemoryIfNeeded()**检测内存是否充足。如果内存不满足新加入数据的最低存储要求，redis要临时删除一些数据为当前指令清理存储空间。清理数据的策略称为**逐出算法**
- **注意**：逐出数据的过程不是100%能够清理出足够的可使用的内存空间，如果不成功则反复执行。当对所有数据尝试完毕后，如果不能达到内存清理的要求，将出现错误信息。



**影响数据追出的相关配置**

- 最大可使用内存

  ```
  maxmemory
  ```

  占用物理内存的比例，默认值为0，表示不限制。生产环境中根据需求设定，通常设置在50%以上。

- 每次选取待删除数据的个数

  ```
  maxmemory-samples
  ```

  选取数据时并不会全库扫描，导致严重的性能消耗，降低读写性能。因此采用**随机获取数据**的方式作为待检测删除数据

- 删除策略

  ```
  maxmemory-policy
  ```

  达到最大内存后的，对被挑选出来的数据进行删除的策略



 检测易失数据![image-20210722130758323](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210722130758323.png)

当前执行了9s，从name、age、addr和gender中选取一个最近最少使用

当前执行了9s，从name、age、addr和gender中选取一个次数使用最少



检测全库数据

![image-20210722131028572](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210722131028572.png)

这些策略和maxmemory-policy 连用

例如：

```
maxmemory-policy volatile-lru
```





**数据逐出策略配置依据**

- 使用**INFO命令**输出监控信息，查询缓存 **hit 和 miss** 的次数，根据业务需求调优Redis配置

![img](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//20200608143004.png)





### redis.conf

#### 服务器基础配置

**服务器端设定**

- 设置服务器以守护进程的方式运行

  ```
  daemonize yes|no
  ```

- 绑定主机地址

  ```
  bind 127.0.0.1
  ```

- 设置服务器端口号

  ```
  port 6379
  ```

- 设置数据库数量

  ```
  databases 16
  ```



**日志配置**

- 设置服务器以指定日志记录级别

  ```
  loglevel debug|verbose|notice|warning
  ```

- 日志记录文件名

  ```
  logfile 端口号.log
  ```

注意：日志级别开发期设置为verbose即可，生产环境中配置为notice，简化日志输出量，降低写日志IO的频度。



**客户端配置**

- 设置同一时间最大客户端连接数，默认无限制。当客户端连接到达上限，Redis会关闭新的连接

  ```
  maxclients 0
  ```

  

- 客户端闲置等待最大时长，达到最大值后关闭连接。如需关闭该功能，设置为0.

  ```
  timeout 300
  ```



**多服务器快捷配置**

- 导入并加载指定配置文件信息，用于快速创建redis公共配置较多的redis实例配置文件，便于维护

  ```
  include /path/server-端口号.conf
  ```





### 高级数据类型

#### Bitmaps

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210902150647625.png" alt="image-20210902150647625" style="zoom:50%;" />

按位存储数据，存入某些 数据的状态：性别、是否为党员等等

操作过程也是按照二进制(01)的形式，**相比于原来的基本数据类型，这并不是一个新的数据类型，可以理解为操作原基本数据二进制的形式**



**基础操作**

- 获取指定key对应偏移量上的bit值

  ```
  getbit key offset
  ```

- 设置指定key对应偏移量上的bit值，**value只能是1或0**

  存入的是二进制的形式 0、1

  例如：key上所在的位置是100，在100的位置设定值为1，那么在第一百位之前都要补0.

  ```
  setbit key 100 1
  ```

  ```
  setbit key offset value
  ```





**扩展操作**

- 对指定key按位进行交、并、非、异或操作，并将结果**保存到destKey**中

  ```
  bitop operate destKey key1 [key2...]
  ```

  - and：与
  - or：或
  - not：非
  - xor：异或

- 统计指定key中1的数量

  ```
  bitcount key [start end]
  ```

**应用于信息状态的统计**

例如统计电影网站上各个电影的点击量

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210902151928428.png" alt="image-20210902151928428" style="zoom:50%;" />



#### HyperLogLog

**基数**

- 基数是数据集**去重后元素个数**
- HyperLogLog 是用来做基数统计的，运用了LogLog的算法

![img](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//20200608143020.png)



**基本操作**

- 添加数据

  ```
  pfadd key element1, element2...
  ```

- 统计数据

  ```
  pfcount key1 key2....
  ```

- 合并数据

  ```
  pfmerge destkey sourcekey [sourcekey...]
  ```



**应用数据统计**

**相关说明**

- 用于进行基数统计，**不是集合，不保存数据**，只记录数量而不是具体数据
- 核心是基数估算算法，最终数值**存在一定误差**
- 误差范围：基数估计的结果是一个带有 0.81% 标准错误的近似值
- **耗空间极小**，每个hyperloglog key占用了12K的内存用于标记基数
- pfadd命令不是一次性分配12K内存使用，会随着基数的增加内存**逐渐增大**，容量的上限是12k。
- Pfmerge命令**合并后占用**的存储空间为**12K**，无论合并之前数据量多少





#### GEO

**基本操作**

- 添加坐标点（将若干个坐标添加到一个容器中）

  ```
  geoadd key longitude latitude member [longitude latitude member ...] 
  ```

- 获取坐标点

  ```
  geopos key member [member ...] 
  ```

- 计算坐标点距离

  ```
  geodist key member1 member2 [unit] 
  ```

```java
127.0.0.1:6379> geoadd geos  22 33 a  //a点坐标
(integer) 1
127.0.0.1:6379> geoadd geos  11 22 b //b点坐标
(integer) 1
127.0.0.1:6379> geopos geos a    
1) 1) "22.00000137090682983"
   2) "32.99999989476653894"
127.0.0.1:6379> geopos geos b
1) 1) "10.99999934434890747"
   2) "21.99999950739083232"
127.0.0.1:6379> geodist geos a b  //a 、 b之间的举例
"1633200.1320"
127.0.0.1:6379> 
```





- 根据坐标求范围内的数据

```
georadius key longitude latitude radius m|km|ft|mi [withcoord] [withdist] [withhash] [count count]
```

- 根据点求范围内数据

  ```
  georadiusbymember key member radius m|km|ft|mi [withcoord] [withdist] [withhash] [count count]
  ```

- 获取指定点对应的坐标hash值

  ```
  geohash key member [member ...]
  ```



```java
127.0.0.1:6379> geoadd geos 1 1 1,1
(integer) 1
127.0.0.1:6379> geoadd geos 1 2 1,2
(integer) 1
127.0.0.1:6379> geoadd geos 1 3 1,3
(integer) 1
127.0.0.1:6379> geoadd geos 2 1 2,1
(integer) 1
127.0.0.1:6379> geoadd geos 2 2 2,2
(integer) 1
127.0.0.1:6379> geoadd geos 2 3 2,3
(integer) 1
127.0.0.1:6379> geoadd geos 3 1 3,1
(integer) 1
127.0.0.1:6379> geoadd geos 3 2 3,2
(integer) 1
127.0.0.1:6379> geoadd geos 3 3 3,3
(integer) 1
127.0.0.1:6379> geoadd geos 5 5 5,5
(integer) 1
127.0.0.1:6379> georadiusbymember geos 2,2 180 km
1) "1,1"
2) "2,1"
3) "1,2"
4) "2,2"
5) "3,1"
6) "3,2"
7) "1,3"
8) "2,3"
9) "3,3"
127.0.0.1:6379> georadiusbymember geos 2,2 100 km
1) "2,2"
127.0.0.1:6379> georadiusbymember geos 2,2 1000 km
 1) "1,1"
 2) "2,1"
 3) "1,2"
 4) "2,2"
 5) "3,1"
 6) "3,2"
 7) "1,3"
 8) "2,3"
 9) "3,3"
10) "5,5"
127.0.0.1:6379> georadius geos 1.5 1.5 90 km
1) "1,2"
2) "2,2"
3) "1,1"
4) "2,1"
127.0.0.1:6379> geohash geos 2,2
1) "s037ms06g70"
127.0.0.1:6379> geohash geos 1,1
1) "s00twy01mt0"
```





## Redis集群

### 主从复制

**多台服务器连接方案**

![image-20210723131642561](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210723131642561.png)

- 提供数据方：master
  - 主服务器，主节点，主库
  - 主客户端
- 接收数据的方：slave
  - 从服务器，从节点，从库
  - 从客户端
- 需要解决的问题
  - **数据同步**
- 核心工作
  - master的数据**复制**到slave中



**主从复制(一对多)**

主从复制即将master中的数据即时、有效的**复制**到slave中

特征：一个master可以拥有多个slave，一个slave只对应一个master

职责：

- master:
  - 写数据
  - 执行写操作时，将出现变化的数据自动**同步**到slave
  - 读数据（可忽略）
- slave:
  - 读数据
  - 写数据（**禁止**）



**作用**

- 读写分离：master写，slave读，提高服务器的读写负载能力
- 负载均衡：基于主从结构，配合读写分离，由slave分担master负载，并根据需求的变化，改变slave的数量，通过多个从节点分担数据读取负载，大大提高Redis服务器并发量与数据吞吐量
- 故障恢复：当master出现问题时，由slave提供服务，实现快速的故障恢复
- 数据冗余：实现数据热备份，是持久化之外的一种数据冗余方式
- 高可用基石：**基于主从复制，构建哨兵模式与集群，实现Redis的高可用方案**



**工作流程**

- 主从复制过程大体可以分为3个阶段
  - 建立连接阶段（即准备阶段）
  - 数据同步阶段
  - 命令传播阶段

![image-20210723133618394](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210723133618394.png)



#### **建立连接阶段(第一阶段)**

建立slave到master的连接，使master能够识别slave，并保存slave端口号

![image-20210723134123265](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210723134123265.png)

补充：在建立了socket连接后，建立定时任务是为了保证slave和master之间连接正常

若master服务器设置了密码，在连接时就需要进行身份验证



**主从连接（slave连接master） **

- 方式一：客户端发送命令

  ```
  slaveof <masterip> <masterport>
  ```

  ```
  127.0.0.1:6380> slaveof 127.0.0.1 6379
  OK
  ```

- 方式二：启动服务器参数

  ```
  redis-server -slaveof <masterip> <masterport>
  ```

  ```
  redis-server /usr/local/redis/redis-4.0.0/conf/redis-6380.conf --slaveof 127.0.0.1 6379
  ```

- 方式三：服务器配置 （常用）

  ```
  slaveof <masterip> <masterport>
  ```

  ```
  port 6380
  //不启动守护进程方式，使用本启动方式，redis将以服务的形式存在，日志不在打印到命令窗口中
  daemonize no
  #logfile "6380.log"
   //当前服务文件保存位置
  dir /usr/local/redis/redis-4.0.0/data
  slaveof 127.0.0.1 6379
  ```

  ![image-20210723141532664](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210723141532664.png)![image-20210723141613418](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210723141613418.png)



**主从断开连接**

- **客户端**发送命令

  ```
  slaveof no one
  ```

  - 说明： slave断开连接后，**不会删除已有数据**，只是不再接受master发送的数据

  

**授权访问**

- master客户端发送命令设置密码

  ```
  requirepass <password>
  ```

- master配置文件设置密码

  ```
  config set requirepass <password> 
  config get requirepass
  ```

- slave客户端发送命令设置密码

  ```
  auth <password>
  ```

- slave配置文件设置密码

  ```
  masterauth <password>
  ```

- slave启动服务器设置密码

  ```
  redis-server –a <password>
  ```



#### **数据同步阶段(第二阶段)**

![image-20210723143039754](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210723143039754.png)

- 全量复制

  - 将master执行bgsave之前，master中所有的数据同步到slave中

- 部分复制

  （增量复制）

  - 将master执行bgsave操作中，新加入的数据（复制缓冲区中的数据）传给slave，slave通过bgrewriteaof指令来恢复数据

**数据同步过程只包含两个部分: 全量复制、部分复制**



 **数据同步阶段master说明**

1. 如果master数据量巨大，数据同步阶段应**避开流量高峰期**，**避免**造成master**阻塞**，影响业务正常执行

2. 复制缓冲区大小设定不合理，会导致数据溢出。如进行全量复制周期太长，进行部分复制时发现数据已经存在丢失的情况，必须进行第二次全量复制，致使slave陷入**死循环**状态。

   ```
   repl-backlog-size 1mb
   ```

   

3. master单机内存占用主机内存的比例不应过大，建议使用50%-70%的内存，留下30%-50%的内存用于执 行bgsave命令和创建复制缓冲区



![image-20210724125114705](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210724125114705.png)

**数据同步阶段slave说明**

1. 为避免slave进行全量复制、部分复制时服务器响应阻塞或数据不同步，**建议关闭**此期间的对外服务。

   ```
   slave-serve-stale-data yes|no
   ```

2. 数据同步阶段，master发送给slave信息可以理解master是slave的一个客户端，主动向slave发送命令

3. 多个slave同时对master请求数据同步，master发送的RDB文件增多，会对带宽造成巨大冲击，如果master带宽不足，因此数据同步需要根据业务需求，适量错峰

4. slave过多时，建议调整拓扑结构，由一主多从结构变为树状结构，中间的节点既是master，也是 slave。注意使用树状结构时，由于层级深度，导致深度越高的slave与最顶层master间数据同步延迟较大，**数据一致性变差，应谨慎选择**

 

#### **命令传播阶段(第三阶段)**

- 当master数据库状态被修改后，导致主从服务器数据库状态不一致，此时需要让主从数据同步到一致的状态，**同步**的动作称为**命令传播**
- master将接收到的数据变更命令发送给slave，slave接收命令后执行命令

- 主从复制过程大体可以分为3个阶段
  - 建立连接阶段（即准备阶段）
  - 数据同步阶段
  - 命令传播阶段



**命令传播阶段的部分复制**

- 命令传播阶段出现了断网现象
  - 网络闪断闪连
  - 短时间网络中断  部分复制
  - 长时间网络中断   全量复制

- 部分复制的**三个核心要素**
  - 服务器的运行 id（run id）
  - 主服务器的复制积压缓冲区
  - 主从服务器的复制偏移量



**服务器的运行ID（runid）**

- 概念：服务器运行ID是每一台服务器每次运行的身份识别码，一台服务器多次运行可以生成多个运行id
- 组成：运行id由40位字符组成，是一个随机的十六进制字符 例如- -
  - fdc9ff13b9bbaab28db42b3d50f852bb5e3fcdce
- 作用：运行id被用于在服务器间进行传输，识别身份
  - 如果想两次操作均对同一台服务器进行，必须每次操作携带对应的运行id，用于对方识别
- 实现方式：运行id在每台服务器启动时自动生成的，master在首次连接slave时，会将自己的运行ID发送给slave，slave保存此ID，通过**info Server**命令，可以查看节点的runid



**复制缓冲区**

- 概念：复制缓冲区，又名复制积压缓冲区，是一个**先进先出（FIFO）的队列**，用于存储服务器执行过的命 令，每次传播命令，master都会将传播的命令记录下来，并存储在复制缓冲区。

  **注意:复制缓冲区默认数据存储空间大小是1M，由于存储空间大小固定，当入队元素的数量大于队列长度时，最先入队的元素会被弹出，而新元素会被放入队列**

- 由来：每台服务器启动时，如果开启有AOF或被连接成为master节点，即创建复制缓冲区

- 作用：用于保存master收到的所有指令（仅影响数据变更的指令，例如set，select）

- 数据来源：当master接收到主客户端的指令时，除了将指令执行，会将该指令存储到缓冲区中

![image-20210724131221079](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210724131221079.png)



**复制缓冲区内部工作原理**

- 组成
  - 偏移量(位置)
  - 字节值
- 工作原理
  - 通过offset区分不同的slave当前数据传播的差异
  - master记录**已发送**的信息对应的offset
  - slave记录**已接收**的信息对应的offset

![image-20210724131739384](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210724131739384.png)



**主从服务器复制偏移量（offset）**

- 概念：一个数字，描述复制缓冲区中的指令字节位置
- 分类：
  - master复制偏移量：记录发送给所有slave的指令字节对应的位置（多个）
  - slave复制偏移量：记录slave接收master发送过来的指令字节对应的位置（一个）
- 数据来源： master端：发送一次记录一次 slave端：接收一次记录一次
- 作用：**同步信息**，比对master与slave的差异，当slave断线后，恢复数据使用



#### 数据同步+命令传播阶段工作流程

![image-20210724133356074](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210724133356074.png)



**心跳机制**

- 进入**命令传播阶段候**，master与slave间需要进行信息交换，使用心跳机制进行维护，实现双方连接保持在线
- master心跳：
  - 指令：PING
  - 周期：由repl-ping-slave-period决定，默认10秒
  - 作用：判断slave是否在线
  - 查询：INFO replication 获取slave最后一次连接时间间隔，lag项维持在0或1视为正常
- slave心跳任务
  - 指令：REPLCONF ACK {offset}
  - 周期：1秒
  - 作用1：汇报slave自己的复制偏移量，获取最新的数据变更指令
  - 作用2：判断master是否在线



**心跳阶段注意事项**

- 当slave多数掉线，或延迟过高时，master为保障数据稳定性，将拒绝所有信息同步操作

  ```
  min-slaves-to-write 2 
  min-slaves-max-lag 8
  ```

  - slave数量少于2个，或者所有slave的延迟都大于等于10秒时，强制关闭master写功能，停止数据同步

- slave数量由slave发送**REPLCONF ACK**命令做确认

- slave延迟由slave发送**REPLCONF ACK**命令做确认

![image-20210724134245251](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210724134245251.png)



#### 常见问题

![img](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//20200608143304.png)

![image-20210724134554939](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210724134554939.png)

![img](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//20200608143317.png)



**网络中断**

![img](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//20200608143327.png)

![img](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//20200821110907.png)

 

**数据不一致**

![img](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//20200608143352.png)



### 哨兵模式

#### 哨兵简介

哨兵(sentinel) 是一个**分布式系统**，用于对主从结构中的每台服务器进行**监控**，当出现故障时通过投票机制**选择**新的master并将所有slave连接到新的master。

![image-20210724141347922](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210724141347922.png)

**作用**

- 监控
  - 不断的检查master和slave是否正常运行。 master存活检测、master与slave运行情况检测
- 通知（提醒）
  - 当被监控的服务器出现问题时，向其他（哨兵间，客户端）发送通知。
- **自动故障转移**
  - 断开master与slave连接，选取一个slave作为master，将其他slave连接到新的master，并告知客户端新的服务器地址

 **注意：**
哨兵也是一台**redis服务器**，只是不提供数据服务 通常哨兵配置数量为**单数**



#### 启用哨兵模式

- 配置一拖二的主从结构

- 配置三个哨兵（配置相同，端口不同）

  - 参看sentinel.conf

- 启动哨兵

  ```
  redis-sentinel sentinel端口号 .conf
  ```



配置哨兵

```java
//这里配置三个哨兵对应三个端口,这里配置文件的端口简写了，实际需要三个对应的配置文件
port 26381/26380/26380
dir /usr/local/redis/redis-4.0.0/data
//根据哨兵数量配置：用来在故障转移时判断主服务器是否宕机的占比数，这里3个哨兵，如果超过两个及以上的哨兵赞同，那么认定主服务器宕机
sentinel monitor mymaster 127.0.0.1 6379 2
sentinel down-after-milliseconds mymaster 30000
sentinel parallel-syncs mymaster 1
sentinel failover-timeout mymaster 180000
```

![image-20210724144152356](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210724144152356.png)



#### **工作原理**

主从切换三个阶段：监控、通知、故障转移



**监控阶段（同步信息）**

- 用于同步各个节点的状态信息
  - 获取各个sentinel的状态（是否在线）
- 获取master的状态
  - master属性
    - runid
    - role：master
    - 各个slave的详细信息
- 获取所有slave的状态（根据master中的slave信息）
  - slave属性
    - runid
    - role：slave
    - master_host、master_port
    - offset

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//20200608143539.png" alt="img" style="zoom: 67%;" />

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210725134144092.png" alt="image-20210725134144092" style="zoom: 50%;" />



**通知阶段（保持联通）**

![image-20210725134317697](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210725134317697.png)

多个哨兵之间形成自己的通讯，一个哨兵去和主服务器以及从服务器作信息交换，之后多个哨兵之间进行信息同步。



**故障转移阶段**



![image-20210725134719772](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210725134719772.png)

当一个哨兵去ping主服务器发现主服务器没有回应时，会判定主服务器可能宕机了，这只是一个哨兵的判断（**主观下线**），当然一个哨兵可能不足以认定，因此其他的哨兵纷纷去ping主服务器，如果都发现主服务器没有回应，那么多数表决一致（**客观下线**），判定主服务器宕机了。



![image-20210725135437225](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210725135437225.png)

发现主服务器宕机了，需要从从服务器中选举出master，这个工作就是由哨兵来，在选举之前，哨兵之间要选举出执行人，它们之间会进行一个竞选过程。



- **由推选出来的哨兵对当前的slave进行筛选**，筛选条件有：
  - 服务器列表中挑选备选master
  - 在线的
  - 响应慢的
  - 与原master断开时间久的
  - 优先原则
    - 优先级
    - offset
    - runid
  - 发送指令（ sentinel ）
    - 向新的master发送**slaveof no one**(断开与原master的连接)
    - 向其他slave发送slaveof 新masterIP端口（让其他slave与新的master相连）



### 集群

#### **简介**

**集群架构**

- 集群就是使用网络将若干台计算机**联通**起来，并提供**统一的管理方式**，使其对外呈现单机的服务效果

![image-20210725141126715](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210725141126715.png)

**集群作用**

- 分散单台服务器的访问压力，实现**负载均衡**
- 分散单台服务器的存储压力，实现**可扩展性**
- **降低**单台服务器宕机带来的**业务灾难**

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210725141228950.png" alt="image-20210725141228950" style="zoom: 50%;" />

#### 结构设计

**数据存储设计**

- 通过算法设计，计算出key应该保存的位置
- 将所有的存储空间计划切割成16384份，每台主机保存一部分 每份代表的是一个存储空间，不是一个key的保存空间
- 将key按照计算出的结果放到对应的存储空间

<img src="https://nyimapicture.oss-cn-beijing.aliyuncs.com/img/20200608143701.png" alt="img" style="zoom: 67%;" />

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210725141650452.png" alt="image-20210725141650452" style="zoom:50%;" />

- 增强可扩展性 ——槽

  一个服务器中内部存储空间分成若干个槽，若增加新的节点，

  将原来各个服务器中一部分槽拿来给的新节点

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210725141942025.png" alt="image-20210725141942025" style="zoom: 50%;" />





**集群内部通讯设计**

- 各个数据库互相连通，保存各个库中槽的编号数据
- 一次命中，直接返回
- 一次未命中，告知具体的位置，key再直接去找对应的库保存数据

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210725142455715.png" alt="image-20210725142455715" style="zoom: 67%;" />

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210725142526718.png" alt="image-20210725142526718" style="zoom:67%;" />



配置集群：

```java
//redis-6379.conf
port 6379
//守护进程方式启动，使用本启动方式，redis将以服务的形式存在，日志不在打印到命令窗口中
daemonize yes
logfile "6379.log"
 //当前服务文件保存位置
dir /usr/local/redis/redis-4.0.0/data
rdbcompression yes
rdbchecksum yes
save 10 2
//是否开启AOF持久化功能，**默认为不开启状态**
appendonly yes
//AOF写数据策略
appendfsync always
appendfilename appendonly-6379.aof
bind 127.0.0.1
databases 16
//启动cluster节点
cluster-enabled yes
//cluster的名称
cluster-config-file nodes-6379.conf
//节点的过期时间
cluster-node-timeout 10000
```



将各个节点连接起来

```
//注意要保持：ruby 和 gem 版本一致
redis-trib.rb  create --replicas 1
 127.0.0.1:6379   127.0.0.1:6380   127.0.0.1:6381
 127.0.0.1:6382   127.0.0.1:6383   127.0.0.1:6384

//创建集群  create
//指定集群内部结构 --replicas 
//2 ：一个master连接两个slave
//1: 一个master连接1个slave
127.0.0.1:6379 127.0.0.1:6380 127.0.0.1:6381 代表master的IP加端口号

127.0.0.1:6382   127.0.0.1:6383   127.0.0.1:6384 代表slave的IP加端口号

//注意一一对应 ， 3个master 对应 3个slave
```

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210725145155534.png" alt="image-20210725145155534" style="zoom: 80%;" />





操作集群命令

```
redis-cli -c
```

![image-20210725145939491](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210725145939491.png)

数据被指定到对应节点的槽上。



当集群中的master服务器上的slave服务器宕机后，对应的master的服务器对其宕机的slave服务器做标记，不影响整个master工作，当宕机的slave重连时，清楚标记，进行数据同步，继续工作。



当集群中的master服务器宕机后，其下的slave服务器尝试重新连接master，如果连接超时，那么该slave服务器翻身成为master服务器。

```
cluster nodes
```

![image-20210725151154787](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210725151154787.png)

当原来的master重新来链接后，成为了slave服务器

![image-20210725151212406](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210725151212406.png)



**Cluster节点操作命令**

查看集群节点信息

```
cluster noges
```

进入一个从节点redis，切换其主节点

```
cluster replicate <master-id>
```

发现一个新节点，新增主节点

```
cluster meet ip:port
```

忽略一个没有solt的节点

```
cluster forget <id>
```

手动故障转移

```
cluster failover
```



### 企业级解决方案

1. ####  缓存预热

**问题排查**

1. 请求数量较高
2. 主从之间数据吞吐量较大，数据同步操作频度较高



**解决方案**

- 前置准备工作：
  - 日常例行统计数据访问记录，统计访问频度较高的热点数据
  - 利用LRU数据删除策略，构建数据留存队列 例如：storm与kafka配合
- 准备工作：
  - 将统计结果中的数据分类，根据级别，redis优先加载级别较高的热点数据
  - 利用分布式多服务器同时进行数据读取，提速数据加载过程
  - 热点数据主从同时预热
- 实施：
  - 使用脚本程序固定触发数据预热过程
  - 如果条件允许，使用了CDN（内容分发网络），效果会更好

**总结**

缓存预热就是系统启动前，提前将相关的缓存数据直接加载到缓存系统。避免在用户请求的时候，先查询数据库，然后再将数据缓存的问题！用户直接查询事先被预热的缓存数据



#### 缓存雪崩

**数据库服务器崩溃（1）**

1. 系统平稳运行过程中，忽然数据库连接量激增
2. 应用服务器无法及时处理请求
3. 大量408，500错误页面出现
4. 客户反复刷新页面获取数据
5. 数据库崩溃
6. 应用服务器崩溃
7. 重启应用服务器无效
8. Redis服务器崩溃
9. Redis集群崩溃
10. 重启数据库后再次被瞬间流量放倒

**问题排查**

1. 在一个**较短**的时间内，缓存中**较多**的key**集中过期**
2. 此周期内请求访问过期的数据，redis未命中，redis向数据库获取数据
3. 数据库同时接收到大量的请求无法及时处理
4. Redis大量请求被积压，开始出现超时现象
5. 数据库流量激增，数据库崩溃
6. 重启后仍然面对缓存中无数据可用
7. Redis服务器资源被严重占用，Redis服务器崩溃
8. Redis集群呈现崩塌，集群瓦解
9. 应用服务器无法及时得到数据响应请求，来自客户端的请求数量越来越多，应用服务器崩溃
10. 应用服务器，redis，数据库全部重启，效果不理想

**问题分析**

- 短时间范围内
- 大量key集中过期

**解决方案（道）**

1. 更多的页面静态化处理
2. 构建**多级缓存架构** Nginx缓存+redis缓存+ehcache缓存
3. 检测Mysql严重耗时业务进行优化 对数据库的瓶颈排查：例如超时查询、耗时较高事务等
4. 灾难预警机制 监控redis服务器性能指标
   - CPU占用、CPU使用率
   - 内存容量
   - 查询平均响应时间
   - 线程数
5. 限流、降级 短时间范围内牺牲一些客户体验，限制一部分请求访问，降低应用服务器压力，待业务低速运转后再逐步放开访问



**解决方案（术）**

1. LRU与LFU切换

2. 数据有效期策略调整

   - 根据业务数据有效期进行**分类错峰**，A类90分钟，B类80分钟，C类70分钟
   - 过期时间使用固定时间+随机值的形式，**稀释**集中到期的key的数量

3. **超热**数据使用永久key

4. 定期维护（自动+人工）

    对即将过期数据做访问量分析，确认是否延时，配合访问量统计，做热点数据的延时

5. 加锁 **慎用！**

**总结**

缓存雪崩就是**瞬间过期数据量太大**，导致对数据库服务器造成压力。如能够**有效避免过期时间集中**，可以有效解决雪崩现象的出现 （约40%），配合其他策略一起使用，并监控服务器的运行数据，根据运行记录做快速调整。

![img](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//20200608143749.png)



#### 缓存击穿

**据库服务器崩溃（2）**

1. 系统平稳运行过程中
2. 数据库连接量**瞬间激增**
3. Redis服务器无大量key过期
4. Redis内存平稳，无波动
5. Redis服务器CPU正常
6. **数据库崩溃**

**问题排查**

1. Redis中**某个key过期，该key访问量巨大**
2. 多个数据请求从服务器直接压到Redis后，均未命中
3. Redis在短时间内发起了大量对数据库中同一数据的访问

**问题分析**

- 单个key高热数据
- key过期

**解决方案（术）**

1. 预先设定

   以电商为例，每个商家根据店铺等级，指定若干款主打商品，在购物节期间，**加大**此类信息key的**过期时长**

   注意：购物节不仅仅指当天，以及后续若干天，访问峰值呈现逐渐降低的趋势

2. 现场调整

   - 监控访问量，对自然流量激增的数据延长过期时间或设置为永久性key

3. 后台刷新数据

   - 启动定时任务，高峰期来临之前，刷新数据有效期，确保不丢失

4. 二级缓存

   - 设置不同的失效时间，保障不会被同时淘汰就行

5. 加锁 分布式锁，防止被击穿，但是要注意也是性能瓶颈，**慎重！**

**总结**

缓存击穿就是**单个高热数据过期的瞬间**，**数据访问量较大**，未命中redis后，发起了大量对同一数据的数据库访问，导致对数据库服务器造成压力。应对策略应该在**业务数据分析与预防方面**进行，配合运行**监控测试**与**即时调整策略**，毕竟单个key的过期监控难度较高，配合雪崩处理策略即可



#### **缓存穿透**

1. 系统平稳运行过程中
2. 应用服务器流量随时间增量较大3
3. Redis服务器命中率随时间逐步降低
4. Redis内存平稳，内存无压力
5. Redis服务器CPU占用激增
6. 数据库服务器压力激增
7. 数据库崩溃

**问题排查**

1. Redis中大面积出现未命中
2. 出现非正常URL访问

**问题分析**

- 获取的数据在数据库中也不存在,数据库查询未得到对应数据
- Redis获取到null数据未进行持久化，直接返回‘
- 下次此类数据到达重复上述过程
- 出现黑客攻击服务器
- 

**解决方案(术)**

1. 缓存null
      对查询结果为null的数据进行缓存（长期使用，定期清理)，设定短时限，例如30-60秒，最高5分钟

2. 白名单策略

   - 提前预热各种分类数据id对应的bitmaps，id作为bitmaps的offset，相当于设置了数据白名单。当加载正常数据时，放行，加载异常数据时直接拦截(效率偏低)
   - 使用**布隆过滤器**(有关布隆过滤器的命中问题对当前状况可以忽略)

3. 实施监控

   实时监控redis命中率(业务正常范围时，通常会有一个波动值）与null数据的占比

   - 非活动时段波动:通常检测3-5倍，超过5倍纳入重点排查对象
   - 活动时段波动:通常检测10-50倍，超过50倍纳入重点排查对象

   根据倍数不同，启动不同的排查流程。然后使用黑名单进行防控(运营)

4. .key加密

   问题出现后，临时启动防灾业务key，对key进行业务层传输加密服务，设定校验程序，过来的key校验
   例如每天随机分配60个加密串，挑选2到3个，混淆到页面数据id中，发现访问key不满足规则，驳回数据访问

**总结**
缓存击穿访问了不存在的数据，跳过了合法数据的redis数据缓存阶段，每次访问数据库，导致对数据库服务器造成压力。通常此类数据的出现量是一个较低的值，当出现此类情况以毒攻毒，并及时报警。应对策略应该在临时预案防范方面多做文章。
无论是黑名单还是白名单，都是对整体系统的压力，警报解除后尽快移除。



#### **性能指标监控**

**性能指标**

性能指标：Performance

![image-20210727160121926](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210727160121926.png)

内存指标：Memory

![image-20210727160612551](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210727160612551.png)

基本活动指标：Basic activity

![image-20210727160638194](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210727160638194.png)

持久性指标：Persistence

![image-20210727160849884](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210727160849884.png)


错误指标：Error


![image-20210727160913438](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210727160913438.png)

