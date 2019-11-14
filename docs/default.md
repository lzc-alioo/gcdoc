启动java进程时不添加任何jvm参数的情况

# 测试环境
> OS
```
[root@altc1-mytest1 build]# more /etc/centos-release
CentOS Linux release 7.5.1804 (Core) 
[root@altc1-mytest1 build]# uname -a                
Linux altc1-mytest1.lego.elenet.me. 3.10.0-229.el7.x86_64 #1 SMP Fri Mar 6 11:36:42 UTC 2015 x86_64 x86_64 x86_64 GNU/Linux
[root@altc1-mytest1 build]# free   
              total        used        free      shared  buff/cache   available
Mem:      131863848    11706188     8327464     5256020   111830196   114285448
Swap:       4063228     2283700     1779528
```

> jdk版本
```
[root@altc1-mytest1 build]# java -version
java version "1.8.0_45"
Java(TM) SE Runtime Environment (build 1.8.0_45-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.45-b02, mixed mode)

[root@altc1-mytest1 build]# which java
/root/work/jdk1.8.0_45/bin/java
```

> java进程
```
[root@altc1-mytest1 build]# ps aux|grep -i md5
root      564177 59.0  1.6 37029560 2136496 pts/2 Sl  08:07   2:05 java -cp javademo-1.0.0-SNAPSHOT-jar-with-dependencies.jar com.alioo.md5.Md5demo
```
---

# jinfo解释说明
> jinfo命令示例
```
[root@altc1-mytest1 build]# jinfo 564177
Attaching to process ID 564177, please wait...
Debugger attached successfully.
Server compiler detected.
JVM version is 25.45-b02
Java System Properties:

java.runtime.name = Java(TM) SE Runtime Environment
java.vm.version = 25.45-b02
sun.boot.library.path = /root/work/jdk1.8.0_45/jre/lib/amd64
java.vendor.url = http://java.oracle.com/
java.vm.vendor = Oracle Corporation
path.separator = :
file.encoding.pkg = sun.io
java.vm.name = Java HotSpot(TM) 64-Bit Server VM
sun.os.patch.level = unknown
sun.java.launcher = SUN_STANDARD
user.country = US
user.dir = /root/gitstudy/javademo/build
java.vm.specification.name = Java Virtual Machine Specification
java.runtime.version = 1.8.0_45-b14
java.awt.graphicsenv = sun.awt.X11GraphicsEnvironment
os.arch = amd64
java.endorsed.dirs = /root/work/jdk1.8.0_45/jre/lib/endorsed
java.io.tmpdir = /tmp
line.separator = 

java.vm.specification.vendor = Oracle Corporation
os.name = Linux
sun.jnu.encoding = ANSI_X3.4-1968
java.library.path = /usr/java/packages/lib/amd64:/usr/lib64:/lib64:/lib:/usr/lib
java.specification.name = Java Platform API Specification
java.class.version = 52.0
sun.management.compiler = HotSpot 64-Bit Tiered Compilers
os.version = 3.10.0-229.el7.x86_64
user.home = /root
user.timezone = UTC
java.awt.printerjob = sun.print.PSPrinterJob
file.encoding = ANSI_X3.4-1968
java.specification.version = 1.8
user.name = root
java.class.path = javademo-1.0.0-SNAPSHOT-jar-with-dependencies.jar
java.vm.specification.version = 1.8
sun.arch.data.model = 64
sun.java.command = com.alioo.md5.Md5demo
java.home = /root/work/jdk1.8.0_45/jre
user.language = en
java.specification.vendor = Oracle Corporation
awt.toolkit = sun.awt.X11.XToolkit
java.vm.info = mixed mode
java.version = 1.8.0_45
java.ext.dirs = /root/work/jdk1.8.0_45/jre/lib/ext:/usr/java/packages/lib/ext
sun.boot.class.path = /root/work/jdk1.8.0_45/jre/lib/resources.jar:/root/work/jdk1.8.0_45/jre/lib/rt.jar:/root/work/jdk1.8.0_45/jre/lib/sunrsasign.jar:/root/work/jdk1.8.0_45/jre/lib/jsse.jar:/root/work/jdk1.8.0_45/jre/lib/jce.jar:/root/work/jdk1.8.0_45/jre/lib/charsets.jar:/root/work/jdk1.8.0_45/jre/lib/jfr.jar:/root/work/jdk1.8.0_45/jre/classes
java.vendor = Oracle Corporation
file.separator = /
java.vendor.url.bug = http://bugreport.sun.com/bugreport/
sun.io.unicode.encoding = UnicodeLittle
sun.cpu.endian = little
sun.cpu.isalist = 

VM Flags:
Non-default VM flags: -XX:CICompilerCount=15 -XX:InitialHeapSize=2111832064 -XX:MaxHeapSize=32210157568 -XX:MaxNewSize=10736369664 -XX:MinHeapDeltaBytes=524288 -XX:NewSize=703594496 -XX:OldSize=1408237568 -XX:+UseCompressedClassPointers -XX:+UseCompressedOops -XX:+UseParallelGC 
Command line:  
```

> jvm参数讲解
尽管我们的启动命令中没有指定jvm参数，但是jvm会结合运行环境的配置对jvm参数赋予一些默认值
```
-XX:CICompilerCount=15             //最大并行编译数为15
-XX:InitialHeapSize=2111832064     //初始化heap堆大小为2G
-XX:MaxHeapSize=32210157568        //heap堆大小最大可以使用32G
-XX:MaxNewSize=10736369664         //新生代最大可以使用10G      
-XX:MinHeapDeltaBytes=524288       //           
-XX:NewSize=703594496              //    
-XX:OldSize=1408237568             //     
-XX:+UseCompressedClassPointers    //              
-XX:+UseCompressedOops             //     
-XX:+UseParallelGC                 // 
```




https://www.oracle.com/technetwork/java/javase/tech/vmoptions-jsp-140102.html
https://docs.oracle.com/javase/8/docs/technotes/tools/unix/java.html



