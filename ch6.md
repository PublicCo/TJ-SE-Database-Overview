## E-R model 专题

三部分：entity sets,relationship sets, attributes

entity:对象，某个人，某个课程，一个entity有很多个attribute（比如一个人的性别，身份证，名字等）

而entity sets就是对象的集合（一个list记录每个人的id，这个list就是记录了人这个对象的集合）

我们将entity sets里的每个entity抽象出一堆属性，用一个矩形记录，上方矩形记录名字，下方矩形记录属性，下划线代表了主键属性

relationship：记录不同entity之间有什么联系（如某个人是另一个人的老师，那么老师与学生就是这两个entity之间的关系）；relationship sets就是记录两个entity set 之间的联系

通常两个entity sets之间，entity的关系是类似的（就像老师set和学生set之间的关系通常是教导），因此relationship set也可以抽象出一个东西

我们用菱形记录relationship set，菱形里的字代表这个relationship的含义

当两个entity之间添加relation时有可能有其他的attribute添加进来（比如我希望学生和老师建立教导关系时会记录日期），我们用一个虚线将代表attribute的矩形和菱形连接起来。

role：entity set自身也可以有联系（比如现在修的课需要先修课，那么课程这个entity set就产生自我关联了）。我们用两条直线将entity set与relationship连接起来，每个直线的名字代表了entity set的某类entity，我们把这类entity叫role

一对一、一对多、多对多：如果relationship set这个菱形指向的entity set是箭头，那么这个entity set在这个关系中最多出一个人；如果是直线，那么可以出任意数量的人（或者说，箭头就代表relation读入另一个entity时，在这个entity set最多找到一个entity与他对应；但如果是直线，可以找到多个）

是否满射：我们用两条直线与菱形相连代表满射。也就是说，遍历另一个entity set,将其中的entity 输入到relation里，relation输出的entity set元素一定包含自己这个entity set里的所有元素。

可以在直线上写l..h，l最小为0，h最大为*（代表任意值）。意思就是另一个entity set输入entity，在这个entity set里可以找到 l-h个entity与他对应。

primary key: relationship 的primary key 比较特殊：如果是多对多，需要两方的primary key才能确定一个relationship。一对多则是由多的那一边的primary key来决定，一对一则两边谁出primary key都行。

weak entity sets：由于这一种entity的primary key（或者其中一部分）是已经在另一个entity被限制了，因此这一种entity依赖于另一个entity存在。（weak entity set必然完全参与relation，因此是双实线连接）我们称这一entity depend on另一个entity

weak entity 用双矩形来框出来，关系也用双菱形框出来。



自顶向下继承：用三角空心箭头指（一般是向上指），指出的entity ”is a“ 被指的entity（如student 指向 person）

自底向上泛化：total 泛化意味着泛化出来的对象必须为至少其中一个底层对象的真子集；partial意味着没有这个必要（默认partial）