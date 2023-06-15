SQL 函数：

语法：create function *function_name* (*para1*,*para2*....)

​				returns *type*

​				//中间变量定义

​				declare *tmpname* *type*;

​				*执行语句*

​				return *result*

​			end

对于return，可以return int，char，也可以return table（attribute 1，attribute2...）

return table的用法：select * from table(*function_name*(*para*))

另一种写法：

create procedure *funcname* (in *para* ,out *para*)

begin

​	语句

end

in 指输入的参数，out指输出的参数



**Triggers**

可以是insert,delete,update,对于delete 就用referencing old row as...;对于insert就用referencing new row as,update 就即引用old也引用new

语法：create trigger *triggername* before/after update/insert/delete of *listname* on *attribute*

referencing new/old row as *rowname*

*函数语句*

