##MVP、MVC和MVVM
-在android中，这几种设计模式是如何体现的？
了解了基础的概念[MVC vs. MVP vs. MVVM](http://kb.cnblogs.com/page/120678/)之后，联想到在android中这些架构模式的体现。
在[Android App整体架构设计的思考(一) ](http://blog.csdn.net/luyi325xyz/article/details/43085409)了解了一个大概。
-Activity常常会出现代码量过于臃肿的情况，这是因为在Activity中兼顾了View的交互以及Controll的逻辑这两大职责。
-在将部分的逻辑处理转移出去之后，Activity依旧庞大，这时候需要对MVP架构进一步进行优化：
```
 转移逻辑操作之后可能部分较为复杂的Activity内代码量还是不少，于是在分层的基础上再加入模板方法（Template Method）。具体做法是在Activity内部分层。其中最顶层为BaseActivity，不做具体显示，而是提供一些基础样式，Dialog，ActionBar在内的内容，展现给用户的Activity继承BaseActivity，重写BaseActivity预留的方法。如有必要再进行二次继承，App中Activity之间的继承次数最多不超过3次。
 ```
