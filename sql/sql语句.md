# 常用语句

+ 查看表结构：desc tab_name
+ 所有字段信息：SHOW FULL COLUMNS FROM tb_user;
+ 统计：  select count(c='1' or null) from table_name(求c=的总数)
+ 求值：  select avg() from(求平均，也可max，min，sum)
+ 算年龄： SELECT TIMESTAMPDIFF(YEAR,'1997-09-27',   '2093-12-31') AS age ，year可以替换成day
+ 算一月前的时间：CreateTime < DATE_SUB(NOW(), INTERVAL 1 MONTH)【内就是>,取出的是HHmmss】MONTH(NOW())返回现在的月数  
     换成时间戳：CreateTime>UNIX_TIMESTAMP(DATE_SUB(CURDATE(), INTERVAL 1 DAY))

## 关键字用法

+ having只能对group by之后操作：
+ <>''和!=''都是不为空，ISNULL(id)和=''都是为空
+ DISTINCT查询不重复的
+ Unix时间戳，是1970年1月1日午夜开始所经过的秒数，UNIX_TIMESTAMP(NOW())（现在）

## 建表,删除和改表语句

+ 建表

 1. create table tab_name (column type,column type);
 2. create table tab_new SELECT * FROM tab_name;
 3. create table tab_name like table_old(加字段alter table table name add column type); 

+ 删除

 1. drop index idxname(删除索引，不可改只能重建,用来删除结构);
 2. alter table tab_name drop column(删除字段结构)
 3. delete from tab_name where condition（用来删除数据）
  
+ 更新修改
  1. ALTER TABLE tab_name MODIFY column VARCHAR(20) 
    (新数据类型 新类型长度  新默认值  新注释)
  2. alter table tab_name change column1  column2 ...；
    (decimal(10,1) DEFAULT NULL COMMENT '注释' 能修改字段名、字段类型、类型长度、默认值、注释)
  3. RENAME table table1 TO table2(重命名)
+ update table_name set column_name='' where condition

## 插入

+ 插入：
   1. INSERT INTO tab_new VALUES ('庚戌','47',NULL,'2','1'),('壬子','49',NULL,'3','4')（两列插入 必须加引号）
   2. insert into table_new column_name select column_name from table_old (复制旧表数据到新表)
