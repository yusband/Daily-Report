##chp11:

###java的异常层次结构：
Throwable---Exception&Error  Exception---IOException&RunTimeException
- RunTimeException都是你的错误
- Error是系统内部错误or资源耗尽错误，应用程序不应该抛出这样的异常。除去通报信息之外，无能为力。
- Error&RunTimeException成为checkedException
- IOException称为uncheckedException

###有四种情况涉及到抛出异常：
- 调用一个抛出已检查异常的方法，例如FileInputStream构造器
- 程序运行过程中发现错误，并利用throw语句抛出一个checked异常
- 程序运行过程中发现错误，抛出一个unchecked异常
- jvm和运行时库出现的error
注：
- 前两种情况（checked异常）必须声明(抛出或者捕获），第三种情况不应该在方法中抛出只能因为这代表代码写错了；最后一种情况会自动抛出
- 子类如果覆盖了父类的一个抛出了异常的方法，则子类中该方法抛出的异常不能比父类中的更通用：
比如父类的方法throw了FileNotFoundException，那么子类就不能抛出FileNotFoundException的父类IOException；当然子类也可以覆盖掉父类中需要抛出异常的操作而不需要在方法声明中抛出异常。
而如果父类的方法没有抛出异常(方法为空或者没有需要抛出异常的逻辑)，而子类覆盖的方法中如果有了需要抛出异常的逻辑，则只能add exceptions to method signatures in the whole method hierarchy
- exception是可以自由定义的


###Q：选择在方法签名中声明抛出异常还是在方法内部捕获抛出的异常？


###try/catch
- try/catch语句中如果try中运行正常则跳过catch语句；
- 可以使用多个catch语句捕获多个异常；也可以将多个异常放在同一个catch语句中捕获(使用|隔开，此处的多个异常不允许有继承关系) 
```
catch (FileNotFoundException | MyException exception) {
            exception.printStackTrace();
        }
```
- 可以在catch语句中抛出异常：对捕获的异常进行封装再抛出。
- finally语句一定会被执行，不论try语句中是否有异常、也不论该异常是否被catch语句捕获：
 - 建议使用独立的try catch /try finally语句（在try catch的try中嵌套一个try finally）
 - finally语句中如果含有return语句，会覆盖之前已有的返回值
 - fianlly语句也可能会抛出异常...再嵌套一个trycatch？java se7给出新的办法（使用带资源的try语句，即资源实现了AutoClosable接口，try语句执行结束后会自动关闭资源）
