#MYSQL NOTES

标签（空格分隔）： 未分类

---

#一.库操作
##查看库:show datebase;
##创建库:creat datebase <name>
##删除库:drop datebase <name>
##使用库 use <name>
#二.表操作
##1.创建表:CREATE TABLE <name>
primary key（主键）
auto_increment（自增长类型）
语句逗号以隔开，表以分号结束
###*创建关联子表:
constraint <约束名> foreign key (<子表属性名> ) references<主表名>（主表属性名）
##2.查看表结构:
查看基本结构:desc t_book;
查看详细结构:show create table t_book
##3.修改表
alter table < oldname> rename < newname>
###修改字段:alter table <name> change
 < old name> < new name> <数据类型>
###增加字段:alter table <name> add 
<属性名> （约束条件）（first/after 属性名）
删除字段:alter table < name> drop <属性名>
##4.删除表
*drop table < name>
##5.单表查询
###1.查询所有字段
（1）SELECT <属性名（可无顺序）>FROM<表名>
（2）SELECT *FROM <表名>
###2.查询指定字段
SELECT <属性名>FROM<表名>
###3.while查询
SELECT *<表名> while <属性名> （运算符）具体值/范围
###4.带INT IN查询
SELECT *<表名> while <属性名> INT IN（，）< -（范围）
###5.带BETWEEN AND查询
SELECT *<表名> while <属性名> BETWEEN （）AND（）
###6.LIKE模糊查询
(1)SELECT *<表名> while <属性名> LIKE `具体值`
(2)SELECT *<表名> while <属性名>
LIKE `具体值%`(以此字段开头包含此字段的所有值)
(3)SELECT *<表名> while <属性名>
LIKE `具体值_`(只查询三位以内)
(4)SELECT *<表名> while <属性名>
LIKE `%具体值%`(可不以此字段开头，包含此字段所有值)
###7.空值查询
SELECT *<表名> while <属性名> IS/IS NOT NULL
###8.带AND/OR条件查询
SELECT *<表名> while <属性名> (`具体值`)AND <属性名>(具体值)
###9.去重复查询
SELECT  DISTINCT <属性名>FROM<表名>
###10.对查询结果排序
SELECT *<表名> ORDER BY <属性名> ASC(升序)/DESC(降序)
###11.GROUP BY分组查询
###（1）结合GROUP_CONCAT函数:
SELECT <属性名1>，GROUP_CONCAT（属性名2）FROM<表名> GROUP BY <属性名1>
###（2）结合聚合函数:（查询结果数量）
SELECT <属性名1>，COUNT（属性名2）FROM<表名> GROUP BY <属性名1>

###（3）结合HAVING范围查询:
SELECT <属性名1>，COUNT（属性名2）FROM<表名> GROUP BY <属性名1> HAVING COUNT (属性名1)（范围）
###（4）结合WITHROLLUP:求和
####①总和:SELECT <属性名1>，COUNT（属性名2）FROM<表名> GROUP BY <属性名1>WITHROLLUP
####②所有文本:SELECT <属性名1>，GROUP_CONCAT（属性名2）FROM<表名> GROUP BY <属性名1>WITHROLLUP
###12.LIMIT分页查询
SELECT *FROM<表名>LIMIT 页数，数据总数
###13.输出数据总和
###一.使用聚合函数查询
##1.count()函数：统计记录条数
SELECT COUNT(*) AS < NEW NAME>FROM <表名>;
(1)SLECT <属性名>COUNT(*) FROM <表名> GROUT BY<属性名>
##2.sum()函数
SELECT <属性名1>，SUM(属性名2) FROM <表名> GROUT BY<属性名1>
##3.avg()函数：
(1)SELECT <属性名1>，AVG(属性名2) FROM <表名> GROUT BY<属性名1>
##4.MAX()/MIN()函数
(1)SELECT <属性名1>，MAX(属性名2) FROM <表名> GROUT BY<属性名1>
###二.连接查询
###1.内连接查询：查询两个或两个以上的表
e.g
（1）SELECT * FROM t_book,t_bookType WHERE 
t_book.bookTypeId=t_bookType.id;
(2)SELECT bookname,author,bookTypeName FROM t_book,t_bookType WHERE t_book.bookTypeId=t_bookType.id
（3）使用别名
SELECT tb.bookname,tb.author,tby.bookType FROM t_book tb,t_bookType tby WHERE tb.bookTypeId=tby.id;
###2.外连接查询：查出一张表所有信息
###左\右连接：
左连接：查出表1所有记录，表2匹配记录
SELECT *FROM t_book LEFT\RIGHT JOIN t_bookType ON t_book.bookTypeId=t_bookType.id;
###3.多条件查询
结尾加AND加判断条件
##6.子查询
##1.带In关键字
e.g:SELECT * FROM t_book WHERE bookTypeId IN (SELECT id FROM t_bookType);
##2.带比较运算符
e.g:SELECT * FROM t_book WHERE price>=(SELECT price FROM t_pricelevel WHERE pricelevel=1);
##3.带Exists关键字
e.g:SELECT * FROM t_book WHERE Exists(SELECT * FROM t_bookType);
##4.带Any关键字
e.g:SELECT * FROM t_book WHERE price>= ANY (SELECT price FROM t_pricelevel WHERE pricelevel=1);
##5.带All关键字
e.g:SELECT * FROM t_book WHERE price>= ALL (SELECT price FROM t_pricelevel WHERE pricelevel=1);
##7.合并查询结果
##1.UNION:合并两张表，去除重复部分
e.g:SELECT id FROM t_book UNION SELECT id FROM t_bookType;
##2.UNION ALL:合并两张表，不去除重复部分
##8.为表和字段取别名
##1.为表取别名
##2.为字段取别名
e.g:SELECT t.bookName AS bk FROM t_book t WHERE t.id=1;
#三.数据操作
##1.插入数据
###（1）：给表所有字段插入数据
e.g:INSERT INTO t_book VALUES (NULL,'bookName'，price，'anthor'，'bookTypeId')
###（2）：给表指定字段插入数据
e.g:INSERT INTO t_book(bookName,anthot) VALUES
（'我爱我家'，'张三'）
###（3）：同时插入多条数据
INSERT INTO t_book VALUES (NULL,'bookName1'，price，'anthor'，'bookTypeId'),(NULL,'bookName2'，price，'anthor'，'bookTypeId'）；
##2.更新数据
e.g:
(1)UPDATE  t_book SET bookName='java编程思想'，price='10' WHERE id=1;
(2)UPDATE t_book SET bookName='我' WHERE bookName LIKE '%我爱我家%'；
##3.删除数据
e.g:
(1)删除一条:DELETE FROM t_book WHERE id=5;
(2)删除多条:DELETE FROM t_book WHERE bookName='我'；
##4.数据备份与还原
###(1)备份
###①.命令行
e.g:mysqldump -c root -p db_book >c:\db_book.sql
###②图形界面
###(2)还原
###①命令行
e.g:mysql -u root -p db_book < backup.sql
###②图形界面

#四.索引
##1.优缺点：
###优点：提高查询数据速度
###缺点：创建和维护索引时间增加
##2.索引分类
###（1）普通索引：可创建在任何数据类型中
###（2）唯一性索引：unique参数，限制索引唯一，取别名
###（3）全文索引：fulltext参数，查询文本等，mysql不支持
###（4）单列索引：在表中给单个字段创建索引，可以是普通或唯一性或全文索引
###（5）多列索引：在表的多个字段创建索引
###（6）空间索引：spatial参数，建立在空间数据类型上，mysql不支持
##3.创建索引
###(1)创建表时创建索引
###①创建普通索引,单列索引
e.g:INDEX (password)
###②创建唯一性索引
e.g:UNIQUE INDEX index_userName(userName)
###③创建多列索引
e.g:INDEX index_userName_passWord(userName,passWord)
###(2)在已存在表上建立索引
e.g:CREATE INDEX index_userName ON t_book(userName)
###(3)用alter table语句创建索引
ALTER TABLE t_user ADD INDEX index_userName(userName)
##4.删除索引
DROP INDEX index_userName ON t_book;
#五.视图
##1.概念：虚拟的表，由其他表导出的数据，数据库存放视图定义
##2.作用
###（1）.操作简便化
###（2）.增加数据安全性
###（3）.提高表的逻辑独立性
##3.创建视图
###（1)单表上创建视图
###①获取表中所有数据
e.g:CREATE VIEW v1 AS SELECT * FROM t_book
###②获取表中部分数据,为数据取别名
e.g:CREATE VIEW v2(b,p) AS SELECT bookName,price FROM t_book;
###(2)多表上创建视图
e.g:CREATE VIEW v2 AS SELECT t.bookName,tby.price FROM t_book tb,t_bookType tby WHERE tb.t_bookTypeId=tby.id;
##4.查看视图
###(1)desc语句：查看基本信息
e.g:desc v1;
###(2)show table status语句：查看基本信息
e.g:①SHOW TABLE STATUS LIKE `v1`;
    ②SHOW TABLE STATUS LIKE `t_book`;
###(3)show create view语句：查看详细信息
e.g:SHOW CREATE VIEW v1 ;
###(4)在view表中查看视图详细信息
##5.修改视图
###(1)CREATE OR REPLACE语句
e.g:CREATE OR REPLACE VIEW v1(bookName,userName) AS SELECT bookName,userName FROM t_book
###(2)ALTER 语句
ALTER VIEW v1 AS SLECT * FROM t_book;
##6.更新视图
插入，更新，删除（同表操作）
##7.删除视图
DROP VIEW IF EXISTS v1;
#六.触发器
##1.概念：由某个事件触发某个操作
##2.创建与使用触发器
###(1):创建只有一个执行语句的触发器
e.g:CREATE TRIGGER trig_book AFTER INSERT
   ON t_book FOR EACH ROW
   UPDATE t_bookType SET bookName=bookName+1 WHERE new.t_bookTypeId=t_bookType.id;
###(2):创建有多个执行语句的触发器
e.g:DELIMITER |
CREATE TRIGGER trig_book AFTER DELETE
   ON t_book FOR EACH ROW 
   BEGIN
   UPDATE t_bookType SET bookName=bookName-1;
   INSERT INTO t_log VALUES (NULL,NOW(),`这里删除了一条语句`)；
   DELETE FROM t_test WHERE old.bookTypeId=t_bookType.id;
   END
   |
DELIMITER;   
##3.查看触发器
###(1)SHOW TRIGGERS;
###(2)trigger表中查看
##4.删除触发器
DROP TRIGGER trig_book ;(空格）
#七.MYSQL常用函数
##1.日期时间函数
###CURDATE(),CURTIME(),CURMONTH()
e.g:SELECT CURDATE(),CURTIME,CURMONTH(birthday) AS m FROM t_t;
##2.字符串函数
###CHAR_LENGTH(),UPPER(),LOWER()
e.g:SELECT userName,CHAR_LENGTH(userName),UPPER(userName),LOWER(userName) FROM t_t;
##3.数学函数
###ABS(),SQRT(),MOD()
e.g:SELECT num,ABS(num) FROM t_t;
    SELECT SQRT(4),NOD(9,4) FROM t_t;
##4.加密函数
###(1)password()
e.g:INSERT INTO t_t VALUES(PASSWORD(`123`);
###(2)MD5()
e.g:INSERT INTO t_t VALUES(MD5(`123`);
###(3)ENCODE(str,pswd_str):结果是二进制数
e.g:INSERT INTO t_t VALUES(ENCODE(`ABCD`,`AB`));
###(4)DECODE(crypt_str,pswd_str)
e.g:INSERT INTO t_t VALUES(DECODE(`PP`,`AB`));
#八.存储过程和函数
##1.概念：两者是SQL的集合，在MYSQL执行
##2.创建存储过程
###(1).创建存储过程
e.g:DELIMITER &&
CREATE PROCEDRUE pro_book(IN pd INT ,OUT count_name INT)
READS SQL DATA;
BEGIN
SELECT COUNT(*) FROM t_book WHERE booKTypeId=pd
END
&&
DELIMITER;
###(2).创建存储函数
e.g:DELIMITER &&
CREATE FUNCTION func_book(bookId INT)
    RETURN VARCHAR(20)
BEGIN
    RETURN(SELECT bookName FORM t_book.id=bookId);
END
&&
DELIMITER;
##3.调用存储过程和函数
###(1)调用存储过程
调用存储过程
e.g：CALL pro_book(1,@total);
###(2)调用储存函数
e.g:SELECT func_book();
##4.查看存储过程和函数
###(1):show status
e.g:SHOW PROCEDURE STATUS lIKE `pro_book` ;
###(2):show create 
e.g:SHOW CREATE PROCEDURE pro_book;
###(3）从information_schema.Routines表中查看
##5.修改存储过程和函数
e.g:ALTER PROCEDURE pro_book COMMENT `测试`（少用)
##5.删除存储过程和函数
e.g:DROP PROCEDURE pro_book;




   








