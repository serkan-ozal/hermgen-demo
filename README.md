# HermGen Demo
Demo application for [HermGen](https://github.com/serkan-ozal/hermgen)

How to Run Demo Applications
==============
All demo applications (and also their test applications under `test` folder on [HermGen repository](https://github.com/serkan-ozal/hermgen/tree/master/src/test/java)) must be run with `HermGenDistributedClassLoader` as system classloader by `-Djava.system.class.loader=com.hazelcast.hermgen.HermGenDistributedClassLoader`.

Demo-1
-------------
This is demo application tries to find unknown class on **Node-1** (test application node) but since that class doesn't exist at classpath of **Node-1** (test application node), HermGen searches and founds that unknown class on **Node-2** (demo application node) then define it also on **Node-1** (test application node).

* At first, run [demo application](https://github.com/serkan-ozal/hermgen-demo/blob/master/src/main/java/demo1/Demo1.java) at HermGen Demo repository with `-Djava.system.class.loader=com.hazelcast.hermgen.HermGenDistributedClassLoader` VM argument.
* Then run [test application](https://github.com/serkan-ozal/hermgen/blob/master/src/test/java/test1/Test1.java) at HermGen repository with `-Djava.system.class.loader=com.hazelcast.hermgen.HermGenDistributedClassLoader` VM argument.
* You will see log message shows that `demo1.Foo` is loaded from other node (demo application node) to current node (test application node) like this:
```
...
System classloader : com.hazelcast.hermgen.HermGenDistributedClassLoader@6a8814e9
Main classloader   : com.hazelcast.hermgen.HermGenDistributedClassLoader@6a8814e9
Class              : demo1.Foo
Class Loader       : com.hazelcast.hermgen.HermGenDistributedClassLoader@6a8814e9
Hello, I am MotherFoo !
	- Hi, I am BabyFoo !
```

Demo-2
-------------
This is demo application tries to find unknown class on **Node-1** (test application node) but since that class doesn't exist at classpath of **Node-1** (test application node), **HermGen** searches and founds that unknown class on **Node-2** (demo application node) then define it also on **Node-1** (test application node).

* At first, run [demo application](https://github.com/serkan-ozal/hermgen-demo/blob/master/src/main/java/demo2/Demo2.java) at HermGen Demo repository with `-Djava.system.class.loader=com.hazelcast.hermgen.HermGenDistributedClassLoader` VM argument.
* Then run [test application](https://github.com/serkan-ozal/hermgen/blob/master/src/test/java/test2/Test2.java) at HermGen repository with `-Djava.system.class.loader=com.hazelcast.hermgen.HermGenDistributedClassLoader` VM argument.
* You will see log message shows that `demo2.User` typed object, put to `IMap` by other node (demo application node), is loaded from `IMap` although `demo2.User` is not defined on current node (test application node) like this:
```
...
System classloader : com.hazelcast.hermgen.HermGenDistributedClassLoader@6a8814e9
Main classloader   : com.hazelcast.hermgen.HermGenDistributedClassLoader@6a8814e9
Hello, I am user Serkan
```
