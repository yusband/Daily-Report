##chp6
- 接口
- 内部类
- 克隆
- 代理

###接口
- 接口对应的是功能、
- 接口所有的方法默认都是public，所以接口内部的方法不需要加上public；但是在实现类中，则必须加上public(前面说过子类的方法的可见性不能够低于父类)
- 接口中的域都默认为是public static final
- 接口中的内部类默认为public static
- 接口中不含实例域（variables declared in interface are by default public, static and final. Since it is static you cannot call it instance variable.）
- java是强类型语言---实现了接口就可以表明该类的实例(非抽象类)一定可以调用接口里的方法

####Q:有了抽象类为什么还需要接口？
接口是更侧重于"功能"的另一种抽象思维的体现：将某种功能抽象化，而不需要抽象类那样的继承关系；此外，类可以实现多个接口，这样接口的使用要比抽象类更灵活(低耦合、高聚合)。

当对象是不可变类的实例时，浅拷贝创建的子对象在声明


###克隆
- Object类的clone方法是protected，所以只能够在子类内部调用，若需要在外部使用则需要重写clone方法并将修饰符改为public
- 需要执行clone操作的实例的类必须实现Cloneable接口，这是一个标记接口，不含有任何方法
- 需要为自定义的clone方法声明一个CloneNotSupportedException异常()
 另一种复制对象的方法是序列化操作，简单、安全但是效率较低



###内部类
- 内部类含有一个隐式的外围类的引用，经由该引用可以获得外围类的域
- 内部类是一种编译器现象，在编译后内部类会被翻译成外围类$内部类.class
- 可以将内部类的声明完全放在一个方法内部：
 - 这样的内部类称为局部内部类
 - 不能使用public private修饰符，因为局部内部类的作用域被限定在该方法中
 - 局部内部类对外界完全隐藏，同一个类中的其他方法不可以访问该类
 - 局部内部类还可以访问所在方法的局部变量（需要被设置为final），事实上，调用所在方法时传入的参数会被局部内部类备份。
- 匿名内部类
 - 没有类名，所以没有构造器；只能在构造时传入参数交给父类的构造器进行构造，而如果匿名内部类拓展的是接口（接口没有构造方法）则不能含有任何构造参数
 - 匿名内部类如果代码量很小，可以节省一些录入时间；但匿名内部类会让程序看起来比较混乱
 - "双花括号构造法"——new SuperClass/interface(){{...}}；内部额外的花括号属于对象构造块；
 - 静态方法无法通过getClass()获取当前类名，可以通过new Object(){}.getClass().getEnclosingClass();获得静态方法的外围类名
- 静态内部类 
 - 静态内部类又叫嵌套类，相比较于一般的内部类只是其不能引用外围类的对象
 - 使用静态方法构造的内部类对象，该内部类必须是静态内部类

###代理：
利用代理可以在运行时创建实现了一组给定接口的新类；这种功能只有在编译时无法确定需要实现哪些接口时才有必要使用 
> A dynamic proxy class (simply referred to as a proxy class below) is a class that implements a list of interfaces specified at runtime when the class is created, with behavior as described below. A proxy interface is such an interface that is implemented by a proxy class. A proxy instance is an instance of a proxy class. Each proxy instance has an associated invocation handler object, which implements the interface InvocationHandler.  
