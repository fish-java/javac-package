# 基本使用
在当前目录下创建`Hello.java`
``` bash
$ javac Hello.java
$ java Hello
Hello Friend!
```

很完美，但是来一点变化
``` bash
$ cd ..
$ java ./base/Hello
Error: Could not find or load main class ..base.Hello
Caused by: java.lang.ClassNotFoundException: //base/Hello
$ java ./base/Hello.class
Error: Could not find or load main class ..base.Hello.class
Caused by: java.lang.ClassNotFoundException: //base/Hello/class
```

哎，好像出错了。

我不清楚读者朋友有没有犯过这样的错误，但是我之前一直写的是nodejs，然后nodejs它是基于文件系统进行模块管理的。程序员可以通过相对或绝对路径的来指明文件的入口，所以我想当然的在Java中也来这一套。

但是其实Java的模块管理其实是基于包的，它是怎么查找.class文件的呢？

Java中的包有三种，具体参考[官方文档](https://docs.oracle.com/javase/8/docs/technotes/tools/findingclasses.html)。

前两种只要你安装JDK后没有瞎折腾，`javac` 和 `java`肯定能找到，这里就不多说了。我们关键说用户自定义的包。

## 用户自定义的包按照下面的规则来查找

### 默认是`.`文件夹，也就是`javac`或者`java`的启动目录

所以之前我们在base目录下执行`java Hello`可以成功，因为`java`把base目录加它的检索范围，它在这个目录下找到了Hello.class文件，然后执行了它。而在第二次的时候，`java`把base目录的上一级目录加入到了检索范围，而它又不会递归的向下查找，所以它找不到Hello.class文件，然后就报错了。

那怎么解决这个问题？往下看

### 然后`java`会查看shell的环境变量，看看CLASSPATH的值。
也就是网上的经常查到的命令行程序

### 通过`-cp`或者`-classpath`指定
``` bash
$ java -cp ./base Hello 
Hello Friend!
$ java -classpath ./base Hello
Hello Friend!
```
我们可以通过这两个参数来指定类的查找路径

#### 参数风格
- 参数位置不能变，这和nodejs很不同
- 单 - 开头的风格，晕

``` bash
# 当然如果我们希望在这个目录编译Hello.java，可以：
$ javac ./base/Hello.java
```

### -jar
这个我们等会再说

## 总结
这种类查找机制一开始我是懵逼的。你不能通过文件路径来寻找class文件，而是把class文件所在的目录添加到环境变量中，然后`java`从所有的classpath里面搜索。