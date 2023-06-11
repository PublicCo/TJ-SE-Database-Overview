**DBMS**：Database management system,管理数据库的系统（如Oracle，mysql等）

数据库常见的使用地方：银行存款，超市购物信息，大学生绩点系统等

使用目的：数据存储冗余and容易出错；没有统一的接口获取数据；数据存储方式很乱；数据不符合实际生活规范要求；并发更新出错；数据安全问题

表头：Column；表数据：Rows

抽象层：物理层，逻辑层，View层（可以根据权限隐蔽一些信息）

Data Definition Language(DDL)：数据定义的方式

Data Manipulation Language（DML）：就是请求语句，用户请求数据（显示声明或隐式声明获得方式）

最简单的就是Select from where

数据存储：files，dictionary（可以存数据存储有关信息），indice（指针，索引）

查询：DDL翻译器（把数据翻译为指定类）和DML编译（解释？）器（将查询语句整出来）

查询过程：语句输入->翻译语句->翻译成关系范式语句->optimizer（这个存疑，15章没听忘了）->查询方案选择优化->开查！->获得数据

Transaction Management:用来保证数据库使用过程中的一致性与安全性

架构：Two-tier：用户请求前端，前端直接向数据库要数据

Three-tier：用户请求前端，前端发给后端，后端发给数据库，数据库再发回去

DBA：数据库管理员，不能由坏人来当.jpg