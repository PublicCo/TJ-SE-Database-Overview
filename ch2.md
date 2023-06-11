关系：R=(A1,A2,……An),其中An是某个元素

比如：   *instructor*  = (*ID, name, dept_name, salary*)

instructor就是一种关系

关系实例：r（R）

其实R就是表头，r（R）就是表内数据

t就是表内数据的元素，An就是表头的类别

同样的：schema就是表头：  instructor (*ID, name, dept_name, salary*)

Instance就是整个表的数据

Superkey：首先K是R的子集，其次每个K可以对应唯一的一组tuple。

Candidate Key：无法继续剔除其中元素的superkey

primary key：candidate key的其中一个。选简单的

比如（A），（B，C）都是Candidate key，那么选（A）作为primary key

Foreign Key：

referencing relation：引用者，一般是某个表的某个属性

referenced relation：被引用者：另一个表的candidate key

几个符号：

•select: σ

•project: Π

•union: ∪

•set difference: *–* 

•Cartesian product: x

•rename: ρ

例如：σ*dept_name=**“**Physics”* (*instructor*)就是从instructor表实例中选择dept_name=**“**Physics”符合的tuple

逻辑符号：大于等于小于，与或非（∪∩）

 project：ΠA1...Ak（r），就是从r中移除1到k属性之外的属性列（或者说选出1到k的列），并且将剩余列中重复的行移除（表是集合）

乘（x）：对于表A，表B相乘，每个Ak后面会接B1到Bn，然后形成一个m乘n列的表。通常会添加select来剔除一些元素。因此，有了如下语句：

​        r⋈_θ s=σ_θ (r × s)

所以⋈为join符号（全相联）

并运算：要求两个实例r1，r2有同样的表头

交运算：同上

减运算（-）：在A且不在B，要求同上

赋值运算(<-)将某些结果赋值给变量（*Physics* <-σ**dept_name=**"**Physics**"(*instructor*)）

ρ*x* (*E*)指将E结果命名为x