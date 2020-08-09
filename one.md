> 今天上班第一天看到一些以前没有接触过的东西

[toc]
##  AtomicLong

1.  `AtomicLong` 类 
     1. 介绍
         1. `AtomicLong` 类存放在`java.util.concurrent.atomic` 包中
         2. 他的作用是在 `Java`中对长整型进行原子操作
         3. 因为在32位操作系统当中，64位的 `long`,`double`变量会被`JVM`当做两个分离的32位来操作，所以他是不具备原子性的, 使用`AtomicLong`能让`long`的操作保持原子型
     2. 类结构图
        1. ![AtomicLong](https://raw.githubusercontent.com/zhuhedong/oss/master/AtomicLong.jpg)
     3. 内部类
        1. 无
     4. 字段
        1. serialVersionUID
            1.`long` 类型
            2.`static`静态的
            3.`final` 不可修改，不可继承
            4.`Jvm`会把传来的字节流中的`serialVersionUID`字段于本地相对应实体类的`serialVersionUID`进行比较，如果一直那么久进行反序列化，不一致则会出现异常`InvalidCastException`
        2. unsafe 
            1.`Unsafe` 对象类型 
            2.提供类似于C++中手动管理内存的能力 
            3.Unsafe类是"final"的，不允许继承。且构造函数是private的
            4.需要通过Java的反射去实例化这个对象
            5.内部使用Unsafe类的compareAndSwapLong方法进行CAS更新操作
        3. valueOffset
            1.value变量在该类中的偏移量 
        4. VM_SUPPORTS_LONG_CAS
            1.记录底层JVM是否支持长整型的无锁CompareAndSwap操作
            2.虽然Unsafe类的compareAndSwapLong方法在两种情况下都是有效的，但在Java级中应该处理一些结构 
            3.以避免锁定用户可见的锁
        5. value
            1.内部维护了一个value值，用来存储原子变量值 