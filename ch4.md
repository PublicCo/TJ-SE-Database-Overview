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

