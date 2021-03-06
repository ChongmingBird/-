# 【MySQL】

## 简介

> **数据库：**
>
> - 存档数据的仓库，数据是有组织的进行存储
> - 英文：DataBase，简称DB
>
> **数据库管理系统：**
>
> - 管理数据库的大型软件
> - 英文：DataBase Management System， 简称DBMS
>
> **关系型数据库：** 关系型数据库是建立在关系模型上的数据库。简单来说，关系型数据库是由多张互相连接的二维表组成的数据库。
>
> ​		表的每一行称为记录（Record），记录是一个逻辑意义上的数据
>
> ​		表的每一列称为字段（Column），同一个表的每一行记录都拥有相同的若干字段。
>
> **优点：**
>
> - 都是使用表结构，格式一致，易于维护
> - 使用通用SQL语言操作，使用方便，可用于复杂查询
> - 数据存储在磁盘中，安全
>
> **SQL：**
>
> - 英文：Structured Query Language，简称SQL，结构化查询语言
> - 操作关系型数据库的编程语言
> - 定义操作所有关系型数据库的统一标准
>
> **MySQL：** 开源免费的中小型数据库(管理系统)，是关系型数据库。
>
> ​	Sun公司收购了MySQL，然后Sun公司又被Oracle收购
>
> ****

## 常用指令

> Server version: 8.0.19 MySQL Community Server - GPL

**登录：**

| 操作 |                             指令                             |
| :--: | :----------------------------------------------------------: |
| 登录 | `mysql -u<帐号>  -p<密码> -h<ip(本机省略) -p<端口号(默认3306)>` |
| 断开 |                        `exit`或`quit`                        |
| 清屏 |                     `mysql> system cls;`                     |

​	注意`EXIT`仅仅断开了客户端和服务器的连接，MySQL服务器仍然继续运行。

​	**数据库：**

|        操作        |          指令          |
| :----------------: | :--------------------: |
|   列出所有数据库   |   `SHOW DATABASES;`    |
| 创建一个新的数据库 | `CREATE DATABASE xxx;` |
|   删除一个数据库   |  `DROP DATABASE xxx;`  |
|  切换/使用数据库   |       `USE xxx;`       |

​	**表：**

|         操作         |           指令           |
| :------------------: | :----------------------: |
| 列出当前数据库所有表 |      `SHOW TABLES;`      |
|   查看一个表的结构   |       `DESC xxx;`        |
| 查看创建表的SQL语句  | `SHOW CREATE TABLE xxx;` |
|        创建表        |   `CREATE TABLE xxx;`    |
|        删除表        |    `DROP TABLE xxx;`     |

​	**创建表：**

```sql
CREAT TABLE 'xxx' {
	-- AUTO_INCREMENT定义列为自增的属性，一般用于主键，数值会自动加1。
	'xxx1' bigint(20) UNSIGNED AUTO_INCREMENT, 	
	'xxx2' VARCHAR(100) NOT NULL,
	'XXX3' VARCHAR(40) NOT NULL,
	'XXX3' DATE,	
	-- PRIMARY KEY关键字用于定义列为主键。 您可以使用多列来定义主键，列间以逗号分隔。
	RRIMARY KET('XXX1')  //没有逗号！！！！！
	-- 设置存储引擎，CHARSET 设置编码。
}ENGINE = InnoDB DEFAULT CHARSET=utf8;
	
```

## 数据类型

MySQL数据类型大致可以分成3类：

- 数值
- 日期
- 字符串

![image-20220424174003908](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424174003908.png)

**简单说明：**

| 名称           | 类型       | 说明                                                         |
| :------------- | :--------- | :----------------------------------------------------------- |
| `INT`          | 整型       | 小整数值                                                     |
| `DOUBLE(M,N)`  | 浮点型     | 双精度浮点数，M是总长度，N是小数点后保留位数                 |
| `DECIMAL(M,N)` | 高精度小数 | 由用户指定精度的小数，使用字符串保存                         |
| `CHAR(N)`      | 定长字符串 | 存储指定长度的字符串，例如，CHAR(100)总是存储100个字符的字符串，**性能高，空间换时间** |
| `VARCHAR(N)`   | 变长字符串 | 存储可变长度的字符串，例如，VARCHAR(100)可以存储0~100个字符的字符串，**性能低，时间换空间** |
| `BOOLEAN`      | 布尔       | 存储True或者False                                            |
| `DATE`         | 日期       | 存储日期，例如，2018-06-22                                   |
| `TIME`         | 时间       | 存储时间，例如，12:20:59                                     |

## SQL简介

**英文：Structured Query Language，简称SQL**

SQL是结构化查询语言，一门操作关系型数据库的编程语言

它定义了操作所有关系型数据库的统一标准

对于同一个需求，每一种数据库操作的方式可能存在一些不一样的地方，称之为“方言”

1. SQL语言可以单行或多行书写，**以分号结尾**
2. MySQL数据库的SQL语句不区分大小写，关键字建议使用大写
3. 注释：

```sql
-- 单行注释
# MySQL特有的单行注释
/*
 * 多行注释
 */
```

**SQL分类：**

- **DDL 数据定义语言(Data Definition Language):** 用来定义数据库的对象，如数据库、表、列等 
- **DML 数据操纵语言(Data Manipulation Language):** 用来对数据库中的数据进行增删改查
- **DQL 数据查询语言(Data Query Language):** 用来查询数据库中表的记录（数据）
- **DCL 数据控制语言(Data Control Language):** 重来定义数据库的访问权限和安全等级，以及创建用用户

> 关系数据库的基本操作就是增删改查，即CRUD：Create、Delete、Update、Retrieve。

## DDL

> **DDL 数据定义语言(Data Definition Language):** 用来定义数据库的对象，如数据库、表、列等 

### 操作数据库

#### 查询库

```sql
SHOW DATABASES;

-- 查询成功，初始四个数据库为mysql自带的数据库
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.00 sec)
```

**自带的数据库: **

|       数据库名       |                             说明                             |
| :------------------: | :----------------------------------------------------------: |
| `information_schema` | 记录了mysql有哪些库有哪些表的信息，使用特殊的"视图"来存储，不存在物理的文件 |
|      `mysql  `       |               存储数据库核心信息，如权限、安全               |
| `performance_schema` |                      存储性能相关的信息                      |
|        `sys`         |                      存储系统相关的信息                      |

创建数据库

```sql
CREATE DATABASE 数据库名;

-- 创建成功
Query OK, 1 row affected (0.01 sec)
```

**如果需要判断无同名数据库时再创建：**

```sql
CREATE DATABASE IF NOT EXISTS 数据库名;
-- 已存在数据库，未创建
Query OK, 1 row affected, 1 warning (0.01 sec)

CREATE DATABASE IF NOT EXISTS 数据库名;
-- 未存在数据库，创建
Query OK, 1 row affected (0.01 sec)
```

#### 删除库

```sql
DROP DATABASE 数据库名;
```

**如果需要判断数据库是否存在再删除：**

```sql
DROP DATABASE IF EXISTS 数据库名;
```

#### 切换库

```sql
USE 数据库名;
```

**查询当前使用的数据库：**

```sql
SELECT DATABASE();
```

![image-20220424175628609](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424175628609.png)

### 操作表

#### 查询表

**查询库内所有表：**

```sql
SHOW TABLES;
```

![image-20220424172925118](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424172925118.png)

**查询某个表的结构：**

```sql
DESC 表名;
```

![image-20220424172955127](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424172955127.png)

#### 创建表

```sql
CREATE TABLE 表名 (
	字段名1  数据类型1,
    字段名2  数据类型2,
    ......
    -- 最后一个字段不需要逗号
    字段名n  数据类型n 
);
```

![image-20220424173717172](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424173717172.png)

**创建案例：**

![image-20220424174936662](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424174936662.png)

```sql
CREATE TABLE stu(
	id INT,
    name VARCHAR(10),
    gender CHAR(1),
    birthday DATE,
    score DOUBLE(5,2),
    email VARCHAR(64),
    tel VARCHAR(15),
    status TINYINT
);
```

![image-20220424175324694](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424175324694.png)

#### 删除表

```sql
DROP TABLE 表名;
```

**删除前判断是否存在：**

```sql
DROP TABLE IF EXISTS 表名;
```

#### 修改表

**修改表名：**

```sql
ALTER TABLE 表名 RENAME TO 新的表名;
```

**添加一列：**

```sql
ALTER TABLE 表名 ADD 列名 数据类型;
```

**修改数据类型：**

```sql
ALTER TABLE 表名 MODIFY 列名 新数据类型;
```

**修改列名和数据类型：**

```sql
ALTER TABLE 表名 CHANGE 列名 新列名 新数据类型
```

**删除列：**

```sql
ALTER TABLE 表名 DROP 列名;
```

## DML

> **DML 数据操纵语言(Data Manipulation Language):** 用来对数据库中的数据进行增删改查

### 添加数据

**给指定列添加数据:**

```sql
INSERT INTO 表名(列名1,列名2,...) VALUES(值1, 值2,...);

-- 给所有列增添数据时可以省略列名
INSERT INTO stu values(值1, 值2,...);
```

![image-20220424195644626](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424195644626.png)

**批量添加： 用逗号隔开**

```sql
INSERT INTO 表名(列名1,列名2,...) VALUES(值1, 值2,...),(值1, 值2,...),(值1, 值2,...),...;
```

![image-20220424200317533](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424200317533.png)

**注意：**

- 自增主键可以由数据库自己推算，有默认值的字段在`INSERT`语句中不必出现

- 字段顺序不必和数据库表的字段顺序一致，但值的顺序必须和字段顺序一致。

### 修改数据

**修改表数据：**

```sql
UPDATE 表名 SET 列名=值1,列名=值2,... [WHERE 条件];
```

![image-20220424200844666](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424200844666.png)

**注意： 如果不写WHERE条件，会把所有的记录全部修改！**

### 删除数据

```sql
DELETE FROM 表名 WHERE ...;
```

**注意：**

- 如果`WHERE`条件没有匹配到任何记录，`DELETE`语句不会报错，也不会有任何记录被删除。
- 最后，要特别小心的是，和`UPDATE`类似，不带`WHERE`条件的`DELETE`语句会删除整个表的数据，最好也先用`SELECT`语句来测试`WHERE`条件是否筛选出了期望的记录集，然后再用`DELETE`删除

## DQL

> **DQL 数据查询语言(Data Query Language):** 用来查询数据库中表的记录（数据）

**查询语法：**

```sql
SELECT 字段列表 FROM 列表表名

WHERE
	条件
GROUP BY
	分组字段
HAVING
	分组后条件
ORDER BY
	排序字段
LIMIT
	分页
;	
```

### 基本查询

```sql
SELECT 列1, 列2,...(简称字段列表) FROM 表名;
```

**注意：**

- `*` 替代列名可以查询到所有字段，但项目中尽量不要使用`*`，写全列名可以明确需要查找的数据
- `DISTINCT` 可以去除重复记录，写在`SELECT`和字段列表之间
- `列名 as/空格 别名` 可以给查询出的列名起别称
- 如果不使用FROM字句，则SELECT会计算出其后跟着的表达式的结果，通常可以用来判断当前到数据库的连接是否有效。许多检测工具会执行一条`SELECT 1;`来测试数据库连接。

![image-20220424202227605](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424202227605.png)

### 条件查询

```sql
SELECT 字段列表 FROM 表名 WHERE 条件;
```

**条件：**

|         符号         |                  功能                   |
| :------------------: | :-------------------------------------: |
|         `>`          |                  大于                   |
|         `<`          |                  小于                   |
|         `>=`         |                大于等于                 |
|         `<=`         |                小于等于                 |
|         `=`          |                  等于                   |
|      `!=`或`<>`      |                 不等于                  |
| `BETWEEN ... AND...` |          在某个范围内(都包含)           |
|      `IN(...)`       |                 多选一                  |
|    `LIKE` 占位符     | 模糊查询:  `_`单个字符，`%`多个任意字符 |

|     符号      |   功能   |
| :-----------: | :------: |
|   `IS NULL`   |  是NULL  |
| `IS NOT NULL` | 不是NULL |
|  `AND`或`&&`  |   并且   |
|  `OR`或`||`   |   或者   |
|  `NOT`或`!`   | 非、不是 |

**注意：** 比对字段是否为NULL要使用`IS NULL`和`IS NOT NULL`，不能用`NULL`

**条件表达式：**

- 和 `<条件1> AND <条件2>`
- 或 `<条件1> OR <条件2>`
  - 简化或写法: `字段 in(值1,值2,...)`
- 否 `NOT <条件>` 
  - `NOT id = 2`等价于`id <>2`
- 条件运算按照`NOT`、`AND`、`OR`的优先级进行，要组合三个或者更多的条件并改变优先级，就需要用小括号`()`表示如何进行条件运算。

**模糊查询案例：**

- 查询第一个是'马'的学员信息:

```sql
SELECT * FROM stu WHERE name LIKE '马%';
```

- 查询第二个字是'花'的学员信息:

```sql
SELECT * FROM stu WHERE name LIKE '_花%';
```

- 查询名字中包含'德'的学员信息：

```sql
SELECT * FROM stu WHERE name LIKE '%德%';
```

### 排序查询

```sql
SELECT * FROM students  ORDER BY 字段名1 排序方式1, 字段名1 排序方式2; 
```

查询时结果集通常是按照主键排序，若要其根据其他条件排序，就可以加上`ORDER BY`子句。

- `ORDER BY 列名 ASC` 升序排序（从小到大），`ASC` 为默认值
- `ORDER BY 列名 DESC` 降序排序（从大到小）
- 如果列有相同的数据，要进一步排序，就可以继续添加列名，也就是说如果有多个排序条件，只有当前一个条件值一样时才会根据第二条件排序。


**注：**`ORDER BY`子句要放到`WHERE`子句后面

**案例：**

- 查询学生信息，按照年龄升序排列

```sql
SELECT * FROM stu ORDER BY age ASC;
```

- 查询学生信息，按照数学成绩降序排列

```sql
SELECT * FROM stu ORDER BY age DESC;
```

- 查询学生信息，按照数学成绩降序排列，如果成绩一样，按照英语成绩升序排列

```sql
SELECT * FROM stu ORDER BY math DESC, english ASC;
```

### 聚合函数

**概念：** 将一列数据作为一个整体，进行纵向计算

**聚合函数语法：**	

```sql
SELECT 聚合函数名(列名) FROM 表;
```

**聚合函数：**

| 函数          | 说明                                                         |
| :------------ | :----------------------------------------------------------- |
| `COUNT(字段)` | 计算列的行数(一般选不为`NULL`的字段，通常为主键)，使用`*`可以统计到所有行 |
| `SUM(字段)`   | 计算某一列的合计值，该列必须为数值类型                       |
| `AVG(字段)`   | 计算某一列的平均值，该列必须为数值类型                       |
| `MAX(字段)`   | 计算某一列的最大值                                           |
| `MIN(字段)`   | 计算某一列的最小值                                           |

**注意： **

- `null`值不参与所有聚合函数运算

- `MAX()`和`MIN()`函数并不限于数值类型。如果是字符类型，`MAX()`和`MIN()`会返回排序最后和排序最前的字符。
- 如果聚合查询携带`WHERE`条件但没有匹配到任何行，`COUNT()`会返回0，而`SUM()`、`AVG()`、`MAX()`和`MIN()`会返回`NULL`
- 如果需要分组使用聚合函数，可以使用`GROUP BY`，要显示分组字段，可以在查询中加入分组字段

```sql
SELECT 分组字段,聚合函数名(列名) 别名 FROM 表 GROUP BY 分组字段;
```

**案例：**

![image-20220424211514727](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424211514727.png)

注意第5条英语成绩为`NULL`，以该字段为参数不会参与到聚合函数运算

- 统计班级共有多少个学生

```sql
-- id是不会为NULL的字段
SELECT COUNT(id) FROM stu;
```

![image-20220424211535698](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424211535698.png)

如果参数是`english`，统计的数据是7，因为有一条记录的`english`为`NULL`

- 查询数学成绩最高分和最低分

```sql
-- 最高分
SELECT MAX(math) FROM stu;
-- 最低分
SELECT MIN(math) FROM stu;
```

![image-20220424211559200](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424211559200.png)

- 查询数学成绩的总分

```sql
SELECT SUM(math) FROM stu;
```

![image-20220424211634257](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424211634257.png)

- 查询数学成绩的平均分

```sql
SELECT AVG(math) FROM stu;
```

![image-20220424211721362](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424211721362.png)

- 查询英语成绩的最低分

### 分组查询

分组查询使用`GROUP BY`

```sql
SELECT 字段列表 FROM 表名 [WHERE 分组前的条件限定] GROUP BY 分组字段名 [HAVING 分组后条件过滤];
```

**`WHERE`和`HAVING`的区别：**

- 执行顺序：`WHERE`>聚合函数>`HAVING`
- 执行时机不同：`WHERE`在分组之前限定，不满足的不参与分组，`HAVING`在分组之后限定，是对分组结果进行过滤
- 可判断的条件不一样：`WHERE`不能对聚合函数进行判断，`HAVING`可以

**案例：**

- 查询男同学和女同学各自的数学平均分

```sql
SELECT sex, AVG(math) FROM stu GROUP BY sex;
```

![image-20220424212843547](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424212843547.png)	

**注意：** 分组之后，查询的字段为聚合函数和分组字段，查询其他字段无任何意义，比如这里哪怕查询了name，结果集中也不会显示

- 查询男同学和女同学各自的数学平均分，以及各自人数

```sql
SELECT sex 性别, AVG(math) 平均分, COUNT(*) 人数 FROM stu GROUP BY sex;
```

![image-20220424213340588](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424213340588.png)

- 查询男同学和女同学各自的数学平均分，以及各自人数，要求：分数低于70分的不参与分组

```sql
SELECT sex 性别, AVG(math) 平均分, COUNT(*) 人数 FROM stu WHERE math > 70 GROUP BY sex;
```

![image-20220424213512861](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424213512861.png)

- 查询男同学和女同学各自的数学平均分，以及各自人数，要求：分数低于70分的不参与分组，分组之后人数大于2个的

```sql
SELECT sex 性别, AVG(math) 平均分, COUNT(id) 人数 FROM stu WHERE math > 70 GROUP BY sex HAVING COUNT(id) > 2;
```

![image-20220424213910479](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424213910479.png)



### 分页查询

分页查询使用关键字`LIMIT M OFFSET <N>`实现，在`MySQL`中`OFFSET`可省略为`<M>, <N> `，这是`MySQL`的方言(不同数据库分页关键字一般不一样)

```sql
SELECT 字段列表 FROM 表名 LIMIT 起始索引, 查询条目数;
```

**注意： 上述语句中的起始索引是从0开始**

**起始索引计算公式：**

```sql
起始索引 = (当前页码 - 1) * 每页显示的条数
```

**案例：**

- 从第0条开始查询，查询3条数据

```sql
SELECT * FROM stu LIMIT 0, 3;
```

- 每页显示3条数据，查询第1页数据

```sql
SELECT * FROM stu LIMIT 0, 3;
```

![image-20220424214750481](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424214750481.png)

- 每页显示3条数据，查询第2页数据

```sql
SELECT * FROM stu LIMIT 3, 3;
```

![image-20220424214809642](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424214809642.png)

- 每页显示3条数据，查询第3页数据（当前页不足3条，有多少显示多少）

```sql
select * from stu limit 6, 3;
```

![image-20220424214827977](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220424214827977.png)

### 多表查询

#### 简介

> 多表查询（笛卡尔查询）：从多张表中一次性的查询出想要的数据

**语法：**

```sql
SELECT * FROM 表1, 表2;

-- 例：
SELECT * FROM students, classes;
```

- **两表分别数据：**

![image-20220425174923021](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220425174923021.png)

- **一次性查询：**

![image-20220425175030328](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220425175030328.png)

结果集仍是二维表，为两张表的行与列两两拼在一起返回（有A,B两个集合，会取尽A,B所有的组合情况），所以列数是两表列之积，行为两表行数之积，其结果可能会非常大。

**多表查询主要操作就是消除无效数据**

#### 分类

**笛卡尔积：** 取A,B两个集合的所有组合情况

**多表查询分类：**

- **连接查询：**
  - 内连接：相当于查询A,B交集数据
  - 外连接：
    - 左外连接：相当于查询A表所有数据和交集部分数据
    - 右外连接：相当于查询B表所有数据和交集部分数据
- **子查询**

##### 内连接

> **内连接：相当于查询A,B交集数据**

**语法：**

```sql
-- 隐式内连接
SELECT 字段列表 FROM 表1,表2… WHERE 条件;

-- 显示内连接
SELECT 字段列表 FROM 表1 INNER JOIN 表2 ON 条件;
```

**案例：**

- 隐式内连接：

  ```sql
  -- 给表 起别名
  SELECT
  	t1.name,
  	t1.gender,
  	t2.dname
  FROM
  	emp t1,
  	dept t2
  WHERE
  	t1.dep_id = t2.did;
  ```

- 显示内连接：

  ```sql
  SELECT 
  	emp.name, 
  	emp.gender, 
  	dept.dname 
  FROM 
  	emp 
  	INNER JOIN dept ON emp.dep_id = dept.did;
  ```

![image-20220425180405344](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220425180405344.png)

##### 外连接

> **左外连接：相当于查询A表所有数据和交集部分数据**
>
> **右外连接：相当于查询B表所有数据和交集部分数据**

**语法：**

```sql
-- 左外连接
SELECT 字段列表 FROM 表1 LEFT OUTER JOIN 表2 ON 条件;

-- 右外连接
SELECT 字段列表 FROM 表1 RIGHT OUTER JOIN 表2 ON 条件;
```

**案例：**

- 查询emp表所有数据和对应的部门信息（左外连接）：

```sql
SELECT * FROM emp LEFT OUTER JOIN dept ON emp.dep_id = dept.did;
```

![image-20220425180741076](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220425180741076.png)

结果显示查询到了 **左表（emp）** 中所有的数据及两张表能关联的数据（如图，尽管小白龙没有关联 **右表(dept)** ，但还是查出来了）

- 查询dept表所有数据和对应的员工信息（右外连接）:

```sql
SELECT * FROM emp RIGHT OUTER JOIN dept ON emp.dep_id = dept.did;
```

![image-20220425181045343](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220425181045343.png)

结果显示查询到了右表（dept）中所有的数据及两张表能关联的数据（如图，没和 **右表(dept)** 关联的小白龙没有查出来，没有和 **左表(emp)** 关联的销售部查出来了）

##### 子查询

> 概念：查询中嵌套查询，称嵌套查询为子查询

**例如，查询工资A高于员工B的员工信息：**

- 查询员工B的工资

```sql
SELECT salary FROM emp WHERE name = 'B'
```

- 查询工资高于员工B员工信息

```sql
SELECT * FROM emp WHERE salary > 3600;
```

**两个需求合二为一即子查询：**

```sql
SELECT * FROM emp WHERE salary > (SELECT salary FROM emp WHERE name = 'B');
```

![image-20220425182033357](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220425182033357.png)

## 约束

### 概念

- 约束是作用于表中列上的规则，用于限制加入表的数据
- 约束的存在保证了数据库中数据的正确性、有效性、完整性
- 例如，约束id字段，让它不可重复

### 分类

**SQL中约束的分类：**

| 约束名称 |    关键字     |                             描述                             |
| :------: | :-----------: | :----------------------------------------------------------: |
| 非空约束 |  `NOT NULL`   |                 保证列中所有数据不能为`NULL`                 |
| 唯一约束 |   `UNIQUE`    |                   保证列中所有数据各不相同                   |
| 主键约束 | `PRIMARY KEY` |           主键是一行数据的唯一标识，要求非空且唯一           |
| 检查约束 |    `CHECK`    |          保证列中的值满足某一条件，**MySQL** 不支持          |
| 默认约束 |   `DEFAULT`   | 保存数据时，未指定值则采用默认值(不给值时才会给默认值，如果给值`NULL`，结果还是`NULL`) |
| 外键约束 | `FOREIGN KEY` | 外键用来将两个表的数据之间建立链接，保证数据的一致性和完整性 |

**注意：** MySQL不支持检查约束

### 非空约束

> **概念：** 非空约束用于保证列中所有数据不能有NULL值

**语法：**

* 添加约束

  ```sql
  -- 创建表时添加非空约束
  CREATE TABLE 表名(
      列名 数据类型 NOT NULL,
      …
  ); 
  ```

  ```sql
  -- 建完表后添加非空约束
  ALTER TABLE 表名 MODIFY 字段名 数据类型 NOT NULL;
  ```

* 删除约束

  ```sql
  ALTER TABLE 表名 MODIFY 字段名 数据类型;
  ```

### 唯一约束

> **概念：** 唯一约束用于保证列中所有数据各不相同

**语法：**

* 添加约束

  ```sql
  -- 创建表时添加唯一约束
  CREATE TABLE 表名(
     列名 数据类型 UNIQUE [AUTO_INCREMENT],
     -- AUTO_INCREMENT: 当不指定值时自动增长
     …
  ); 
  
  -- 在建表语句末尾添加唯一约束
  CREATE TABLE 表名(
     列名 数据类型,
     …
     CONSTRAINT 约束名称 UNIQUE(列名)
  ); 
  ```

  ```sql
  -- 建完表后添加唯一约束
  ALTER TABLE 表名 MODIFY 字段名 数据类型 UNIQUE;
  ```

* 删除约束

  ```sql
  ALTER TABLE 表名 DROP INDEX 字段名;
  ```

### 主键约束

> **概念：** 主键是一行数据的唯一标识，要求非空且唯一
>
> **一张表只能有一个主键**

**语法：**

* 添加约束

  ```sql
  -- 创建表时添加主键约束
  CREATE TABLE 表名(
      列名 数据类型 PRIMARY KEY [AUTO_INCREMENT],
      …
  ); 
  -- 建表末尾添加主键约束
  CREATE TABLE 表名(
      列名 数据类型,
      CONSTRAINT 约束名称 PRIMARY KEY(列名)
  ); 
  ```

  ```sql
  -- 建完表后添加主键约束
  ALTER TABLE 表名 ADD PRIMARY KEY(字段名);
  ```

* 删除约束

  ```sql
  ALTER TABLE 表名 DROP PRIMARY KEY;
  ```

### 默认约束

> **概念：** 保存数据时，未指定值则采用默认值

**语法：**

* 添加约束

  ```sql
  -- 创建表时添加默认约束
  CREATE TABLE 表名(
      列名 数据类型 DEFAULT 默认值,
      …
  ); 
  ```

  ```sql
  -- 建完表后添加默认约束
  ALTER TABLE 表名 ALTER 列名 SET DEFAULT 默认值;
  ```

* 删除约束

  ```sql
  ALTER TABLE 表名 ALTER 列名 DROP DEFAULT;
  ```

### 案例

```sql
-- 员工表
CREATE TABLE emp (
    -- 员工id，主键且自增长
    id INT PRIMARY KEY auto_increment, 
    -- 员工姓名，非空并且唯一
    ename VARCHAR(50) NOT NULL UNIQUE, 
    -- 入职日期，非空
    joindate DATE NOT NULL , 
    -- 工资，非空
    salary DOUBLE(7,2) NOT NULL , 
    -- 奖金，如果没有奖金默认为0
    bonus DOUBLE(7,2) DEFAULT 0 
);
```

![image-20220425143542085](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220425143542085.png)

### 外键约束

#### 概述

> 外键用来让两个表的数据之间建立链接，保证数据的一致性和完整性。

比如员工表中有员工所属的部门id，部门表中有各部门及其id，此时员工表中的部门id和部门表中的部门id是有联系的（逻辑上的）。

如果删除了部门表中的某一个部门id，可能会导致员工表中的部门id出现错误，

所以需要通过外键让这两张表产生数据库层面的关系（物理层面的联系），这样只删除部门表中的1号部门时，数据将无法删除。

#### 语法

**添加外键约束：**

```sql
-- 创建表时添加外键约束
CREATE TABLE 表名(
    列名 数据类型,
    …
    CONSTRAINT 外键名称 FOREIGN KEY(外键列名) REFERENCES 主表(主表列名) 
); 
```

```sql
-- 建完表后添加外键约束
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称);
```

**删除外键约束：**

```sql
ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
```

#### 案例

**创建员工表和部门表，并添加上外键约束：**

```sql
-- 删除表
DROP TABLE IF EXISTS emp;
DROP TABLE IF EXISTS dept;

-- 部门表
CREATE TABLE dept(
	id INT PRIMARY KEY auto_increment,
	dep_name VARCHAR(20),
	addr VARCHAR(20)
);
-- 员工表 
CREATE TABLE emp(
	id INT PRIMARY KEY auto_increment,
	name VARCHAR(20),
	age INT,
	dep_id INT,

	-- 添加外键 dep_id,关联 dept 表的id主键
	CONSTRAINT fk_emp_dept FOREIGN KEY(dep_id) REFERENCES dept(id)	
);
```

![image-20220425150556745](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220425150556745.png)

![image-20220425150618211](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220425150618211.png)

**添加数据：**

```sql
-- 添加 2 个部门
insert into dept(dep_name,addr) values
('研发部','广州'),('销售部', '深圳');

-- 添加员工,dep_id 表示员工所在的部门
INSERT INTO emp (name, age, dep_id) VALUES 
('张三', 20, 1),
('李四', 20, 1),
('王五', 20, 1),
('赵六', 20, 2),
('孙七', 22, 2),
('周八', 18, 2);
```

![image-20220425150732866](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220425150732866.png)

**此时删除 `研发部` 这条数据，会发现无法删除：**

```sql
DELETE FROM emp WHERE dep_name = '研发部';
```

![image-20220425151056508](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220425151056508.png)

## 数据库设计

### 简介

**软件的研发步骤：**

<img src="https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20210724130925801.png" alt="image-20210724130925801" style="zoom:80%;" />

**数据库设计概念：**

* 数据库设计就是根据业务系统的具体需求，结合我们所选用的DBMS(数据库管理系统)，为这个业务系统构造出最优的数据存储模型。
* 建立数据库中的表结构以及表与表之间的关联关系的过程。
* 有哪些表？表里有哪些字段？表和表之间有什么关系？

**数据库设计的步骤：**

* **需求分析：**（数据是什么? 数据具有哪些属性? 数据与属性的特点是什么）

* **逻辑分析：**（通过ER图对数据库进行逻辑建模，不需要考虑我们所选用的数据库管理系统）

  ER(Entity/Relation)图：

  <img src="https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20210724131210759.png" alt="image-20210724131210759" style="zoom:80%;" />

* **物理设计：**（根据数据库自身的特点把逻辑设计转换为物理设计）

* **维护设计：**（1.对新的需求进行建表；2.表优化）

**表关系：**

* **一对一**
  * 如：用户 和 用户详情
  * 一对一关系多用于表拆分，将一个实体中经常使用的字段放一张表，不经常使用的字段放另一张表，用于提升查询性能

* **一对多**
  * 如：部门 和 员工

  * 一个部门对应多个员工，一个员工对应一个部门。

* **多对多**
  * 如：商品 和 订单
  * 一个商品对应多个订单，一个订单包含多个商品。

### 一对一关系

> **一对一**
>
> * 如：用户 和 用户详情
> * 一对一关系多用于表拆分，将一个实体中经常使用的字段放一张表，不经常使用的字段放另一张表，用于提升查询性能

**实现方式：** 在任意一方加入外键，关联另一方主键，并且设置外键为`UNIQUE`

```sql
CREATE TABLE tb_user_desc (
	id INT PRIMARY KEY auto_increment,
	city VARCHAR(20),
	edu VARCHAR(10),
	income INT,
	status CHAR(2),
	des VARCHAR(100)
);

create table tb_user (
	id INT PRIMARY KEY auto_increment,
	photo VARCHAR(100),
	nickname VARCHAR(50),
	age INT,
	gender CHAR(1),
	desc_id INT UNIQUE,
	-- 添加外键
	CONSTRAINT fk_user_desc FOREIGN KEY(desc_id) REFERENCES tb_user_desc(id)	
);
```

![image-20220425154555757](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220425154555757.png)

### 一对多关系

> **一对多**
>
> * 如：部门 和 员工
> * 一个部门对应多个员工，一个员工对应一个部门。

**实现方式：** 在多的一方建立外键，指向一的一方的主键

```sql
-- 部门表
CREATE TABLE dept(
    -- 部门表是一，id为组建
	id INT PRIMARY KEY auto_increment,
	dep_name VARCHAR(20),
	addr VARCHAR(20)
);
-- 员工表 
CREATE TABLE emp(
	id INT PRIMARY KEY auto_increment,
	name VARCHAR(20),
	age INT,
	dep_id INT,

	-- 员工表是多，建立外键，dep_id，关联dept表的id主键
	CONSTRAINT fk_emp_dept FOREIGN KEY(dep_id) REFERENCES dept(id)	
);
```

![image-20220425152957367](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220425152957367.png)

### 多对多关系

> **多对多**
>
> * 如：商品 和 订单
> * 一个商品对应多个订单，一个订单包含多个商品。

**实现方式：** 建立第三张中间表，中间表至少包含两个外键，分别关联双方的主键

```sql
-- 订单表
CREATE TABLE tb_order(
    -- 订单表的主键
    id INT PRIMARY KEY auto_increment,
	payment DOUBLE(10,2),
	payment_type TINYINT,
	status TINYINT
);

-- 商品表
CREATE TABLE tb_goods(
    -- 商品表的主键
	id INT PRIMARY KEY auto_increment,
	title VARCHAR(100),
	price DOUBLE(10,2)
);

-- 订单商品中间表
CREATE TABLE tb_order_goods(
	id INT PRIMARY KEY auto_increment,
	-- 订单表id，需要作为外键关联到订单表主键
    order_id INT,
    -- 商品表id，需要作为外键关联到商品表主键
	goods_id INT,
    -- 在订单表中可以存放当前商品购买的数量
	count INT
);

-- 建完表后，添加外键
ALTER TABLE tb_order_goods ADD CONSTRAINT fk_order_id FOREIGN KEY(order_id) REFERENCES tb_order(id);
ALTER tb_order_goods ADD CONSTRAINT fk_goods_id FOREIGN KEY(goods_id) REFERENCES tb_goods(id);
```

![image-20220425153849088](https://chongming-images.oss-cn-hangzhou.aliyuncs.com/images-master/image-20220425153849088.png)

**场景：** 如果用户需要创建一个订单，选中3个商品，只需要在中间表中添加3条记录，每条记录记录下用户id和选中的商品id以及商品数量即可



**子查询根据查询结果不同，作用不同：**

* **单行单列：** 子查询语句作为条件值，使用 `= > < `等进行条件判断

  ```sql
  SELECT 字段列表 FROM 表 WHERE 字段名 = (子查询);
  ```

* **多行单列：** 子查询语句作为条件值，使用`IN`等关键字进行条件判断

  ```sql
  SELECT 字段列表 FROM 表 WHERE 字段名 IN(子查询);
  ```

* **多行多列：** 子查询语句作为虚拟表

  ```sql
  SELECT 字段列表 FROM (子查询) WHERE 条件;
  ```

## 事务

### 简介

> 数据库的事务（Transaction）是一种机制、一个操作序列，包含了一组数据库操作命令
>
> 事务把所有的命令作为一个整体一起向系统提交或撤销操作请求，即这一组数据库命令要么同时成功，要么同时失败
>
> 事务是不可分割的工作逻辑单元

**在执行SQL语句的时候，某些业务要求，一系列操作必须全部执行，而不能仅执行一部分。**

例如，一个转账操作：

```sql
-- 从id=1的账户给id=2的账户转账100元
-- 第一步：将id=1的A账户余额减去100
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
-- 第二步：将id=2的B账户余额加上100
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
```

这两条SQL语句必须全部执行，或者，由于某些原因，如果第一条语句成功，第二条语句失败，就必须全部撤销。

**这种把多条语句作为一个整体进行操作的功能，被称为数据库事务。**

数据库事务可以确保该事务范围内的所有操作都可以 **全部成功** 或者 **全部失败** 。如果事务失败，那么效果就和没有执行这些SQL一样，不会对数据库数据有任何改动。

**数据库事务具有ACID这4个特性：**

- **A：Atomic 原子性** 事务是不可分割的最小操作单元，要么全部执行，要么全部不执行；
- **C：Consistent 一致性** 事务完成后，所有数据的状态都是一致的，即A账户只要减去了100，B账户则必定加上了100；
- **I：Isolation 隔离性** 如果有多个事务并发执行，同时操作一批数据，每个事务作出的修改必须与其他事务隔离，隔离性越强，即看不见别的事务对数据的修改，同时性能越低；
- **D：Duration 持久性** 即事务完成后，对数据库数据的修改被持久化存储。

### 语法

**隐性事务：** 对于单条SQL语句，数据库系统自动将其作为一个事务执行，这种事务被称为隐式事务。

**显性事务：** 要手动把多条SQL语句作为一个事务执行，使用`BEGIN`开启一个事务，使用`COMMIT`提交一个事务，这种事务被称为显式事务

```sql
-- 开启事务，也可以使用BEGIN
START TRANSACTION;

-- 提交事务
COMMIT;
-- 回滚事务
ROLLBACK;
```

例如，把上述的转账操作作为一个显式事务：

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;

-- COMMIT是指提交事务，即试图把事务内的所有SQL所做的修改永久保存。如果COMMIT语句执行失败了，整个事务也会失败。

-- 有些时候，我们希望主动让事务失败，这时，可以用ROLLBACK回滚事务，整个事务会失败:
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
ROLLBACK;
```

### 数据不一致

#### 脏读

**读取未提交数据**

A事务读取B事务尚未提交的数据，此时如果B事务发生错误并执行回滚操作，那么A事务读取到的数据就是脏数据。

就好像原本的数据比较干净、纯粹，此时由于B事务更改了它，这个数据变得不再纯粹。这个时候A事务立即读取了这个脏数据，但事务B良心发现，又用回滚把数据恢复成原来干净、纯粹的样子，而事务A却什么都不知道，最终结果就是事务A读取了此次的脏数据，称为脏读。

这种情况常发生于转账与取款操作中：

| 时间顺序 |                     转账事务                      |                     取款事务                     |
| :------: | :-----------------------------------------------: | :----------------------------------------------: |
|    1     |                                                   |                     开始事务                     |
|    2     |                     开始事务                      |                                                  |
|    3     |                                                   |               查询账户余额为2000元               |
|    4     |                                                   |          取款1000元，余额被更改为1000元          |
|    5     |               查询账户余额为1000元                |                                                  |
|    6     |                                                   | 取款操作发生未知错误，事务回滚，余额变更为2000元 |
|    7     | 转入2000元，余额被更改为3000元（脏读的1000+2000） |                                                  |
|    8     |                     提交事务                      |                                                  |
|   备注   |      按照正确逻辑，此时账户余额应该为4000元       |                                                  |

####  不可重复读

**前后多次读取，数据内容不一致**

事务A在执行读取操作，由整个事务A比较大，前后读取同一条数据需要经历很长的时间。

而在事务A第一次读取数据，比如此时读取了小明的年龄为20岁，事务B执行更改操作，将小明的年龄更改为30岁，此时事务A第二次读取到小明的年龄时，发现其年龄是30岁，和之前的数据不一样了，也就是数据不重复了，系统不可以读取到重复的数据，称为不可重复读。

| 时间顺序 |                      事务A                      |        事务B         |
| :------: | :---------------------------------------------: | :------------------: |
|    1     |                    开始事务                     |                      |
|    2     |          第一次查询，小明的年龄为20岁           |                      |
|    3     |                                                 |       开始事务       |
|    4     |                    其他操作                     |                      |
|    5     |                                                 | 更改小明的年龄为30岁 |
|    6     |                                                 |       提交事务       |
|    7     |          第二次查询，小明的年龄为30岁           |                      |
|   备注   | 按照正确逻辑，事务A前后两次读取到的数据应该一致 |                      |

#### 幻读

事务A在执行读取操作，需要两次统计数据的总量，前一次查询数据总量后，此时事务B执行了新增数据的操作并提交后，这个时候事务A读取的数据总量和之前统计的不一样，就像产生了幻觉一样，平白无故的多了几条数据，成为幻读。

| 时间顺序 |                        事务A                        |     事务B     |
| :------: | :-------------------------------------------------: | :-----------: |
|    1     |                      开始事务                       |               |
|    2     |             第一次查询，数据总量为100条             |               |
|    3     |                                                     |   开始事务    |
|    4     |                      其他操作                       |               |
|    5     |                                                     | 新增100条数据 |
|    6     |                                                     |   提交事务    |
|    7     |             第二次查询，数据总量为200条             |               |
|   备注   | 按照正确逻辑，事务A前后两次读取到的数据总量应该一致 |               |

### 隔离级别

对于两个并发执行的事务，如果涉及到操作同一条记录的时候，可能会发生问题。因为并发操作会带来数据的不一致性，包括**脏读、不可重复读、幻读** 等。数据库系统提供了隔离级别来让我们有针对性地选择事务的隔离级别，避免数据不一致的问题。

​	SQL标准定义了4种隔离级别，分别对应可能出现的数据不一致的情况：

| Isolation Level  | 脏读（Dirty Read） | 不可重复读（Non Repeatable Read） | 幻读（Phantom Read） |
| :--------------: | :----------------: | :-------------------------------: | :------------------: |
| Read Uncommitted |        Yes         |                Yes                |         Yes          |
|  Read Committed  |         -          |                Yes                |         Yes          |
| Repeatable Read  |         -          |                 -                 |         Yes          |
|   Serializable   |         -          |                 -                 |          -           |

#### Read Uncommitted

​	Read Uncommitted是隔离级别最低的一种事务级别。

​	在这种隔离级别下，一个事务会读到另一个事务更新后但未提交的数据，如果另一个事务回滚，那么当前事务读到的数据就是脏数据，这就是脏读（Dirty Read）

#### Read Committed

​	在Read Committed隔离级别下，一个事务可能会遇到不可重复读（Non Repeatable Read）的问题。

​	不可重复读是指，在一个事务内，多次读同一数据，在这个事务还没有结束时，如果另一个事务恰好修改了这个数据，那么，在第一个事务中，两次读取的数据就可能不一致。

#### Repeatable Read

​	在Repeatable Read隔离级别下，一个事务可能会遇到幻读（Phantom Read）的问题。

​	幻读是指，在一个事务中，第一次查询某条记录，发现没有，但是，当试图更新这条不存在的记录时，竟然能成功，并且，再次读取同一条记录，它就神奇地出现了。

#### Serializable

​	Serializable是最严格的隔离级别。在Serializable隔离级别下，所有事务按照次序依次执行，因此，脏读、不可重复读、幻读都不会出现。

​	虽然Serializable隔离级别下的事务具有最高的安全性，但是，由于事务是串行执行，所以效率会大大下降，应用程序的性能会急剧降低。如果没有特别重要的情景，一般都不会使用Serializable隔离级别。

## 其他语句

### 插入或替换

​	如果我们希望插入一条新记录（INSERT），但如果记录已经存在，就先删除原记录，再插入新记录。此时，可以使用`REPLACE`语句，这样就不必先查询，再决定是否先删除再插入：

```sql
REPLACE INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99);
```

​	若`id=1`的记录不存在，`REPLACE`语句将插入新记录，否则，当前`id=1`的记录将被删除，然后再插入新记录。

### 插入或更新

​	如果我们希望插入一条新记录（INSERT），但如果记录已经存在，就更新该记录，此时，可以使用`INSERT INTO ... ON DUPLICATE KEY UPDATE ...`语句：

```sql
INSERT INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99) ON DUPLICATE KEY UPDATE name='小明', gender='F', score=99;
```

​	若`id=1`的记录不存在，`INSERT`语句将插入新记录，否则，当前`id=1`的记录将被更新，更新的字段由`UPDATE`指定。

### 插入或忽略

​	如果我们希望插入一条新记录（INSERT），但如果记录已经存在，就啥事也不干直接忽略，此时，可以使用`INSERT IGNORE INTO ...`语句：

```sql
INSERT IGNORE INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99);
```

​	若`id=1`的记录不存在，`INSERT`语句将插入新记录，否则，不执行任何操作。

### 快照

​	如果想要对一个表进行快照，即复制一份当前表的数据到一个新表，可以结合`CREATE TABLE`和`SELECT`：

```sql
-- 对class_id=1的记录进行快照，并存储为新表students_of_class1:
CREATE TABLE students_of_class1 SELECT * FROM students WHERE class_id=1;
```

​	新创建的表结构和`SELECT`使用的表结构完全一致。

### 写入查询结果集

​	如果查询结果集需要写入到表中，可以结合`INSERT`和`SELECT`，将`SELECT`语句的结果集直接插入到指定表中。

​	例如，创建一个统计成绩的表`statistics`，记录各班的平均成绩：

```sql
CREATE TABLE statistics (
    id BIGINT NOT NULL AUTO_INCREMENT,
    class_id BIGINT NOT NULL,
    average DOUBLE NOT NULL,
    PRIMARY KEY (id)
);
```

​	然后，我们就可以用一条语句写入各班的平均成绩：

```sql
INSERT INTO statistics (class_id, average) SELECT class_id, AVG(score) FROM students GROUP BY class_id;
```

​	确保`INSERT`语句的列和`SELECT`语句的列能一一对应，就可以在`statistics`表中直接保存查询的结果：

```sql
> SELECT * FROM statistics;
+----+----------+--------------+
| id | class_id | average      |
+----+----------+--------------+
|  1 |        1 |         86.5 |
|  2 |        2 | 73.666666666 |
|  3 |        3 | 88.333333333 |
+----+----------+--------------+
3 rows in set (0.00 sec)
```

### 强制使用指定索引

​	在查询的时候，数据库系统会自动分析查询语句，并选择一个最合适的索引。但是很多时候，数据库系统的查询优化器并不一定总是能使用最优索引。如果我们知道如何选择索引，可以使用`FORCE INDEX`强制查询使用指定的索引。例如：

```sql
> SELECT * FROM students FORCE INDEX (idx_class_id) WHERE class_id = 1 ORDER BY id DESC;
```

​	指定索引的前提是索引`idx_class_id`必须存在。

# 练习

1. **用T-SQL语句创建符合如下要求的两个表**

​																													表 departments

| 字段名  | 数据类型     | 说明           |
| ------- | ------------ | -------------- |
| depid   | tinyint      | 部门编号(主键) |
| depname | char(12)     | 部门名称       |
| depnote | varchar(100) | 有关说明       |

​																													表 employees

| 字段名    | 数据类型      | 说明                 |
| --------- | ------------- | -------------------- |
| empid     | char(6)       | 员工编号(主键)       |
| empname   | char(20)      | 员工姓名(非空)       |
| birthdate | smalldatetime | 出生日期             |
| depid     | tinyint       | 所在部门(外键)(非空) |
| salary    | float         | 月薪                 |
| position  | char(8)       | 职务                 |

```mysql
CREATE TABLE `departments` (
	`depid` TINYINT NOT NULL COMMENT '部门编号(主键)',
	`depname` CHAR ( 12 ) NOT NULL COMMENT '部门名称',
	`depnote` VARCHAR ( 100 ) DEFAULT NULL COMMENT '有关说明',
	-- 申明主键约束
	PRIMARY KEY ( `depid` ) 
) ENGINE = INNODB DEFAULT CHARSET = utf8mb3;

CREATE TABLE `employees` (
	`empid` CHAR ( 6 ) NOT NULL COMMENT '员工编号(主键)',
	`empname` CHAR ( 20 ) NOT NULL COMMENT '员工姓名(非空)',
	`birthdate` DATE DEFAULT NULL COMMENT '出生日期',
	`depid` TINYINT DEFAULT NULL COMMENT '所在部门(外键)(非空)',
	`salary` FLOAT DEFAULT NULL COMMENT '月薪',
	`position` CHAR ( 8 ) DEFAULT NULL COMMENT '职务',
	-- 申明主键约束
	PRIMARY KEY ( `empid` ),
	-- 申明外键约束 
	CONSTRAINT `depid_fk` FOREIGN KEY ( `depid` ) REFERENCES `departments` ( `depid` )
) ENGINE = INNODB DEFAULT CHARSET = utf8mb3;

-- 查询结果
DESC departments;
DESC employees;
```

2. **向第1题的departments表中添加如下数据：**

| depid | depname    | depnote |
| ----- | ---------- | ------- |
| 1     | 软件开发部 | null    |
| 2     | 系统集成部 |         |

3. **向第1题的employees表中添加如下数据：**

| empid  | empname | birthdate  | depid | salary  | position |
| ------ | ------- | ---------- | ----- | ------- | -------- |
| A00001 | 王晓丽  | 1970-4-27  | 2     | 2400.00 |          |
| A00003 | 刘晴    | 1972-9-12  | 1     | 2200.00 |          |
| A00004 | 马明    | 1962/3/14  | 1     | 4600.00 | 副经理   |
| A00007 | 赵书生  | 1968/12/15 | 2     | 2700.00 |          |

```mysql
INSERT INTO departments(depid, depname, depnote) VALUES
(1, '软件开发部', NULL),
(2, '系统集成部', '');

INSERT INTO employees(empid,empname,birthdate,depid,salary,position)
VALUES
("A00001","王晓丽","1970-4-27",2,2400, NULL),
("A00002","刘晴","1972-9-12",1,2200, NULL),
("A00003","马明","1962/3/14",1,4600,"副经理"),
("A00007","赵树生","1968/12/15",2,2700, NULL);

-- 查询结果
SELECT * FROM departments;
SELECT * FROM employees;
```

4. **完成以下练习**

(1) 查询所有1970年以后出生的员工的信息。

```mysql
SELECT * FROM employees WHERE DATE_FORMAT(birthdate,'%Y-%m-%d') > '1970-01-01';
```

(2) 查询工资高于2000的员工的信息。

```mysql
SELECT * FROM employees WHERE salary > 2000;
```

(3) 查询系统集成部的所有员工的信息。

```mysql
SELECT * FROM employees WHERE depid = 2;
```

(4) 将所有员工的工资上调10%。

```mysql
UPDATE employees SET salary = salary * 1.1;
-- 查询结果
SELECT * FROM employees;
```

(5) 统计软件开发部的人数。

```mysql
SELECT COUNT(*) FROM employees WHERE depid = 1;
```

(6) 查询所有员工中工资最高和最低的人。

```mysql
-- 查询所有员工中工资最高的人
SELECT * FROM employees WHERE salary = (SELECT MAX(salary) FROM employees);
-- 查询所有员工中工资最低的人	
SELECT * FROM employees WHERE salary = (SELECT MIN(salary) FROM employees);
```

(7) 将工资收入低于2500的员工每人加薪200元。

```mysql
UPDATE employees SET salary = salary + 200 WHERE salary < 2500;
-- 查询结果
SELECT * FROM employees;
```

(8) 对所有“岗位”一栏为空的记录，将其“岗位”改为“职员”。

```mysql
UPDATE employees SET position = '职员' WHERE position IS NULL;
-- 查询结果
SELECT * FROM employees;
```

(9) 删除年龄大于50岁的员工的信息。

```mysql
DELETE FROM employees WHERE DATE_FORMAT(birthdate,'%Y-%m-%d') < '1972-05-19';
-- 查询结果
SELECT * FROM employees;
```

