无损分解：要求分解出的r1×r2 的结果等于r。如果r1×r2包含r，说明有损

functional dependency：函数依赖的意思是：对于R中某个attribute a，b；如果在tuple里t1[a]=t2[a]一定可以推出t1[b]=t2[b],就说存在a->b

**注意！如果a其实是主键（换句话说，没有两个tuple能够让t[a1]=t[a2]),仍然可以说明a->b,因为t1[a]=t2[a]时就说明他们其实是一个tuple，则t1[b]=t2[b])**

闭包：如果说所有的函数依赖集合用F表示，那么这个集合的闭包就用F+（F右上角加个+）来表示。闭包即要求添加传递性（自反默认，不用对称）。

闭包判断superkey：对于属性集合（键）K，只需要K->R（或者说K的闭包=R）那他就是superkey。如果要当candidate key，就要求K没有子集可以成为superkey。

如果tuple集合r符合关系集F，那么r satisfies F, F holds on r.

trivial functional dependencies: 如果b是a的子集，那么a->b就是trivial的。

**判断lossless：对于分解出来的R1,R2，如果R1∩R2->R1或R2，那么分解就是lossless的**

例：R={A，B，C}，F={A->B,B->C},那么分解为{A,B},{B,C}就是无损的。因为R1∩R2={B},而B->{B，C},BC = R2.



保持函数依赖：当表被拆成两张表后，如果函数依赖集可以仅根据这两张表来检查而不需要重新将两个表乘回去检查，那么就说这个分解是保持函数依赖的。

BCNF：要求：对于R和F，如果F的闭包F+中的所有函数依赖在R的属性都满足下列关系：
1：a->b是trivial的（b是a子集）

2：a是R的superkey

那么就说R满足BC范式。

BC范式分解算法：对于任何使得表不满足BC范式的functional dependency a->b,将这个表分为：

R-（b-a) 和（a∪b）。

BC肯定无损，但是dependency preservation不一定能满足。为了满足dependency preservation，我们采取Third Normal Form的分解

Third Normal Form：要求：对于R和F，如果闭包F+所有关系a->b满足如下关系：

1：满足BCNF

2：对于在b不在a的attribute，这些attribute都在R的candidate key的一部分（每个attribute可以在不同的candidate key里，但必须在）

3NF存在information repetition,且有时会要用null来占位，但可以在一张表内检查所有的functional dependency。

无损分解是必须的，3NF和BCNF的权衡点在于是否需要维持函数依赖检查性和redundancy是否应该存在。

第三范式分解：首先计算canonical cover，然后把每个canonical cover 中的a->b的a，b放在同一个r中：r（a,b),然后检查是否有表中属性加起来是r的candidate key，没有就加一个表，里面属性是candidate key。最后检查是否有表是其他表的子集，删去重复的表。



关系理论：

关系集F，闭包F+，正则覆盖Fc

闭包：对于F，如果不满足传递性就给他添加传递性，添加到不能添加就是F+

闭包计算定理：

* 如果b被包含于a，那么a->b；
* 如果a->b,那么ca->cb;
* 如果a->b,b->c,那么a->c

由此推出如下定理： 

* a->b 且 a->y,那么a->by(a->ay,ay->by)
* 如果a->by,那么a->b且a->y(a->by,by->b or by->y)
* 如果a->b 且by->c,那么ay->c(ay->by,by->c)

检查闭包属性集方法：如果属性集可以推出新的属性就把新属性加进来，直到推不出新属性。

如果闭包属性集包含了R中所有属性，那么这个属性就是superkey

检查是否有a->b，只需要检查b是不是在a的闭包属性集里。

正则覆盖：用于检查修改是否违反函数依赖的最小依赖集。我们需要将多余的attribute从F中踢出去，并且不改变F+。

判断多余：总的准则就是如果去掉了仍然不改变闭包属性集，那么就是多余的；右侧依赖多余即去掉右侧的某个属性，左侧的闭包属性集仍然能推出右侧去掉的那个属性；左侧多余即去掉左侧某个属性，左侧的闭包集仍然能够推出右侧整个属性集。

判断是否dependency preserving：判断总的F的闭包是否等于每个分解出去的functional dependency的闭包的和。

检测是否为BCNF：只需要检查所有的关系依赖F是否满足BCNF；然而，在decompose后有可能因为关系不存在于任一子集中导致错误认为每个R都是BCNF的。因此，检查依赖闭包F+是最稳头的方式。这很麻烦，因此另一个算法是：我们仍然考虑没有分解的集合，但对于分解出来的Ri的属性子集，检查这个子集的闭包属性集是否包括Ri中所有元素（这是主键）或者闭包属性集没有Ri-a中的元素。

   

多值依赖：如果对于三个或多个属性，满足：如果x1,y1,z1 和x1,y2,z2在r中，那么x1,y2,z1和x1,y1,z2在r中，就说y->->z（y对z多值依赖）

函数依赖就一定是多值依赖。

第四范式：如果a->->b,那么a满足：这个关系是trivial的（b是a子集或者a∪b=R），或者a是R的superkey。那么这个R满足第四范式。

拆的算法和BC范式类似，就是把多值依赖的左右都放进R１中，并把R中ｂ的内容删掉成为R２.

