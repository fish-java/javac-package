# package
接下来说包的概念。我以前是真的晕，当时在eclipse中又是什么新建一个类，一个包，一个项目，真的懵逼。说多了都是泪，如果当初我是从Python或者JS开始学多好。

初学Java的，建议从普通的文本编辑器开始，不要使用IDE！！等到搞清楚命令行，把坑踩一遍再使用IDE.

其实包就是一种目录结构。我们可以在当前文件夹创建
```bash
$ mkdir -p com/github/fish
# 这就是我们的包了
```

然后把我们之前的Hello.java复制到fish文件夹里面,然后添加
```
package com.github.fish;
```
到Hello.java 声明这个.java文件是属于这个包的。其实我觉得在编译阶段`javac`能够推断出包名的，但是写了这个的话方便IDE工作。

## 解析
这其实就是Java中的模块化方式。像在nodejs和python中，都是基于文件系统来管理的。但是Java（其实其他编译型语言一样）做不到这一点。

因为中间有一个编译过程，.java文件要被编译成.class文件，所以你要是像nodejs那样就没办法写。

同时如果想nodejs那样import了一个模块，这在Java中没办法表示import的这个是什么东西。因为Java是完全基于类的，而nodejs是基于对象的，我们在nodejs中import的东西就是一个模块对象，Java中不好表达他

那我们怎么做

```
$ javac com/github/fish/Hello.java
$ java -cp . com.github.fish.Hello 
```
大家看到了吗，当我们编译一个java文件的时候，我们是通过相对或绝对路径找到这个文件的。

而如果我们尝试执行这个class文件的话，我们是把这个包所在的目录添加到`java`的搜索路径的。然后我们通过包名来指定对应的main class。

在`java`加载不同的包的时候，它们其实是平行的列表

java.lang ...
java.io ....
...
com.github.fish ...
...

这也是为什么Java推荐大家根据自己的域名来命名包，因为它们都是平行的，如果随意命名很容易冲突

## 对比
- js python 的模块管理机制是通过文件系统来的
  而且import一个包的时候就是相当于生成一个模块对象，你可以把它赋值给一个变量，然后自己用

- 而java中的是基于包管理机制的，它的包是扁平化，所有的包都是平级的
  - java.lang.*
  - xyz.bitfish.*
  JVM通过相关的规则找到它们之后，它们就在同一个层级，就想到与都在一个目录下面，所以Java强调大家都用自己的域名来命名包。。。。。