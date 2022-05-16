# 第一部分：基础——增删查改

## Getting Started

A DATABASE is a collection of data stored in a format that can easily be accessed

1. Relational Database
2. NoSQL MongoDB

把数据存储在**通过某些关系相互关联的数据表中，每张表储存特定的一类数据**

如果每个应用程序都各自写自己的读写的代码，一方面效率低，容易出错，另一方面，每个应用程序访问数据的接口都不相同，数据难以复用。有了数据库之后，应用程序不需要自己管理数据，而是通过数据库软件提供的接口来读写数据。

## 主流商业数据库

1. 商用数据库 Oracle SQL server 
2. 开源数据库 MySQL PostgreSQL
3. 桌面数据库 Access
4. 嵌入式数据库 Sqlite 适合手机应用和桌面程序

## SQL

SQL（Structured Query Language，结构化查询语言）是专门用来处理（包括查询和修改）关系型数据库的标准语言

不同的数据库都支持SQL，但是某个特定数据库的扩展SQL换一个类型就不能执行了

DDL Data Definition Language

DML Data Manipulation Language

DQL Data Query Language

SQL语言不区分大小写，但是针对表明和列名，有的数据库会区分大小写

## Primary Key

对于关系表，任意两条记录不能重复。不是指两条记录不完全相同，而是指能够通过某个字段唯一区分出不同的记录，这个字段成为主键。

主键一旦插入，不能再修改，所以不使用任何业务相关的字段作为主键。

关系数据库还允许通过多个字段唯一标识记录，这种主键被称为联合主键。对于联合主键，允许一列有重复。一般不使用联合主键。

## Foreign Key

外键是通过定义外键约束实现的

```sql
ALTER TABLE students
ADD CONSTRAINT fk_class_id # 外键约束名称
FOREIGN KEY (class_id)  # 指定class_id作为外键
REFERENCES classes (id); # 将外键关联到classes表的id列

ALTER TABLE students
DROP FOREIGN KEY fk_class_id;
```

由于外键约束会降低数据库性能，大部分情况下为了追求速度并不设置外键约束，而是靠程序自身保证逻辑正确。

## Index

索引是关系数据库中对某一列或多个列的值进行预排序的数据结构。通过使用索引，可以让数据库系统不必扫描整个表，而是直接定位到符合条件的记录，加快查询速度。索引的列值越互不相同，那么索引效率越高。

索引可以提高查询效率，但是会拖慢插入、更新和删除记录的速度。

```sql
ALTER TABLE students
ADD INDEX idx_score (score)

ALTER TABLE students
ADD UNIQUE INDEX idx_score (score)
```





## Retrieving Data From a Single Table

### Select Statement

- SELECT FROM WHERE ORDER BY
- AS 别名
- DISTINCT 使用
- LIMIT M OFFSET N 随着N越大，查询效率越低
- SELECT * FROM 表1M, 表2N 笛卡尔乘积  MxN个记录

### Where Statement

- 一行行验证是否符合条件
- 比较运算 `> < = >= <= !=`
- 日期、文本比较
- 执行优先级：数学→比较→逻辑
- ` WHERE order_id = 6 AND quantity * unit_price > 30`

### AND OR NOT 运算符

实现多重条件筛选

NOT AND 优先级高于 OR

### IN 运算符

将某属性与多个值比较

NOT IN

### BETWEEN 运算符

- BETWEEN AND
- 双闭区间
- 可用于日期

### LIKE 运算符

- 模糊查找
- 用引号包裹字符串
- % any number of character
- _ single character

### REGEXP 运算符

- ^ 开头
- $ 以结束
- | 或者
- [a-h]

### IS NULL 运算符

找出空值

IS NOT NULL

### ORDER BY 子句

- 默认按主键排序
- 可以使用公式 arithmetic expression 
- 加入DESC 变为降序
- MYSQL可以使用没有select的列
- MYSQL可以使用别名
- 避免使用 `ORDER BY 1,2`

### Limit 子句

Limit 在最后

6,3 offset, num 7-9个

> select` `from` `where` + `order by` `limit

## Retrieving Data From Multiple Tables

### INNER JOIN 内连接

- `from` 表A `join` 表B `on` AB的关系
- 有同名列时，需要加上表名前缀
- 最好先`SELECT * FROM`选择，等写好`FROM JOIN ON`后，在明确select的列

### JOINING ACROSS DATABASE

对其他库的表名加上库名前缀

可以用别名简化

### SELF JOINS  自连接

一个表自己和自己合并

使用不同的别名

### JOINING MULTIPLE  TABLES  多表连接

`FROM` 一个核心表A，用多个 `JOIN …… ON ……` 分别通过不同的链接关系链接不同的表

### COMPOUND JOIN CONDITIONS 符合连接条件

针对复合主键

`FROM 表1 JOIN 表2 ON 条件1 AND 条件2` 

### IMPLICIT JOIN SYNTAX 隐式连接语法

用FROM WHERE取代FROM JOIN ON

尽量避免使用

### OUTER JOINS 外连接

`LEFT/RIGHT (OUTER) JOIN` 结果里除了交集，还包含只出现在左/右表中的记录

FULL OUTER JOIN，它会把两张表的所有记录全部选择出来，并且，自动把对方不存在的列填充为NULL

### OUTER JOIN BETWEEN MULTIPLE TABLES 多表外连接

统一只用 [INNER] JOIN 和 LEFT [OUTER] JOIN

### SELF  OUTER JOINS 自我外部连接

用LEFT JOIN让得到的 员工-上级 合并表也包括老板本人

### USING 子句

当作为合并条件（join condition）的列在两个表中有相同的列名时，可用 `USING (……, ……)` 取代 `ON …… AND ……` 予以简化

### NATURE JOINS 自然连接

让MYSQL自动检索同名列作为合并条件

避免使用

### CROSS JOINS 交叉连接

得到名字和产品的所有组合

可以用于尺寸和颜色的全部组合

### UNIONS 组合

 joining rows

合并的查询结果必须列数相等

列名由排在前面的SELECT决定

## Inserting, Updating, and deleting data 插入 更新 和 删除数据

INSERT INTO ()
VALUES (),()

 last_insert_id() 把父表记录插入子表

如果我们希望插入一条新记录（INSERT），但如果记录已经存在，就更新该记录，此时，可以使用`INSERT INTO ... ON DUPLICATE KEY UPDATE ...`

如果我们希望插入一条新记录（INSERT），但如果记录已经存在，就啥事也不干直接忽略，此时，可以使用`INSERT IGNORE INTO ...`

CREATE TABLE 新表名 AS 子查询

INSERT INTO 表名 子查询

UPDATE TABLE
SET COLUMN
WHERE

DELETE FROM 表 
WHERE 行筛选条件

# 第二部分：基础进阶——汇总、复杂查询、内置函数

## 汇总数据

### 聚合函数 Aggregate Functions

输入一系列值并聚合为一个结果的函数

`MIN MAX SUM COUNT`

### GROUP BY 子句

按一列或者多列分组

顺序 `where group by order by`

### HAVING 子句

| WHERE                                                        | HAVING                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 对  FROM JOIN 中原表的列进行 **事前筛选**<br />所以可以对没有选择的列进行筛选<br />必须使用原名不能使用别名 | 对分组并聚合查询后的列进行 **事后筛选**<br />不能对未选择的字段进行筛选<br />必须使用别名<br />筛选聚合函数时，可以不出现在SELECT中 |

### ROLLUP 运算符

`GROUP BY ... WITH ROLL UP` 

自动汇总型分组

MYSQL独有

使用 ROLLUP 之后 不能使用别名

### SQL 查询语句执行顺序

1. FROM JOIN 选择和连接本次查询所需的表

2. ON/USING WHERE 按条件筛选行

3. GROUP BY 分组

4. HAVING （事后/分组后）筛选行

5. SELECT 筛选列

   注意1：若进行了分组，这一步常常要聚合

   注意2：SELECT 和 HAVING 在 MySQL 里的执行顺序我还有点疑问，见后面的叙述

6. DISTINCT 去重

7. UNION 纵向合并

8. ORDER BY 排序

9. LIMIT 限制

## 编写复杂查询

### Subqueries

不确定执行顺序的时候加上括号确保万无一失

子查询可以用在 WHERE SELECT FROM 中

### The IN Operator

IN NOT IN

### Subqueries vs Joins

子查询和链接一般可互换

使用哪种取决于性能和可读性

### The ALL Keyword

`> (MAX (……))` 和 `> ALL(……)` 等效可互换

### The ANY Keyword

`> ANY/SOME (……)` 与 `> (MIN (……))` 等效

`= ANY/SOME (……)` 与 `IN (……)` 等效

### Correlated Subqueries

非关联子查询会直接得出查询结果再返回给主查询

关联查询是在主查询每一条记录层面上依次进行的

所以执行速度会慢一些

```sql
SELECT *
FROM employees e  -- 关键 1
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE office_id = e.office_id  -- 关键 2
    -- 【子查询表字段不用加前缀，主查询表的字段要加前缀，以此区分】
)
```

### The EXISTS Operator 

`IN + 子查询 等效于 EXISTS + 相关子查询`

`EXISTS` 逐条验证，占用内存少 


### Subqueries in the SELECT  Clause

`SELECT`的元素除了可以是原始的列，具体的数值，也同样可以是其它各种花里胡哨的子查询的结果

### Subqueries in the FROM  Clause

子查询的结果可以作为虚拟表作为FROM的来源

复杂的子查询用视图会更好

## MySQL的基本函数 Essential MySQL Functions

### Numeric Functions 

ROUND、TRUNCATE、CEILING 向上取整、FLOOR 向下取整、ABS、RAND

### String Functions

1. LENGTH, UPPER, LOWER
2. TRIM, LTRIM, RTRIM
3. LEFT, RIGHT, SUBSTRING
4. LOCATE, REPLACE, CONCAT
4. substring_index(profile,'/',-1)

### Date Functions in MySQL

1. NOW, CURDATE, CURTIME
2. YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, DAYNAME, MONTHNAME
3. EXTRACT(单位 FROM 日期时间对象)， 如 EXTRACT(YEAR FROM NOW())

### Formatting Dates and Times 

`DATE_FORMAT(date, format)` 
`TIME_FORMAT(time, format)`

### Calculating Dates and Times

1. DATE_ADD, DATE_SUB
2. DATEDIFF
3. TIME_TO_SEC 从零点到该时间经历的秒数

```sql
# 不用函数 用加减更简洁
NOW() - INTERVAL 1 DAY
NOW() - INTERVAL 1 YEAR 
```

### The IFNULL and COALESCE Functions

替换空值

COALESCE 返回一系列值中的首个非空值

### The IF Function 

IF(条件表达式, 返回值1, 返回值2)

只能有一个条件表达式

### The CASE Operator 

```sql
CASE 
    WHEN …… THEN ……
    WHEN …… THEN ……
    WHEN …… THEN ……
    ……
    [ELSE ……] （ELSE子句是可选的）
END
```

多个条件表达式

# 第三部分：提高效率——视图、存储过程、函数

## 视图Views

### Creating Views 创建视图

存储起来的模块化的查询结果

没有真正储存数据

```sql
CREATE VIEW VIEWNAME AS
	SELECT ...
```

### Altering or Dropping Views 更新或删除视图

最好将views保存为sql文件并放入git

```sql
DROP VIEW IF EXISTS VIEWNAME;

CREATE OR REPLACE VIEWNAME AS
	SELECT ...
```

### Updatable Views 可更新视图

没有以下元素的视图都是可更新视图（可以增查删改）

1. DISTINCT
2. GROUP BY / HAVING /  AGGREGATE FUNCTION
3. UNION

INSERT 需要视图包含了原表的所有必须字段

### THE WITH CHECK OPTION Clause

防止执行让视图中某些记录消失的修改语句

### Other Benefits of Views 视图的其他优点

1. 简化查询 simplify queries
2. Reduce the impact of changes：如果数据库设计改变了（如一个字段从一个表转移到了另一个表），只需修改视图的查询语句使其能保持原有查询结果即可。
3. Restrict access to the data

## 存储过程 Stored Procedure

### 存储过程三大作用

1. Store and organize SQL

2. Faster execution

3. Data security

### 创建 使用 删除 存储过程

```sql
DELIMITER $$
CREATE PROCEDURE get_clients()
	BEGIN
		
	END$$
DELIMITER :

CALL get_clients();

DROP PROCEDURE IF EXISTS get_clients;
```

### 参数  Parameters

```sql
CREATE PROCEDURE get_clients_by_state
(
    state CHAR(2)  -- 参数的数据类型
)
BEGIN
    SELECT * FROM clients c
    WHERE c.state = state; -- 取别名表示区分
END
```

- Parameter 形参 创建过程中用的占位符
- Argument 实参 调用时实际传入的值

### 默认参数

```sql
利用 IF(condition,A,B) 或 IF THEN ELSE 或 IFNULL(A,B) 实现默认参数
```

### 参数验证

```sql
IF 错误参数条件式 THEN
	SIGNAL SQLSTATE '错误类型'
		SET MESSAGE_TEXT = '补充信息' -- 可选项
```

### 变量  Variable

```sql
-- 会话变量，一般用于带输出参数的存储过程中
set @invoice_count=0; 

-- 本地变量
CREATE PROCEDURE get_risk_factor()
BEGIN
    -- 声明三个本地变量，可设默认值
    DECLARE risk_factor DECIMAL(9, 2) DEFAULT 0;
    DECLARE invoices_total DECIMAL(9, 2);
    DECLARE invoices_count INT;

    -- 用SELECT得到需要的值并用INTO传入invoices_total和invoices_count
    SELECT SUM(invoice_total), COUNT(*)
    INTO invoices_total, invoices_count
    FROM invoices;

    -- 用SET语句给risk_factor计算赋值
    SET risk_factor = invoices_total / invoices_count * 5;

    -- 展示最终结果risk_factor
    SELECT risk_factor;        
END
```

### 函数 Functions

```sql
`CREATE DEFINER=`root`@`localhost` FUNCTION `get_risk_factor_for_client`
(
    client_id INT
) 
RETURNS INTEGER
-- DETERMINISTIC 决定性的
READS SQL DATA
-- MODIFIES SQL DATA 是否有增删改
BEGIN
    DECLARE risk_factor DECIMAL(9, 2) DEFAULT 0;
    DECLARE invoices_total DECIMAL(9, 2);
    DECLARE invoices_count INT;

    SELECT SUM(invoice_total), COUNT(*)
    INTO invoices_total, invoices_count
    FROM invoices i
    WHERE i.client_id = client_id;
    -- 注意不再是整体risk_factor而是特定顾客的risk_factor

    SET risk_factor = invoices_total / invoices_count * 5;
    RETURN IFNULL(risk_factor, 0);  -- 返回值而不是查询值
END
```

# 第四部分：高阶主题——触发器、事件、事务、并发

## 触发器和事件 Triggers and Events

### 触发器 Triggers

> A block of SQL code that automatically gets executed before or after an insert, update or delete statement

```sql
DELIMITER $$

CREATE TRIGGER payments_after_insert # 命名习惯 触发表_before or after_type
    AFTER INSERT ON payments # 触发条件语句
    FOR EACH ROW # 触发频率语句
BEGIN
    UPDATE invoices # 不能修改触发表
    SET payment_total = payment_total + NEW.amount # NEW or OLD
    WHERE invoice_id = NEW.invoice_id;
END$$

DELIMITER ;
```

### 查看删除触发器

```sql
SHOW TRIGGERS LIKE 'payments%'

DROP TRIGGER [IF EXISTS] payments_after_insert
```

### 事件

```sql
SET GLOBAL event_scheduler = ON/OFF

DELIMITER $$

CREATE EVENT yearly_delete_stale_audit_row

-- 设定事件的执行计划：
ON SCHEDULE  
    EVERY 1 YEAR [STARTS '2019-01-01'] [ENDS '2029-01-01']    
    # 只执行一次用 AT

-- 主体部分：（注意 DO 关键字）
DO BEGIN
    DELETE FROM payments_audit
    WHERE action_date < NOW() - INTERVAL 1 YEAR;
END$$

DELIMITER ;
```

### 查看删除更改事件

```sql
SHOW EVENTS [LIKE 'yearly%'];  

DROP EVENT IF EXISTS yearly_delete_stale_audit_row;

ALTER EVENT yearly_delete_stale_audit_row [DISABLE/ENABLE]
```



## 事务和并发 transactions and concurrency

### 事务 transactions

> 事务（trasaction）是**完成一个完整事件的一系列SQL语句**。如果一部分执行成功一部分执行失败那成功的那一部分就会复原（revert）以保持数据的一致性。

**ACID 特性**

1. Atomicity 不可拆分性 将所有SQL作为原子工作单元执行，要么全部执行，要么全部不执行
2. Consistency 一致性，事务完成之后，所有数据的状态是一致的
3. Isolation 隔离性：多个事务要修改相同数据，每次只能被一个事务修改
4. Durability 持久性：事务执行完毕，修改是永久的

### 创建事务 Creating Transactions

用 START TRANSACTION 创建事务，用 COMMIT 来关闭事务

```sql
START TRANSACTION;

INSERT INTO orders (customer_id, order_date, status)
VALUES (1, '2019-01-01', 1);
-- 只需明确声明并插入这三个非自增必须（不可为空）字段

INSERT INTO order_items 
-- 所有字段都是必须的，就不必申明了
VALUES (last_insert_id(), 1, 2, 3);

COMMIT;
```

我们执行的每一个语句，就算没有 START TRANSACTION + COMMIT，也都会被 MySQL 包装（wrap）成事务并在没有错误的前提下autocommit

### 并发和锁定 Concurrency and Locking

**四个并发问题**

1. Lost Update 两个事务更新同一行，最后提交的事务将覆盖先前所做的更改
2. Dirty Reads 读取了未提交的数据
3. Non-repeating Reads 在事务中两次读取相同的数据，得到不同的结果
4. Phantom Reads 另一个事务修改数据，却没有意识到，在查询中缺失了一行或多行

**四个事务隔离等级**

1. Read Uncommitted 事务间完全没有隔离，可以读取彼此未提交的修改，无法解决任何并发问题
2. Read Committed 有一定隔离，只能读取已提交的数据，能防止Dirty Read
3. Repeatable Read 可以确信不同的读取会返回相同的结果，即使数据在期间被更改和提交，MySQL的默认等级
4. Serializable 可以防止所有并发问题，但是会占用存储和计算资源

**改变隔离等级**

```sql
SHOW VARIABLE LIKE 'transaction_isolation'

SET [SESSION]/[GLOBAL] TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

**死锁 Deadlock**

死锁不能完全避免，但是可以减少发生

# 第五部分：脱颖而出——数据类型、设计数据库、索引、保护

## 数据类型 Data Types

### 存储单位

- 一个晶体管开和关，代表1和0两个值，是最小存储单位 1位bit 
- 一字节Byte 有8位 可以表示 2^8^ 个值，即256个值
- 字节 B 千字节 KB 兆字节 MB 千兆字节 GB 太字节 TB 相邻之间换算比率是2^10，即1024，约1000

### 支持的数据类型

1. String Types 字符串类型
2. Numeric Types 数字类型
3. Date and Time Types 日期和时间类型
4. Blog Types 存放二进制的数据类型
5. Spatial Types 存放地理数据的类型

### 字符串类型 String Types

- 英文字符占用1字节
- 欧洲和中东语言字符占2个字节
- 中日等亚洲语言占3个字节

CHAR VARCHAR

VARCHAR(50) 可以用来记录用户名和密码这种短文本

 VARCHAR(255) 可以用来记录地址这种长文本

MEDIUMTEXT 最大存储16MB











