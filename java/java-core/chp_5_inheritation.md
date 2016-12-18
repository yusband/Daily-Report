##chp5继承

####父类的私有域是否被继承
- 子类含有父类的私有域，但不能直接使用；只能通过父类相应的get方法获取该私有域。
- 当父类的get方法被子类重写时，如果需要在重写的get方法中获取父类的相应域，需要使用suoer关键字引用父类的get方法。
- 当子类中拥有和父类中某个私有域重名的域时，子类的该域会覆盖父类的该域。

####super和构造器
- 当父类中不含默认构造方法时（空的构造方法），子类从父类中继承的域只能通过父类的构造方法完成初始化（且该语句必须是子类构造方法第一行语句），而不能够自行对其赋值
- 此时若子类的构造器没有通过super关键字调用父类的构造器时，会报错
- 当父类中含默认构造方法时（空的构造方法），则没有必要使用super关键字引用父类构造器

####ArrayStoreException
对于同一个完成初始化的子类对象数组，可以使用父类的数组变量指向该数组，并将数组中的对象使用父类的构造方法初始化；这样做在可以通过编译，但是对该父类对象使用子类的方法时（如set一个子类特有的域的值），会因为该域在父类对象中不存在抛出ArrayStoreException。
```
       Boy[] boys=new Boy[10];
       Human[] humen=boys;
       humen[0]=new Human();
       //只有boy拥有toy，而boys[0]是一个Human对象
       boys[0].setToys(100);
       System.out.println(boys[0].getToys());
```

####动态绑定的过程
1. x.f(params)，知道x的声明类型和方法名，在该类中搜寻拥有该方法名的方法及其超类中搜寻访问权限为public的方法名一致的方法
2. 在上一步获得的所有方法中匹配参数，这一过程成为重载解析，若没有匹配则报错
3. 调用和x的类型(实际类型)最匹配的那个方法
注：虚拟机为每个类创建了一个方法表，真正调用方法时搜索这个表


####关于Object类中的方法：
- equals以及编写自己设计的类时需要重写equals方法的几点注意事项
- hashcode方法：重新定义了equals方法就必须重新定义hashcode方法--将在hashtable中讨论
- toString方法
- 其他的方法跟线程相关

####数组、数组列表（ArrayList）
涉及到了一点操作效率的描述：
- 数组操作比对象操作高效很多
- 数组列表的容量是可以自动扩展的
- 总是在数组中部进行增删的操作效率会随着数组容积变大而降低，这种时候需要使用链表代替数组

####final 关键字
- 包装类都是不可变类（final）
- final类中所有方法都默认是final，而域不是

####抽象类
- 含有抽象方法的类必须声明为抽象类：为了提高程序的清晰度
- 不含抽象方法的类也可以声明为抽象类
- 抽象方法没有方法体，以；结尾，充当着占位的角色
- 抽象类可以作为变量类型名，引用一个非抽象子类的实例
- 抽象类是对父类的更高一层次的抽象

####反射机制：
- Q：反射机制是什么？
A：the ability to examine or modify the runtime behavior of applications running in the Java virtual machine.（常用到getClass().getSimpleName()获得对象类型名做为log的TAG) 
- Q：反射机制优点和缺点？
A：反射机制能够在运行中分析类、查看对象的信息、通用的数组操作代码(泛型)；可以越过非反射机制下代码中设置的权限进行操作。这样破坏了封装性、有安全隐患同时反射机制会消耗更多的时间。
- Q：应用场景：主要应用于工具的创建而非应用开发，如文件浏览器、单元测试工具
参：
- [Reflection API](http://docs.oracle.com/javase/tutorial/reflect/index.html)
- [What is reflection and why is it useful?](http://stackoverflow.com/questions/37628/what-is-reflection-and-why-is-it-useful)
- [Java Reflection: Why is it so slow?](http://stackoverflow.com/questions/1392351/java-reflection-why-is-it-so-slow)


基本数据类型的强制转换
####类继承的设计技巧：
1. 公共操作、域放在父类
2. protected修饰符(同一个包以及子类可见)对于需要在子类中重新定义而不是一般用途的方法很有效(如android中Activity的onCreate()方法)，否则不实用
3. 继承要严格符合 A is a B的逻辑关系，某些相互包含的关系容易混淆(钟点工相较于雇员，没有salary这个域)
4. 所有继承的方法都要有意义
5. 继承的方法在重写时，不应该改变用途
6. 当需要在某个方法里需要对不同的子类对象加以区分时，额外加上一个标签变量(tag)不如利用多态性解决
7. 少用反射
