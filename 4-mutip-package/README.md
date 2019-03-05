```
src.1 $ javac Main.java
$ tree
.
├── Main.java
├── OTHER
│   └── com
│       └── github
│           ├── Bird.class
│           └── Bird.java
├── README.md
└── xyz
    └── bitfish
        ├── Fish.class
        └── Fish.java
```

## 编译时指定多个路径
```
$ javac -cp ./OTHER:. Main.java
```
通过cp指明所有依赖的.java文件，记得不要忘了当前文件夹，因为指明cp会覆盖默认设置

## 执行时引用多个
```
$ java -cp ./OTHER:. Main
hello world
hi, I am a Bird
```
一个classpath用于寻找Main，一个用来寻找相关的包