# Mysql高级知识点 1

| 序号 | Day01              | Day02       | Day03          | Day04          |
| :--: | ------------------ | ----------- | -------------- | -------------- |
|  1   | Linux系统安装MySQL | 体系结构    | 应用优化       | MySQL 常用工具 |
|  2   | 索引               | 存储引擎    | 查询缓存优化   | MySQL 日志     |
|  3   | 视图               | 优化SQL步骤 | 内存管理及优化 | MySQL 主从复制 |
|  4   | 存储过程和函数     | 索引使用    | MySQL锁问题    | 综合案例       |
|  5   | 触发器             | SQL优化     | 常用SQL技巧    |                |

## 1.(Deepin环境下)Linux系统下安装Mysql

1. 下载Deepin的apt仓库包

    下载网址: https://dev.mysql.com/downloads/ 

   ![image-20210507143524518](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210507143524518.png)

2. 更换镜像源(阿里源)

   ```shell
   sudo vim /etc/apt/sources.list
   ```

   ![image-20210507144316534](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210507144316534.png)

   ```
   deb [by-hash=force] https://mirrors.aliyun.com/deepin apricot main contrib non-free
   ```

3. 更新

   ```
   sudo apt update
   sudo apt upgrade
   ```

4. cd到apt包的路径下

   ![image-20210507143849810](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210507143849810.png)

   ```
   安装命令
   sudo dpkg -i mysql-apt-config_0.8.17-1_all.deb 
   ```

   

   进入当前页面，选择mysql版本

   ![image-20210507145109763](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210507145109763.png)

   

   上面命令结束后使用

   ```
   sudo apt-get update
   ```

   ![image-20210507144828393](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210507144828393.png)

5. 安装Mysql的server和client

   ```
    sudo aptitude install mysql-server mysql-client
   ```

    设置mysql登陆密码： 

   ![image-20210507145300412](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210507145300412.png)

   ![image-20210507145322238](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210507145322238.png)

   

   之后安装成功，使用指令测试

   ```
   mysql -u root -p
   ```

   ![image-20210507145446465](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210507145446465.png)



### 1.1使用windows上连接linux中的mysql(远程连接)

1.  进入Linux中mysql

   ```
   mysql -u root -p 
   ```

2.  授权远程访问 

   ```
   grant all privileges on *.* to 'root' @'%' identified by 'yourMysqlpassword';
   
   ```

3. 记得关闭防火墙

   ```
   安装防火墙输入：sudo apt-get install ufw
   查看防火墙状态：sudo ufw status
   提示：Status: active 说明已经成功开启了
   提示：Status: inactive 说明已经关闭成功
   打开防火墙：sudo ufw enable
   关闭防火墙：sudo ufw disable
   ```

4. 测试连接

   ![image-20210507150208800](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210507150208800.png)

   ![image-20210507150218225](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210507150218225.png)

## 2.索引

### 2.1索引概述

官方术语：MySQL官方对索引的定义为：索引（index）帮助MySQL高效获取数据的数据结构（有序）。在数据之外，数据库系统还维护着满足特定查找算法的数据结构，这些数据结构以某种方式引用（指向）数据， 这样就可以在这些数据结构上实现高级查找算法，这种数据结构就是索引。如下面示意图所示 : 

![image-20210507150410767](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210507150410767.png)

索引：**就是一种指向数据的数据结构，能够高效获取数据**。





### 2.2索引优势劣势

**优势**

1） 类似于书籍的目录索引，提高数据检索的效率，降低数据库的IO成本。

2） 通过索引列对数据进行排序，降低数据排序的成本，降低CPU的消耗。

**劣势**

1） 实际上索引也是一张表，该表中保存了主键与索引字段，并指向实体类的记录，所以索引列也是要占用空间的。

2） 虽然索引大大提高了查询效率，同时却也降低更新表的速度，如对表进行INSERT、UPDATE、DELETE。因为更新表时，MySQL 不仅要保存数据，还要保存一下索引文件每次更新添加了索引列的字段，都会调整因为更新所带来的键值变化后的索引信息。





### 2.3索引结构

索引是在MySQL的**存储引擎层**中实现的，而不是在服务器层实现的。所以每种存储引擎的索引都不一定完全相同，也不是所有的存储引擎都支持所有的索引类型的。MySQL目前提供了以下**4种索引**：

- **BTREE 索引** ： 最常见的索引类型，大部分索引都支持 B 树索引。

- HASH 索引：只有Memory引擎支持 ， 使用场景简单 。

- R-tree 索引（空间索引）：空间索引是MyISAM引擎的一个特殊索引类型，主要用于地理空间数据类型，通常使用较少，不做特别介绍。

- Full-text （全文索引） ：全文索引也是MyISAM的一个特殊索引类型，主要用于全文索引**，InnoDB从Mysql5.6版本开始支持全文索引**。

  

  ​							**MyISAM、InnoDB、Memory三种存储引擎对各种索引类型的支持**

| 索引        | InnoDB引擎      | MyISAM引擎 | Memory引擎 |
| ----------- | --------------- | ---------- | ---------- |
| BTREE索引   | 支持            | 支持       | 支持       |
| HASH 索引   | 不支持          | 不支持     | 支持       |
| R-tree 索引 | 不支持          | 支持       | 不支持     |
| Full-text   | 5.6版本之后支持 | 支持       | 不支持     |

我们平常所说的索引，如果没有特别指明，都是指B+树（多路搜索树，并不一定是二叉的）结构组织的索引。其中聚簇索引、复合索引、前缀索引、唯一索引默认都是使用 B+tree 索引，统称为 索

### 2.3.1 BTREE 结构

BTree又叫多路平衡搜索树（**B-树**），一颗m叉的BTree特性如下：

- 树中每个节点最多包含m个孩子。
- 除根节点与叶子节点外，每个节点至少有[ceil(m/2)]个孩子。
- 若根节点不是叶子节点，则至少有两个孩子。
- 所有的叶子节点都在同一层。
- 每个非叶子节点由n个key与n+1个指针组成，其中[ceil(m/2)-1] <= n <= m-1 



以5叉BTree为例，key的数量：公式推导[ceil(m/2)-1] <= n <= m-1。所以 2 <= n <=4 。当n>4时，中间节点分裂到父节点，两边节点分裂。

插入 C N G A H E K Q M F W L T Z D P R X Y S 数据为例。

演变过程如下：

1). 插入前4个字母 C N G A 

插入前的顺序是混乱的，在插入时按照字母顺序插入，如下图

![image-20210508105821324](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210508105821324.png)

2). 插入H，H应该放在G之后，n>4，key的位置不够了，中间元素G字母向上分裂到新的节点



![image-20210508105809711](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210508105809711.png) 

3). 插入E，K，Q不需要分裂，原因是：key最大值为4，下面的位置都能够放下

上面有一条BTree的特点：**每个非叶子节点由n个key与n+1个指针组成，其中[ceil(m/2)-1] <= n <= m-1 **

以下图的G来说：key为：1  指针：2，

一个指针指向小于G的数据块，另一个指针指向大于G的数据块

![image-20210508105835885](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210508105835885.png)

4). 插入M，M插入到K和N的中间，n>4,key的位置不够，中间元素M字母向上分裂到父节点G，原来的四个数据分裂两个单独的数据块

M放到G的后面，key+1，指针数+1，key:2,指针数:3

![image-20210508105905801](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210508105905801.png)

5). 插入F，W，L，T不需要分裂

![image-20210508105922505](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210508105922505.png)

6). 插入Z，中间元素T向上分裂到父节点中 

![image-20210508105934092](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210508105934092.png)

7). 插入D，中间元素D向上分裂到父节点中。然后插入P，R，X，Y不需要分裂

![image-20210508105947385](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210508105947385.png)

8). 最后插入S，NPQR节点n>5，中间节点Q向上分裂，但分裂后父节点DGMT的n>5，中间节点M向上分裂

![image-20210508105958881](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210508105958881.png)

到此，该BTREE树就已经构建完成了， BTREE树 和 二叉树 相比， 查询数据的效率更高， 因为对于相同的数据量来说，BTREE的层级结构比二叉树小（**深度浅**），因此搜索速度快。



### 2.3.3 B+TREE 结构

B+Tree为BTree的变种，B+Tree与BTree的区别为：

1). m叉B+Tree最多含有n个key（**ceil(m/2) <= n <=m**），而BTree最多含有m-1个key。

2). B+Tree的叶子节点保存所有的key信息，依key大小顺序排列。

3). 所有的非叶子节点都可以看作是key的索引部分。

 ![image-20210508110038186](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210508110038186.png)

由于B+Tree只有叶子节点保存key信息，查询任何key都要从root走到叶子。所以B+Tree的查询效率更加稳定。



### 2.3.3 MySQL中的B+Tree

MySql索引数据结构对经典的B+Tree进行了优化。在原B+Tree的基础上，**增加一个指向相邻叶子节点的链表指针**，就形成了带有顺序指针的B+Tree，能够进行范围搜索，提高区间访问的性能。

MySQL中的 B+Tree 索引结构示意图: 

![image-20210508110053843](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210508110053843.png)





### 2.4 索引分类

1） **单列索引** ：即一个索引只包含单个列，一个表可以有多个单列索引

2） **唯一索引** ：索引列的值必须唯一，但允许有空值

**唯一索引的选择性是1，这是最好的索引选择性，性能也是最好的**

3） **复合索引** ：即一个索引包含多个列

环境：BTree索引下，数据是按照顺序存储的

**在使用复合索引时遵循最左前缀法则，按照复合索引中的最左列索引来排序，其实是第二列等等。**

**复合索引中多个索引定义的顺序不同，会导致查询的效率不同**

如果在不考虑Where条件后的排序和分组的条件下，一般将选择性高的(**区分度高的索引**)索引放在前面，当然这仅仅只限于不考虑排序和分组的情况，若考虑排序和分组的情况，它们的出现对于查询的效率就有很大的影响，就要另当考虑了。

4）**聚簇索引**

并不是单独的索引类型， 而是一种**数据存储方式**，将数据和索引存放到一起，当找到了索引就找到了数据。



**非聚簇索引(二级索引)**：它是将数据和索引分开，找到了索引并不代表找到了对应的行数据，需要通过**二次索引查找**才能够找到数据。

之所以进行二次索引查找的原因在于：**非聚簇索引中保存的不是指向行的物理地址的指针，而是行的主键值，这是第一次查找。通过这个主键值去聚簇索引中查找对应的行，这是第二次查找**



**聚簇索引具有唯一性，一个表中只能够有一个聚簇索引**

在InnoDB中，**聚簇索引默认是主键**，若表中没有定义主键，会选择一个唯一的非空索引作为聚簇索引，若上述的情况都不存在，InnoDB会隐式定义一个主键作为聚簇索引。InnoDB 只聚集在同一个页面中的记录。包含相邻键值的页面可能相距甚远。



聚簇索引既有优点又有缺点，正确的使用才能够保证性能的正向提升。

优点：

- **可以将相关数据保存在一起**，例如：通过用户ID来聚集数据，只需要从磁盘中读取少量的数据页就可以获取对应用户的全部数据。若不使用聚簇索引，对应用户的每个数据都要进行I/O操作。**在相同的结果集下，减少IO的过程就是我们最终的目的**
- **数据访问更快**。聚簇索引将数据和索引绑定到一起，比起非聚簇索引它的查询速度更快
- **取出一定范围数据的时候，使用用聚簇索引**

劣势：

- **若聚簇索引的长度过大，导致其他索引的长度也会变大，其他索引中叶子节点存储的是主键值**

- **插入的速度依赖于插入的顺序**，当前插入到顺序是按照主键顺序插入，插入的速度是最快的，若插入的顺序不是按照主键的顺序插入，每次插入都是乱序的，InnoDB不得不频繁的做**页分裂**，会导致大量的数据移动。虽然可以通过 **optimize 命令重新组织表，但这并不是我们想要看到的**。

- **更新聚簇索引的代价很高**，当前页中的数据已经达到饱和的状态，此时要在已经饱和的情况下保证新的数据的插入，进行页分裂，InnoDB必须要开辟新空间，将原来的数据进行移动，占用的空间就会更多。

- **会导致全表扫描变慢**，因为新数据的插入和页分裂，导致占用的空间变大以及存储数据不连续，导致了碎片化的存储空间。

  使用**UUId（随机ID）**作为主键，使数据存储稀疏。

  <img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210924143426346.png" alt="image-20210924143426346" style="zoom: 80%;" />

  **建议使用int的auto_increment作为主键进行顺序插入**

  <img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210924143546919.png" alt="image-20210924143546919" style="zoom:80%;" />

  主键的值是顺序的，所以 InnoDB 把每一条记录都存储在上一条记录的后面。当达到页的最大填充因子时（**InnoDB 默认的最大填充因子是页大小的 15/16，留出部分空间用于以后修改**），下一条记录就会写入新的页中。一旦数据按照这种顺序的方式加载，主键页就会近似于被顺序的记录填满（二级索引页可能是不一样的）

  

**InnoDB和MyISAM的数据分布对比**

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210924142055879.png" alt="image-20210924142055879" style="zoom: 67%;" />

InnoDB中采用**聚簇索引**搜索，将主键放到**B+树**结果的数据中，行数据就位于叶子节点上，通过主键索引一次检索就可以找到对应位置上的行数据

InnoDB中的**非聚簇索引**搜索，需要进行两次的索引检索，才能够找到对应的行数据，第一次在叶子节点中找到对应的聚簇索引的主键值，通过主键值去聚簇索引的数据中找到对应的行数据。



MyISAM中采用了**非聚簇索引**，由上图所知，聚簇索引和非聚簇索引在MyISAM中没有什么区别，两者都是B+树的结构，只是存储的内容的有所不同，主键索引B+树的节点存储了主键，辅助键索引B+树存储了辅助键。表数据存储在独立的地方，这两颗B+树的叶子节点都使用一个地址指向真正的表数据，对于表数据来说，这两个键没有任何差别。由于**索引树是独立的，通过辅助键检索无需访问主键的索引树**。



5）**覆盖索引**

一个索引包含所有需要查询的字段的值，该索引就是覆盖索引。

覆盖索引从非聚簇索引中就可以查询到聚簇索引中的行数据，减少了第二次回表查询的过程，性能得到提升。

好处

- 在InnoDB中，默认主键为聚簇索引，通过其他非聚簇索引查询数据时，需要进行两次查询才能够得到数据，有了覆盖索引在第一次查询时就可以通过主键值查询到行数据，避免了回表二次查询。
- 索引数目远小于行数目，只读取索引，就能够减少数据量的访问。

注意：**不是所有的类型索引都可以成为覆盖索引，哈希索引、空间索引、全文索引就无法转换成覆盖索引，因为它们无法存储索引列的值，能够转成覆盖索引的只有B-Tree索引**



### 2.5 索引语法

索引在创建表的时候，可以同时创建， 也可以随时增加新的索引。

准备环境:

```SQL
create database demo_01 default charset=utf8mb4;

use demo_01;

CREATE TABLE `city` (
  `city_id` int(11) NOT NULL AUTO_INCREMENT,
  `city_name` varchar(50) NOT NULL,
  `country_id` int(11) NOT NULL,
  PRIMARY KEY (`city_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

CREATE TABLE `country` (
  `country_id` int(11) NOT NULL AUTO_INCREMENT,
  `country_name` varchar(100) NOT NULL,
  PRIMARY KEY (`country_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;


insert into `city` (`city_id`, `city_name`, `country_id`) values(1,'西安',1);
insert into `city` (`city_id`, `city_name`, `country_id`) values(2,'NewYork',2);
insert into `city` (`city_id`, `city_name`, `country_id`) values(3,'北京',1);
insert into `city` (`city_id`, `city_name`, `country_id`) values(4,'上海',1);

insert into `country` (`country_id`, `country_name`) values(1,'China');
insert into `country` (`country_id`, `country_name`) values(2,'America');
insert into `country` (`country_id`, `country_name`) values(3,'Japan');
insert into `country` (`country_id`, `country_name`) values(4,'UK');
```



### 2.5.1 创建索引

语法 ： 	

```sql
CREATE 	[UNIQUE|FULLTEXT|SPATIAL]  INDEX index_name 
[USING  index_type]
ON tbl_name(index_col_name,...)


index_col_name : column_name[(length)][ASC | DESC]
```

示例 ： 为city表中的city_name字段创建索引 ；

![1551438009843](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//1551438009843.png)	  

​	

### 2.5.2 查看索引

语法： 

```
show index  from  table_name;
```

示例：查看city表中的索引信息；

![1551440511890](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//1551440511890.png)

![1551440544483](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//1551440544483.png)

### 2.5.3 删除索引

语法 ：

```
DROP  INDEX  index_name  ON  tbl_name;
```

示例 ： 想要删除city表上的索引idx_city_name，可以操作如下：

![1551438238293](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//1551438238293.png) 



### 2.5.4 ALTER命令

```
1). alter  table  tb_name  add  primary  key(column_list); 

	该语句添加一个主键，这意味着索引值必须是唯一的，且不能为NULL
	
2). alter  table  tb_name  add  unique index_name(column_list);
	
	这条语句创建索引的值必须是唯一的（除了NULL外，NULL可能会出现多次）
	
3). alter  table  tb_name  add  index index_name(column_list);

	添加普通索引， 索引值可以出现多次。
	
4). alter  table  tb_name  add  fulltext  index_name(column_list);
	
	该语句指定了索引为FULLTEXT， 用于全文索引
	
```



### 2.6 索引设计原则

	索引的设计可以遵循一些已有的原则，创建索引的时候请尽量考虑符合这些原则，便于提升索引的使用效率，更高效的使用索引。

- 对查询频次较高，且数据量比较大的表建立索引。

- 索引字段的选择，最佳候选列应当从where子句的条件中提取，如果where子句中的组合比较多，那么应当挑选最常用、过滤效果最好的列的组合。

- 使用唯一索引，区分度越高，使用索引的效率越高。

- 索引可以有效的提升查询数据的效率，但索引数量不是多多益善，索引越多，维护索引的代价自然也就水涨船高。对于插入、更新、删除等DML操作比较频繁的表来说，索引过多，会引入相当高的维护代价，降低DML操作的效率，增加相应操作的时间消耗。另外索引过多的话，MySQL也会犯选择困难病，虽然最终仍然会找到一个可用的索引，但无疑提高了选择的代价。

- 使用短索引，索引创建之后也是使用硬盘来存储的，因此提升索引访问的I/O效率，也可以提升总体的访问效率。假如构成索引的字段总长度比较短，那么在给定大小的存储块内可以存储更多的索引值，相应的可以有效的提升MySQL访问索引的I/O效率。

- 利用最左前缀，N个列组合而成的组合索引，那么相当于是创建了N个索引，如果查询时where子句中使用了组成该索引的前几个字段，那么这条查询SQL可以利用组合索引来提升查询效率。

  ```
  创建复合索引:
  
  	CREATE INDEX idx_name_email_status ON tb_seller(NAME,email,STATUS);
  
  就相当于
  	对name 创建索引 ;
  	对name , email 创建了索引 ;
  	对name , email, status 创建了索引 ;
  ```


## 3. 视图

### 3.1 视图概述

	视图（View）是一种虚拟存在的表。视图并不在数据库中实际存在，行和列数据来自定义视图的查询中使用的表，并且是在使用视图时动态生成的。通俗的讲，视图就是一条SELECT语句执行后返回的结果集。所以我们在创建视图的时候，主要的工作就落在创建这条SQL查询语句上。

视图相对于普通的表的优势主要包括以下几项。

- 简单：使用视图的用户完全不需要关心后面对应的表的结构、关联条件和筛选条件，对用户来说已经是过滤好的复合条件的结果集。
- 安全：使用视图的用户只能访问他们被允许查询的结果集，对表的权限管理并不能限制到某个行某个列，但是通过视图就可以简单的实现。
- 数据独立：一旦视图的结构确定了，可以屏蔽表结构变化对用户的影响，源表增加列对视图没有影响；源表修改列名，则可以通过修改视图来解决，不会造成对访问者的影响。

### 3.2 创建或者修改视图

创建视图的语法为：

```sql
CREATE [OR REPLACE] [ALGORITHM = {UNDEFINED | MERGE | TEMPTABLE}]

VIEW view_name [(column_list)]

AS select_statement

[WITH [CASCADED | LOCAL] CHECK OPTION]
```

修改视图的语法为：

```sql
ALTER [ALGORITHM = {UNDEFINED | MERGE | TEMPTABLE}]

VIEW view_name [(column_list)]

AS select_statement

[WITH [CASCADED | LOCAL] CHECK OPTION]
```

```
选项 : 
	WITH [CASCADED | LOCAL] CHECK OPTION 决定了是否允许更新数据使记录不再满足视图的条件。
	
	LOCAL ： 只要满足本视图的条件就可以更新。
	CASCADED ： 必须满足所有针对该视图的所有视图的条件才可以更新。 默认值.
```

示例 , 创建city_country_view视图 , 执行如下SQL : 

```sql
create or replace view city_country_view 
as 
select t.*,c.country_name from country c , city t where c.country_id = t.country_id;

```

查询视图 : 

![1551503428635](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//1551503428635.png)



### 3.3 查看视图

	从 MySQL 5.1 版本开始，使用 SHOW TABLES 命令的时候不仅显示表的名字，同时也会显示视图的名字，而不存在单独显示视图的 SHOW VIEWS 命令。

![1551537565159](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//1551537565159.png)

同样，在使用 SHOW TABLE STATUS 命令的时候，不但可以显示表的信息，同时也可以显示视图的信息。	

![1551537646323](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//1551537646323.png)

如果需要查询某个视图的定义，可以使用 SHOW CREATE VIEW 命令进行查看 ： 

![1551588962944](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//1551588962944.png)

### 3.4 删除视图

语法 : 

```sql
DROP VIEW [IF EXISTS] view_name [, view_name] ...[RESTRICT | CASCADE]	
```

示例 , 删除视图city_country_view :

```
DROP VIEW city_country_view ;
```



## 4. 存储过程和函数

### 4.1 存储过程和函数概述

	存储过程和函数是  事先经过编译并存储在数据库中的一段 SQL 语句的集合，调用存储过程和函数可以简化应用开发人员的很多工作，减少数据在数据库和应用服务器之间的传输，对于提高数据处理的效率是有好处的。	
	
	存储过程和函数的区别在于函数必须有返回值，而存储过程没有。
	
	函数 ： 是一个有返回值的过程 ；
	
	过程 ： 是一个没有返回值的函数 ；

### 4.2 创建存储过程

```sql
CREATE PROCEDURE procedure_name ([proc_parameter[,...]])
begin
	-- SQL语句
end ;
```



示例 ：

```sql 
delimiter $

create procedure pro_test1()
begin
	select 'Hello Mysql' ;
end$

delimiter ;
```



<strong><font color="red">知识小贴士</font></strong>

DELIMITER

	该关键字用来声明SQL语句的分隔符 , 告诉 MySQL 解释器，该段命令是否已经结束了，mysql是否可以执行了。默认情况下，delimiter是分号;。在命令行客户端中，如果有一行命令以分号结束，那么回车后，mysql将会执行该命令。



### 4.3 调用存储过程

```sql
call procedure_name() ;	
```

### 4.4 查看存储过程

```sql
-- 查询db_name数据库中的所有的存储过程
select name from mysql.proc where db='db_name';


-- 查询存储过程的状态信息
show procedure status;


-- 查询某个存储过程的定义
show create procedure test.pro_test1 \G;
```

### 4.5 删除存储过程

```sql
DROP PROCEDURE  [IF EXISTS] sp_name ；
```



### 4.6 语法

存储过程是可以编程的，意味着可以使用变量，表达式，控制结构 ， 来完成比较复杂的功能。

### 4.6.1 变量

-  DECLARE

  通过 DECLARE 可以定义一个局部变量，该变量的作用范围只能在 BEGIN…END 块中。

```sql
DECLARE var_name[,...] type [DEFAULT value]
```

示例 : 

```sql
 delimiter $

 create procedure pro_test2() 
 begin 
 	declare num int default 5;
 	select num+ 10; 
 end$

 delimiter ; 
```



- SET

直接赋值使用 SET，可以赋常量或者赋表达式，具体语法如下：

```
  SET var_name = expr [, var_name = expr] ...
```

示例 : 

```sql
  DELIMITER $
  
  CREATE  PROCEDURE pro_test3()
  BEGIN
  	DECLARE NAME VARCHAR(20);
  	SET NAME = 'MYSQL';
  	SELECT NAME ;
  END$
  
  DELIMITER ;
```



也可以通过select ... into 方式进行赋值操作 :

```SQL
DELIMITER $

CREATE  PROCEDURE pro_test5()
BEGIN
	declare  countnum int;
	select count(*) into countnum from city;
	select countnum;
END$

DELIMITER ;
```



### 4.6.2 if条件判断

语法结构 : 

```sql
if search_condition then statement_list

	[elseif search_condition then statement_list] ...
	
	[else statement_list]
	
end if;
```

需求： 

```
根据定义的身高变量，判定当前身高的所属的身材类型 

	180 及以上 ----------> 身材高挑

	170 - 180  ---------> 标准身材

	170 以下  ----------> 一般身材
```

示例 : 

```sql
delimiter $

create procedure pro_test6()
begin
  declare  height  int  default  175; 
  declare  description  varchar(50);
  
  if  height >= 180  then
    set description = '身材高挑';
  elseif height >= 170 and height < 180  then
    set description = '中等身材';
  else
    set description = '一般身材';
  end if;
  
  select description ;
end$

delimiter ;
```

调用结果为 : 

![1552057035580](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//1552057035580.png)



### 4.6.3 传递参数

语法格式 : 

```
create procedure procedure_name([in/out/inout] 参数名   参数类型)
...


IN :   该参数可以作为输入，也就是需要调用方传入值 , 默认
OUT:   该参数作为输出，也就是该参数可以作为返回值
INOUT: 既可以作为输入参数，也可以作为输出参数
```

**IN - 输入**

需求 :

```
根据定义的身高变量，判定当前身高的所属的身材类型 
```

示例  : 

```sql
delimiter $

create procedure pro_test5(in height int)
begin
    declare description varchar(50) default '';
  if height >= 180 then
    set description='身材高挑';
  elseif height >= 170 and height < 180 then
    set description='中等身材';
  else
    set description='一般身材';
  end if;
  select concat('身高 ', height , '对应的身材类型为:',description);
end$

delimiter ;
```



**OUT-输出**

 需求 :

```
根据传入的身高变量，获取当前身高的所属的身材类型  
```

示例:

```SQL 
create procedure pro_test5(in height int , out description varchar(100))
begin
  if height >= 180 then
    set description='身材高挑';
  elseif height >= 170 and height < 180 then
    set description='中等身材';
  else
    set description='一般身材';
  end if;
end$	
```

调用:

```
call pro_test5(168, @description)$

select @description$
```

<font color='red'>**小知识** </font>

@description :  这种变量要在变量名称前面加上“@”符号，叫做用户会话变量，代表整个会话过程他都是有作用的，这个类似于全局变量一样。

@@global.sort_buffer_size : 这种在变量前加上 "@@" 符号, 叫做 系统变量 



### 4.6.4 case结构

语法结构 : 

```SQL
方式一 : 

CASE case_value

  WHEN when_value THEN statement_list
  
  [WHEN when_value THEN statement_list] ...
  
  [ELSE statement_list]
  
END CASE;


方式二 : 

CASE

  WHEN search_condition THEN statement_list
  
  [WHEN search_condition THEN statement_list] ...
  
  [ELSE statement_list]
  
END CASE;

```

需求:

```
给定一个月份, 然后计算出所在的季度
```

示例  :

```sql
delimiter $


create procedure pro_test9(month int)
begin
  declare result varchar(20);
  case 
    when month >= 1 and month <=3 then 
      set result = '第一季度';
    when month >= 4 and month <=6 then 
      set result = '第二季度';
    when month >= 7 and month <=9 then 
      set result = '第三季度';
    when month >= 10 and month <=12 then 
      set result = '第四季度';
  end case;
  
  select concat('您输入的月份为 :', month , ' , 该月份为 : ' , result) as content ;
  
end$


delimiter ;
```



### 4.6.5 while循环

语法结构: 

```sql
while search_condition do

	statement_list
	
end while;
```

需求:

```
计算从1加到n的值
```

示例  : 

```sql
delimiter $

create procedure pro_test8(n int)
begin
  declare total int default 0;
  declare num int default 1;
  while num<=n do
    set total = total + num;
	set num = num + 1;
  end while;
  select total;
end$

delimiter ;
```



### 4.6.6 repeat结构

有条件的循环控制语句, 当满足条件的时候退出循环 。while 是满足条件才执行，repeat 是满足条件就退出循环。

语法结构 : 

```SQL
REPEAT

  statement_list

  UNTIL search_condition

END REPEAT;
```

需求: 

```
计算从1加到n的值
```

示例  : 

```sql
delimiter $

create procedure pro_test10(n int)
begin
  declare total int default 0;
  
  repeat 
    set total = total + n;
    set n = n - 1;
    until n=0  
  end repeat;
  
  select total ;
  
end$


delimiter ;
```



### 4.6.7 loop语句

LOOP 实现简单的循环，退出循环的条件需要使用其他的语句定义，通常可以使用 LEAVE 语句实现，具体语法如下：

```sql
[begin_label:] LOOP

  statement_list

END LOOP [end_label]
```

如果不在 statement_list 中增加退出循环的语句，那么 LOOP 语句可以用来实现简单的死循环。



### 4.6.8 leave语句

用来从标注的流程构造中退出，通常和 BEGIN ... END 或者循环一起使用。下面是一个使用 LOOP 和 LEAVE 的简单例子 , 退出循环：

```SQL
delimiter $

CREATE PROCEDURE pro_test11(n int)
BEGIN
  declare total int default 0;
  
  ins: LOOP
    
    IF n <= 0 then
      leave ins;
    END IF;
    
    set total = total + n;
    set n = n - 1;
  	
  END LOOP ins;
  
  select total;
END$

delimiter ;
```



### 4.6.9 游标/光标

游标是用来存储查询结果集的数据类型 , 在存储过程和函数中可以使用光标对结果集进行循环的处理。光标的使用包括光标的声明、OPEN、FETCH 和 CLOSE，其语法分别如下。

声明光标：

```sql
DECLARE cursor_name CURSOR FOR select_statement ;
```

OPEN 光标：

```sql
OPEN cursor_name ;
```

FETCH 光标：

```sql
FETCH cursor_name INTO var_name [, var_name] ...
```

CLOSE 光标：

```sql
CLOSE cursor_name ;
```



示例 : 

初始化脚本:

``` sql
create table emp(
  id int(11) not null auto_increment ,
  name varchar(50) not null comment '姓名',
  age int(11) comment '年龄',
  salary int(11) comment '薪水',
  primary key(`id`)
)engine=innodb default charset=utf8 ;

insert into emp(id,name,age,salary) values(null,'金毛狮王',55,3800),(null,'白眉鹰王',60,4000),(null,'青翼蝠王',38,2800),(null,'紫衫龙王',42,1800);

```



``` SQL
-- 查询emp表中数据, 并逐行获取进行展示
create procedure pro_test11()
begin
  declare e_id int(11);
  declare e_name varchar(50);
  declare e_age int(11);
  declare e_salary int(11);
  declare emp_result cursor for select * from emp;
  
  open emp_result;
  
  fetch emp_result into e_id,e_name,e_age,e_salary;
  select concat('id=',e_id , ', name=',e_name, ', age=', e_age, ', 薪资为: ',e_salary);
  
  fetch emp_result into e_id,e_name,e_age,e_salary;
  select concat('id=',e_id , ', name=',e_name, ', age=', e_age, ', 薪资为: ',e_salary);
  
  fetch emp_result into e_id,e_name,e_age,e_salary;
  select concat('id=',e_id , ', name=',e_name, ', age=', e_age, ', 薪资为: ',e_salary);
  
  fetch emp_result into e_id,e_name,e_age,e_salary;
  select concat('id=',e_id , ', name=',e_name, ', age=', e_age, ', 薪资为: ',e_salary);
  
  fetch emp_result into e_id,e_name,e_age,e_salary;
  select concat('id=',e_id , ', name=',e_name, ', age=', e_age, ', 薪资为: ',e_salary);
  
  close emp_result;
end$

```



通过循环结构 , 获取游标中的数据 : 

```sql
DELIMITER $

create procedure pro_test12()
begin
  DECLARE id int(11);
  DECLARE name varchar(50);
  DECLARE age int(11);
  DECLARE salary int(11);
  DECLARE has_data int default 1;
  
  DECLARE emp_result CURSOR FOR select * from emp;
  DECLARE EXIT HANDLER FOR NOT FOUND set has_data = 0;
  
  open emp_result;
  
  repeat
    fetch emp_result into id , name , age , salary;
    select concat('id为',id, ', name 为' ,name , ', age为 ' ,age , ', 薪水为: ', salary);
    until has_data = 0
  end repeat;
  
  close emp_result;
end$

DELIMITER ; 
```



### 4.7 存储函数

语法结构:

``` 
CREATE FUNCTION function_name([param type ... ]) 
RETURNS type 
BEGIN
	...
END;
```

案例 : 

定义一个存储过程, 请求满足条件的总记录数 ;

```SQL

delimiter $

create function count_city(countryId int)
returns int
begin
  declare cnum int ;
  
  select count(*) into cnum from city where country_id = countryId;
  
  return cnum;
end$

delimiter ;
```

调用: 

```
select count_city(1);

select count_city(2);
```



## 5. 触发器

### 5.1 介绍

触发器是与表有关的数据库对象，指在 insert/update/delete 之前或之后，触发并执行触发器中定义的SQL语句集合。触发器的这种特性可以协助应用在数据库端确保数据的完整性 , 日志记录 , 数据校验等操作 。

使用别名 OLD 和 NEW 来引用触发器中发生变化的记录内容，这与其他的数据库是相似的。现在触发器还只支持行级触发，不支持语句级触发。

| 触发器类型      | NEW 和 OLD的使用                                        |
| --------------- | ------------------------------------------------------- |
| INSERT 型触发器 | NEW 表示将要或者已经新增的数据                          |
| UPDATE 型触发器 | OLD 表示修改之前的数据 , NEW 表示将要或已经修改后的数据 |
| DELETE 型触发器 | OLD 表示将要或者已经删除的数据                          |



### 5.2 创建触发器

语法结构 : 

```sql
create trigger trigger_name 

before/after insert/update/delete

on tbl_name 

[ for each row ]  -- 行级触发器

begin

	trigger_stmt ;

end;
```



示例 

需求

```
通过触发器记录 emp 表的数据变更日志 , 包含增加, 修改 , 删除 ;
```

首先创建一张日志表 : 

```sql
create table emp_logs(
  id int(11) not null auto_increment,
  operation varchar(20) not null comment '操作类型, insert/update/delete',
  operate_time datetime not null comment '操作时间',
  operate_id int(11) not null comment '操作表的ID',
  operate_params varchar(500) comment '操作参数',
  primary key(`id`)
)engine=innodb default charset=utf8;
```

创建 insert 型触发器，完成插入数据时的日志记录 : 

```sql
DELIMITER $

create trigger emp_logs_insert_trigger
after insert 
on emp 
for each row 
begin
  insert into emp_logs (id,operation,operate_time,operate_id,operate_params) values(null,'insert',now(),new.id,concat('插入后(id:',new.id,', name:',new.name,', age:',new.age,', salary:',new.salary,')'));	
end $

DELIMITER ;
```

创建 update 型触发器，完成更新数据时的日志记录 : 

``` sql
DELIMITER $

create trigger emp_logs_update_trigger
after update 
on emp 
for each row 
begin
  insert into emp_logs (id,operation,operate_time,operate_id,operate_params) values(null,'update',now(),new.id,concat('修改前(id:',old.id,', name:',old.name,', age:',old.age,', salary:',old.salary,') , 修改后(id',new.id, 'name:',new.name,', age:',new.age,', salary:',new.salary,')'));                                                                      
end $

DELIMITER ;
```

创建delete 行的触发器 , 完成删除数据时的日志记录 : 

```sql
DELIMITER $

create trigger emp_logs_delete_trigger
after delete 
on emp 
for each row 
begin
  insert into emp_logs (id,operation,operate_time,operate_id,operate_params) values(null,'delete',now(),old.id,concat('删除前(id:',old.id,', name:',old.name,', age:',old.age,', salary:',old.salary,')'));                                                                      
end $

DELIMITER ;
```



测试：

```sql
insert into emp(id,name,age,salary) values(null, '光明左使',30,3500);
insert into emp(id,name,age,salary) values(null, '光明右使',33,3200);

update emp set age = 39 where id = 3;

delete from emp where id = 5;
```



### 5.3 删除触发器

语法结构 : 

```
drop trigger [schema_name.]trigger_name
```

如果没有指定 schema_name，默认为当前数据库 。

### 5.4 查看触发器

可以通过执行 SHOW TRIGGERS 命令查看触发器的状态、语法等信息。

语法结构 ： 

```
show triggers ；
```

 

## 6.范式

### 第一范式（1st NF）

保证表格中的每一列都是原子列，不可以再分更小的数据单元

![image-20210924161716580](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210924161716580.png)

上图中地址列，不符合第一范式的规定，可以进行再分。

### 第二范式（2st NF）

在保证第一范式的基础上，保证表格中**非主键列不存在对主键的部分依赖，而是全部依赖，若存在部份依赖，需要分出新的表格**

**保证每个表格只表述一件事情**

![image-20210924161952941](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210924161952941.png)

上图中价格非主键列对于主键订单编号不存在依赖关系，因此需要分表。



### 第三范式（3st NF）

在满足第二范式的基础上，保证表格中的**列不存在对非主键的传递依赖关系**。

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210924162846580.png" alt="image-20210924162846580" style="zoom:80%;" />

上图中出现了顾客姓名依赖于非主键列的顾客编号。



好处：

**范式可以避免数据冗余，减少数据库的空间，减轻维护数据完整性的麻烦。**



缺点：

越高级的范式设计出来的表越多，表数量越多对于我们查询数据来说就越复杂，涉及到多表查询的情况，多表查询相比于单表查询的速度要低得多。所以我们在利用范式设计表的时候，要根据具体的需求再去权衡是否使用更高范式去设计表。在一般的项目中，我们用的最多也就是第三范式，第三范式也就可以满足我们的项目需求，性能好而且方便管理数据；

###  **反范式**  

​    **所谓反范式**，故名思义，跟范式所要求的正好相反，在反范式的设计模式，我们可以允许适当的数据的冗余，用这个冗余去取操作数据时间的缩短。**也就是利用空间来换取时间**,把数据冗余在多个表中，当查询时可以减少或者是避免表之间的关联；

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210925162604202.png" alt="image-20210925162604202" style="zoom: 80%;" />

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210925162615008.png" alt="image-20210925162615008" style="zoom:80%;" />

字段冗余设计，在订单表中直接加入商品名称，避免了每次查询都要关联订单表和商品表。

**查多改少的场景，适合用字段冗余**



## 7.数据切分(垂直切分、水平切分)

### 数据切分含义

关系型数据库本身比较容易造成**系统瓶颈、单机存储容量、连接数、处理能力都有限**。

当**单表**中的数据量达到了1000w或者100G以后，由于查询维度较多，数据量很大，**即使通过添加从库、优化索引也没办法很好的提升查询效率时**，就要考虑进行**数据切分**。

数据切分：将数据分散到多个数据库中，使得单一的数据库中的数据量变小，通过扩充数据库的数量来缓解单一数据库的性能问题，从而达到提升数据库操作性能。

目的：减少单一数据库的负担，提升查询的效率。

数据切分类型：**垂直切分和水平切分**



### 垂直切分

垂直切分常见的有**垂直分库和垂直分表**

#### 垂直分库

将**关联度低的不同表**存放在不同的数据库中

例如，我们会建立定义**数据库 workDB、商品数据库 payDB、用户数据库 userDB、日志数据库 logDB** 等，分别用于

存储项目**数据定义表、商品定义表、用户数据表、日志数据表**等。

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210925152139776.png" alt="image-20210925152139776" style="zoom:80%;" />

#### 垂直分表

根据**数据库中表的列**来进行划分的。

比如：某个表格中的字段较多，可以将当中不常用的字段或者字段较大较长的分离出去，放到一张扩展表中。

好处：

1. Mysql底层中通过**数据页**来存储数据的，若字段较长的没有被划分出去，所有的数据都在一张表中，达到了单页的最大程度，就会进行页分裂，会占用新的空间，造成额外的开销。
2. 将不常用的字段和字段长度较大的划分出去之后，原表格中剩下的都是访问频率较高和长度较短的字段，单页中能够加载更多的数据，查询效率上也会高很多，减少io消耗，提升数据库的性能。

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210925153035492.png" alt="image-20210925153035492" style="zoom:67%;" />

**总结**

垂直切分的优点

1. 业务层面的解耦合，将各个表格分库存储。
2. 单个表格垂直分割，在高并发情况，一定程度上提升IO性能

缺点

1. 部分表无法join，只能通过接口聚合方式解决，增加了开发的复杂度
2. 分布式事务处理复杂
3. **依然存在单表数据量过大的问题**



### 水平切分

当一个数据库难以在**细粒度垂直切分或者切分后存在单表的数据量任然庞大的问题时**,造成单库读写、存储性能的瓶颈时，这时就需要通过**水平切分**

水平切分可以分为：**库内分表和分库分表**

水平切分是根据表内数据内在的逻辑关系，将同一个表按照不同的条件分散到多个数据库中或多个表格中，每个表中只包含一部分数据，这就可以将单个过于庞大数据表单，分散到各个地方，使得单个表的数据量变小，达到分布式的效果。

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210925154544139.png" alt="image-20210925154544139" style="zoom:67%;" />

根据上面描述的，将单个庞大的数据表单，分散大到各个表中，这些还是在同一个库中，这就是**库内分表**。

虽然解决了单一表单数据量过大的问题，但是对于缓解单一数据库的压力并没有提升。

**因此最好使用分库分表**，将数据分布到各个数据库中，减少单一数据库的压力。



水平切分后同一张表会出现在多个数据库/表中，每个库/表的内容不同。几种典型**的数据分片规则**为：

1. **根据数值范围**

   **按照时间区域或者ID来切分**。

   例如：按日期将不同月甚至是日的数据分散到不同的库中；将userId为1~9999的记录分到第一个库，10000~20000的分到第二个库，以此类推。某种意义上，某些系统中使用的"冷热数据分离"，将一些使用较少的历史数据迁移到其他库中，业务功能上只提供热点数据的查询，也是类似的实践。

   优点：

   **最大的优点在于便于后期扩容，只需要添加节点即可，无需对其他分片的数据进行迁移**

   使用**分片字段**进行范围查找，连续分片可快速定位分片进行快速查询，有效避免跨分片查询的问题。

   

2. **根据数值取模**

   一般采用**hash取模的分片方式**。

   例如：将 Customer 表根据 cusno 字段切分到4个库中，余数为0的放到第一个库，余数为1的放到第二个库，以此类推。这样同一个用户的数据会分散到同一个库中，如果查询条件带有cusno字段，则可明确定位到相应库去查询。

   优点：

   相比于数据范围分片，数值取模，**能让数据分布的更加均匀**，不容易出现热点和并发访问的瓶颈

   缺点：

   **后期进行扩容时，需要迁移旧的数据**（**使用一致性hash算法能较好的避免这个问题**）

   **容易面临跨分片查询的复杂问题。**

   比如上例中，如果频繁用到的查询条件中不带cusno时，将会导致无法定位数据库，从而需要同时向4个库发起查询，再在内存中合并数据，取最小集返回给应用，分库反而成为拖累。



#### 分库分表

采用分库分表能够解决单一表单数据量过大的问题，减轻单一数据库的压力。同时这样做也会带来一些问题

1. **事务一致性的问题**

    **分布式事务**

   当对于分表的数据进行事务操作时，因为数据分散到了各个库中，不可避免会带来跨库事务问题。

   一般的解决方案有：**XA协议**和 **两阶段提交**

   XA协议：交易中间件与数据库之间的接口规范（即接口函数），交易中间件用它来通知数据库事务的开始、结束以及提交、回滚等。

   **两阶段提交**

   在计算机网络以及数据库领域内，为了使**基于分布式系统架构下**的**所有节点在进行事务提交时保持一致性**而设计的一种算法(Algorithm)。

   在分布式系统中，每个节点可以知晓自身的情况，但是却无法知晓其他节点的情况。**这时引入一个协调者的组件来统一掌握所有界节点的操作并且指示这些节点是否要把操作结果进行真正的提交**。

   二阶段提交的**算法思路可以概括**为：参与者将操作成败通知协调者，再由协调者根据所有参与者的反馈情报决定各参与者是否要提交操作还是中止操作。

   两个阶段分别是：**准备阶段和提交阶段**

    分布式事务最大限度保证了**数据库操作的原子性**。但是在提交事务时需要协调多个节点，推后了提交事务的时间点，延迟了事务的执行时间。

   

   **最终一致性**

   对于那些性能要求很高，但对一致性要求不高的系统，往往不苛求系统的实时一致性，只要在允许的时间段内达到最终一致性即可，可采用事务补偿的方式。

2. **跨节点关联查询join问题**

   切分之前，需要进行多方面的查询关联多个数据，一般通过join来进行关联查询。在切分之后，数据可能分布在不同库不同节点上，此时join查询就会带来性能上面的问题。

   解决方案：

   - **全局表**

     全局表，也可看做是"数据字典表"，就是系统中所有模块都可能依赖的一些表，为了避免跨库join查询，可以将这类表在每个数据库中都保存一份。

   - **字段冗余**

     反范式设计，**利用空间换取时间**

   - **数据组装**

     分两次查询，第一次查询的结果集中找出关联数据id，然后根据id发起第二次请求得到关联数据。最后将获得到的数据进行字段拼装。

   - **ER分片**

     关系型数据库中，如果可以先确定表之间的关联关系，并将那些存在关联关系的表记录存放在同一个分片上，那么就能较好的避免跨分片join问题。

3. **跨节点分页、排序、函数问题**

   业务避免不了对数据进行分页、排序等操作，在跨节点多库中进行**分页排序**查询时，如果排序的字段是按照**分片字段**来查询时，能够很快定位到目标数据，但是排序的字段不是按照分片字段来查询时，在多库中查询时就比较复杂，需要先在不同的分片节点中将数据进行排序并返回，然后将不同分片返回的结果集进行汇总和再次排序，最终返回给用户。

   在使用**Max、Min、Sum、Count之类的函数进行计算的时候**，也需要先在每个分片上执行相应的函数，然后将各个分片的结果集进行汇总和再次计算，最终将结果返回。

4. **全局主键避免重复问题**

    在分库分表的环境中，由于表中的数据分布在不同的库中，一般的主键值在这种情况下就无法保证唯一性。因此需要单独设计**全局主键**，**避免跨库主键重复问题**。

   常见的策略：

   - **UUID**

     UUID标准形式包含32个16进制数字，分为5段，形式为8-4-4-4-12的36个字符，例如：550e8400-e29b-41d4-a716-446655440000

     UUID是主键是最简单的方案，本地生成，性能高，没有网络耗时。

     有很明显的缺点，UUID本身长度过长，会占据大量的存储空间，其次它本身数据的是无序，最典型的在InnoDB中，UUID的无序性会引起数据存储位置的频繁变动，导致页分裂，存储内存碎片化。

   - **数据库自增id**

     建立2个以上的全局ID生成的服务器，每个服务器上只部署一个数据库，每个库有一张sequence表用于记录当前全局ID。表中ID增长的步长是库的数量，起始值依次错开，这样能将ID的生成散列到各个数据库上。

   - **利用Redis生成id**

     性能较好，灵活方便，不依赖于数据库。可用性低，编码更加复杂，增加了成本

5. **数据迁移、扩容问题**

    当业务高速发展，面临性能和存储的瓶颈时，才会考虑分片设计，此时就不可避免的需要考虑历史数据迁移的问题。一般做法是先读出历史数据，然后按指定的分片规则再将数据写入到各个分片节点中。

   如果采用数值范围分片，只需要添加节点就可以进行扩容了，不需要对分片数据迁移。如果采用的是数值取模分片，则考虑后期的扩容问题就相对比较麻烦。





### 什么时候考虑数据切分

- **能不切分尽量不要切分**

  并不是所有的表格都要切分，主要还是看数据的增长速度。因为将表格切分后，表格/数据库的数量就增加了，从业务层面来考虑业务的复杂度就上升了。

  **分库分表是最后的办法，在这之前需要将能够做到的事情都做到，例如：升级硬件、升级网络、读写分离、索引优化等等**。当单表的数据量过大，数据库的性能达到瓶颈时，在考虑分表分库。

- **数据量过大，正常运维影响业务访问**

  - 对数据库备份，如果单表太大，备份时需要大量的磁盘IO和网络IO。例如1T的数据，网络传输占50MB时候，需要20000秒才能传输完毕，整个过程的风险都是比较高的
  - 大表会经常访问与更新，就更有可能出现锁等待。将数据切分，用空间换时间，变相降低访问压力

- **随着业务发展，需要对某些字段垂直拆分**

  举个例子，假如项目一开始设计的用户表如下：

  ```javascript
  id                   bigint             #用户的ID
  name                 varchar            #用户的名字
  last_login_time      datetime           #最近登录时间
  personal_info        text               #私人信息
  .....                                   #其他信息字段
  ```

  在项目初始阶段，这种设计是满足简单的业务需求的，也方便快速迭代开发。而当业务快速发展时，用户量从10w激增到10亿，用户非常的活跃，每次登录会更新  last_login_name 字段，使得 user 表被不断update，压力很大。而其他字段：id, name,  personal_info 是不变的或很少更新的，此时在业务角度，就要将 last_login_time 拆分出去，新建一个 user_time  表。

  personal_info 属性是更新和查询频率较低的，并且text字段占据了太多的空间。这时候，就要对此垂直拆分出 user_ext 表了。

- **数据量快速增长**

- **安全性和可用性**





