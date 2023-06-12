## 数据类型：

char（n）：定长字符数组

varchar(n):变长字符数组，最大到n

int

smallint（short）

numeric（p,d):有效数字为p个，

float（n）：小数点后n位的float

## 语句

**create table**: create table instructor

(

​		ID       char(5),
​	    name     varchar(20),
​	    dept_name varchar(20),
​	    salary      numeric(8,2))

​		primary key(ID) //指定主键

​		foreign key (dept_name) references department; //指定外键，department是表

​		//括号内的为属性可以有多个，和上一章的属性一个意思

)

**insert**： insert into 表名 values （每个atrribute的值）

**drop**：drop table r

**Delete**：delete from r where （condition）

**Alter**：用于在已有的表中添加、删除或修改列。

ALTER TABLE 表名 ADD/DROP/MODIFY COLUMN 列名 数据类型

添加新列时会给已有tuple 这一属性设为null



select from：在选取某个列时，可以指定该列元素重复（select all from）或者该列不重复（select distinct from）。

全选：select * from 表名

没用from： select ATTRIBUTE：获得一个一行一列的表，元素为ATTRUBUTE。

select A1 as FOO：给这个表命名为FOO

select ‘A’ from r：返回一个一列n行的表（n为r中tuple数量），里面元素全是A

select 内嵌表达式： select salary/12 as new_colomn_name from r: 将salary中元素全除以十二，再把表名改为new_colomn name.



select from where: where 里可以用大于等于小于，还可以用关键字and，or，not(注意，相等是一个等号不是两个等号)

select * from r1，r2：from表为r1×r2. 如果两个表中有重名元素会将它命名为r1.A1

对自己select两次：select r as a，r as b。（同样，from 也可以 r as a， r as b）

正则：'\_date\_'中下划线代表字符（一个下划线一个字符）；'%date%'中百分号代表变长通配

转义符\也一样。

select from **order by** A1 desc（asc）：根据属性A1进行降序（升序）排列

between： where salary **between** 90000 **and** 100000: 

**Union**:

> SELECT *column_name(s)* FROM *table1*
> (UNION,INTERSECT,EXCEPT)(ALL)
> SELECT *column_name(s)* FROM *table2*;

将两个结果合并/取交集/取差集到一列中（没有ALL则去掉duplicate）



**Null**:Null的含义是“unknown”。因此对于数值运算，n（运算）null = null

判断：is（not）null

在逻辑运算中，null作为unknown进行运算（即将null作为true和false同时带进去，如果结果一定是true or false则可以得到true或者false，否则结果就是unknown）在where语句中unknown结果是会被当成false的。



聚合函数：avg，min，max，sum，count，参数都是某一列

其中min是返回该列最小值，max是该列最大值。

引出groupby-having语句：group by要在有函数的时候用（avg，min，max，sum，count），意思是根据某个元素（group by name）划分出几组子表，然后在表中使用函数进行运算**（注意！group by name中的name必须出现在select中，并且包括了所有没用被使用聚合函数的列）** having是在group by后面使用，where是在groupby前使用（提前筛掉一部分）简单来说就是：

先筛出一部分->将列中元素分门别类放好并使用函数统计每个子表的元素特性->再根据特性使用having语句筛一部分。



挑出符合特征：

select（distinct） A1

from r 

where condition1 and condition2 and (attribute or primary key)in(select clause)



比较：some语句：where A1 > some(select clause):比select clause里的某一个元素的A1值大就行（有一个为真就行），因此（=some）就是in（但不等于some不一定not in，因为有一个不等于some就行）；

all语句：where A1 > all(select clause)：比全部元素的A1值都要大（全部为真才行），因此（≠all）就是not in（但是＝all不一定是in，因为in是有一个，但是=all是全部都等于才行）。

exists/not exists （select clause）：检查参数是否为空表，一般用法为:

select A from r where condition1 and exists(select clause)。这就是说，先根据condition1将表筛一遍，然后对着每一行检查这一行是不是在select clause里（如果是not exist就是反过来）。

unique（select clause）：要求select clause里没有重复元素。



from里可以嵌套一个select clause，根据这个语句返回的表接着select

with语句：创建一个临时表（with r as（select clause）），其中可以显式声明r的attribute：

with r（A1，A2）as  （select clause）



select可以嵌套select clause，但必须返回的是一个value



将select换成delete且不加参（直接delete from）就可以删掉指定的tuple了。



insert into 表名 values（A1，A2 ... An）/select clause（在select clause中可以强制将某个值修改以添加记录）



Update： Update 表名 set A1 = New_Value Where condition

其中，set语句可以用case语句：

set A1 = case

​					when condition1 then New_Value1

​					when condition2 then New_Value2

​					else New_Value3

​				end