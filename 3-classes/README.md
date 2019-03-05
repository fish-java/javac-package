如果没有写包名，其实他们都在一个`无名包`之中
``` bash
$ ls
Dog.java Main.java  README.md
$ javac Main.java
$ ls
Dog.class  Dog.java   Main.class Main.java  README.md

$ java Main
Bob is marking
```