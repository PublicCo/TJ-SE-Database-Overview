Join语句：分natural join，inner join和outer join

语法：from r1 ()join r2（）join r3

natural join：r1乘r2，将相同attribute的值都一致的tuple留下，重复的tuple会只留下一个。

为了防止全匹配，可以用using来指导匹配哪个字段：

from r1 join r2 using(A1)

同样可以用on来实现类似于where的功能：

from r1 join r2 on condition

但有时候我们希望不要删去表中的元素，这时用outer join（如果相同的类型没有匹配的则将另一边的数据置为null）

left outer join：左表的元素不能被删；right outer join：右表的元素不能被删；full outer join：两边的元素都不能被删

inner join 和natural join区别在于inner join是不会删去同名列的（一般来说，由你来指定哪两列相等作为join），一般为 r1 inner join r2 on condition



View: 用于hide一些数组的列来保证权限管理。

语法：create view v as (select clause):v 只能接触到select clause这个子表中的数据

依赖：直接依赖就是v2是从v1的select clause中产生的，依赖就是v2从v1的子表产生的（自己也行）

插入view：insert into View_Name values(A1,A2,...An)

要求：value里要有view 的每一个属性。

由于insert可能破坏view中的关系限制，一般不让update，只允许simple view update，即select只有属性名，from只基于一个db，没被select的attribute是可以设为null的，且没有group or having语句

transaction：要求原子化，要不就完成所有工作，要不就一点commit都不做，不能提交一半更新不提交一半更新

constraints：not null,primary key, unique, check(condition)(即要求db始终符合这个condition)

foreign constraint：语法：foreign key（Attribute_Name) references list(primary):其中Attribute name是自己的键，list是另一个表，Attribute_Name是list的candidate key

对于foreign constraint，用delete/update cascade可以级联删除或者更新

断言：语法：create assertion \<assertion-name> check (condition)

自定义的struct：create type *typename* as *type*

对表设置索引：create index \<indexname> on \<table>(attribute)

权限设置：grant \<可以执行的操作权限> on <表或view> to <user-id或public>

权限类别：insert,update,delete,all privileges

取消权限：revoke <权限> on <表或view> from \<user-list>(任何基于该权限设置的权限在被取消后也一并取消)

设置权限role:为某个人贴个“标签”，然后为标签设置权限：

生成：create role rolename

设置user：grant \<role> to \<username>

设置权限: grant \<privillege> on <list/view> to \<rolename>

设置外键constraint：grant reference(primary key) on (list-name) to (role-name)
