### 如何创建自己的jar包？
- `jar cf jar-file input-file(s)`

``` bash
jar cf ./dist/fish-bird.jar ./com/github/Bird.class
```

### 编译阶段如何引用jar包？
#### 使用 `-d` 来指明jar包所在的目录
``` bash
javac -d ./dist Main.java
```

#### 或者使用`-cp`
``` bash
javac -cp ./dist/*.jar Main.java
```
这一步又很坑，不能使用`./dist/*`

### 启动时引用
好了,./dist文件夹有我们的jar包和Main.class,那么如何执行呢？
``` bash
$ java -cp ./dist/fish-bird.jar:. Main
hi, I am a Bird

$ java -cp ./dist:. Main
hi, I am a Bird

$ java -cp ./dist/*:. Main 
Error: Could not find or load main class ..dist.fish-bird.jar
Caused by: java.lang.ClassNotFoundException: //dist/fish-bird/jar
# failed, 使用*必须加上引号

$ java -cp "./dist/*:." Main
# success
```