#AOP & OOP

> [重学Spring之面向切面](https://mp.weixin.qq.com/s?__biz=MzA4NTE1MDk5MA==&mid=2672797679&idx=1&sn=4c44e1a27b37cd30505f1f1eec88f51a&chksm=85675b8eb210d298295ed6a51fe16a632d83d732413564e88e508c66a1cebe77e89a6c0cb9fe#rd)

面向对象侧重静态，名词，状态，组织，数据，载体是空间。

面向过程侧重动态，动词，行为，调用，算法，载体是时间。



行为（方法），状态（属性）。



web项目中，controller、servicer、dao等组件层，有行为而无状态，即使有属性，也只是对下一层组件的特有；

vo、entity等modle，有状态而无行为，围着状态打转；



程序需要状态，但组件不需要状态，甚至如果组件拥有了状态，会出现并发等烦人的问题。

程序的状态，统一由数据库、缓存、任务队列等外部容器持有；处理时，仅在对象的方法中以局部变量的形式出现，被封在线程内部，朝生夕灭，任由回收。



web开发，本质是用面向对象的组织，面向过程的逻辑，来解决问题。

但是仍然会遇到另一种问题，即假如一个流程分三步：X、A、Y，另一个流程也分三步：X、B、Y。

具体业务实现就会是XAY、XBY，明显这样是不对的，违反了**DRY**原则；如果把X、Y分别抽象成一个方法，但至少还是要写一条语句来调用，就成了xAy、xBy，重复依然在。

如果采用**控制反转**来处理这种问题，就是采用模板方法的模式，在抽象父类方法体里声明x?y，其中?为抽象方法，由子类实现；但是这里就出现了**继承**，而且调用者只能调用父类声明的方法，**耦合性**太强。

所以，只有哪些本来就是调用者调用父类声明的方法的情况，如表现层，或者说本来就不用太灵活，如只提供CRUD的持久层，才总是出项抽象父类的影子。



这类问题可以抽象成：在A或者B执行前，或者执行后，做点什么操作。

这就是面向切面。



Filter就是一层一层的切面，但是只能在Servlet之外，能上不能下，过于暴力。

Spring AOP的实现方式：**Java动态代理**、**Cglib** （默认使用动态代理，如果目标对象没有实现接口时，就会使用后者），采用**代理模式**，Filter (Struts2 Intercepter) 则是**责任链模式**；



目标对象，代理对象；



重构时可以先考虑使用策略、装饰器、模板方法等模式，如果解决不了时，就可以考虑使用AOP了。



[使用core Java实现AOP](http://www.importnew.com/15420.html)



#### AOP & IOC



