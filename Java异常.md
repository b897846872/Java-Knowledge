## Java异常
所有的异常类是从 java.lang.Exception 类继承的子类。
Exception 类是 Throwable 类的子类。除了Exception类外，Throwable还有一个子类Error 。
Java 程序通常不捕获错误。错误一般发生在严重故障时，它们在Java程序处理的范畴之外。
Error 用来指示运行时环境发生的错误。
例如，JVM 内存溢出。一般地，程序不会从错误中恢复。
异常类有两个主要的子类：IOException 类和 RuntimeException 类。
![1](http://www.runoob.com/wp-content/uploads/2013/12/12-130Q1234I6223.jpg "1")
![2](https://images2015.cnblogs.com/blog/1189312/201707/1189312-20170703132540112-2053625299.png "2")
- **Error**类中包括虚拟机错误和线程死锁，一旦Error出现了，程序就彻底的挂了
- **非检查异常**：该异常的出现绝大数情况是代码本身有问题应该从逻辑上去解决并改进代码。
- **检查异常**：该异常我们必须手动在代码里添加捕获语句来处理该异常。**没有完善错误处理的代码根本没有机会被执行**。

**在 Java 中你可以自定义异常。编写自己的异常类时需要记住下面的几点:**
- 所有异常都必须是 Throwable 的子类。
- 如果希望写一个检查性异常类，则需要继承 Exception 类。
- 如果你想写一个运行时异常类，那么需要继承 RuntimeException 类。
