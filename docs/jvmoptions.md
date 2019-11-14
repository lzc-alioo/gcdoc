
jvm相关参数官方已经有了详尽的说明，由于是英文的，对于大多数程序员来说有一定的门槛，故进行整理翻译了一下。
官方文章链接：https://docs.oracle.com/javase/8/docs/technotes/tools/unix/java.html


Java HotSpot VM Options

# Launches a Java application.

## Synopsis
java [options] classname [args]

java [options] -jar filename [args]

options
Command-line options separated by spaces. See Options.

classname
The name of the class to be launched.

filename
The name of the Java Archive (JAR) file to be called. Used only with the -jar option.

args
The arguments passed to the main() method separated by spaces.

## Description
The java command starts a Java application. It does this by starting the Java Runtime Environment (JRE), loading the specified class, and calling that class's main() method. The method must be declared public and static, it must not return any value, and it must accept a String array as a parameter. The method declaration has the following form:

public static void main(String[] args)
The java command can be used to launch a JavaFX application by loading a class that either has a main() method or that extends javafx.application.Application. In the latter case, the launcher constructs an instance of the Application class, calls its init() method, and then calls the start(javafx.stage.Stage) method.

By default, the first argument that is not an option of the java command is the fully qualified name of the class to be called. If the -jar option is specified, its argument is the name of the JAR file containing class and resource files for the application. The startup class must be indicated by the Main-Class manifest header in its source code.

The JRE searches for the startup class (and other classes used by the application) in three sets of locations: the bootstrap class path, the installed extensions, and the user's class path.

Arguments after the class file name or the JAR file name are passed to the main() method.

java命令启动一个java应用程序。它通过启动Java运行时环境（JRE）、加载指定的类并调用该类的main（）方法来实现。方法必须声明为public和static，不能返回任何值，并且必须接受字符串数组作为参数。方法声明的格式如下：

public static void main(String[] args)

java命令可用于通过加载具有main（）方法或扩展JavaFX application类来启动JavaFX应用程序。在后一种情况下，启动程序构造应用程序类的实例，调用其init（）方法，然后调用start（javafx.stage.stage）方法。

默认情况下，java命令选项的第一个参数是要调用的类的全路径。如果指定了-jar选项，则其参数是包含应用程序的类和资源文件的jar文件的名称。启动类必须由jar文件中的META_INF/MANIFEST.MF Main-Class参数来指定。

JRE会在三个位置中搜索启动类（以及应用程序使用的其他类）：启动类路径、扩展类路径和用户定义的类路径。

启动命令中紧接着类的全路径或JAR文件名之后的参数会传递给类的main（）方法中。

# Options
The java command supports a wide range of options that can be divided into the following categories:

Standard Options
Non-Standard Options
Advanced Runtime Options
Advanced JIT Compiler Options
Advanced Serviceability Options
Advanced Garbage Collection Options

Standard options are guaranteed to be supported by all implementations of the Java Virtual Machine (JVM). They are used for common actions, such as checking the version of the JRE, setting the class path, enabling verbose output, and so on.
Non-standard options are general purpose options that are specific to the Java HotSpot Virtual Machine, so they are not guaranteed to be supported by all JVM implementations, and are subject to change. These options start with -X.
Advanced options are not recommended for casual use. These are developer options used for tuning specific areas of the Java HotSpot Virtual Machine operation that often have specific system requirements and may require privileged access to system configuration parameters. They are also not guaranteed to be supported by all JVM implementations, and are subject to change. Advanced options start with -XX.
To keep track of the options that were deprecated or removed in the latest release, there is a section named Deprecated and Removed Options at the end of the document.
Boolean options are used to either enable a feature that is disabled by default or disable a feature that is enabled by default. Such options do not require a parameter. Boolean -XX options are enabled using the plus sign (-XX:+OptionName) and disabled using the minus sign (-XX:-OptionName).
For options that require an argument, the argument may be separated from the option name by a space, a colon (:), or an equal sign (=), or the argument may directly follow the option (the exact syntax differs for each option). If you are expected to specify the size in bytes, you can use no suffix, or use the suffix k or K for kilobytes (KB), m or M for megabytes (MB), g or G for gigabytes (GB). For example, to set the size to 8 GB, you can specify either 8g, 8192m, 8388608k, or 8589934592 as the argument. If you are expected to specify the percentage, use a number from 0 to 1 (for example, specify 0.25 for 25%).

java命令支持多种选项，可分为以下类别：
标准选项
非标准选项
高级运行时选项
高级JIT编译器选项
高级可维护性选项
高级垃圾收集选项

Java虚拟机（JVM）的所有实现都保证支持标准选项。它们用于常见的操作，例如检查JRE的版本、设置类路径、启用详细输出等等。
非标准选项是特定于Java HotSpot虚拟机的通用选项，因此它们不能保证得到所有JVM实现的支持，并且可能会发生更改。这些选项以-X开头。
不建议使用高级选项。这些是开发人员选项，用于调整Java热点虚拟机操作的特定区域，这些区域通常具有特定的系统要求，并且可能需要对系统配置参数进行特权访问。它们也不能保证得到所有JVM实现的支持，并且可能会发生更改。高级选项从-XX开始。
为了跟踪在最新版本中已弃用或删除的选项，文档末尾有一个名为deprecated and removed options的部分。
布尔选项用于启用默认禁用的功能或禁用默认启用的功能。这样的选项不需要参数。布尔-XX选项使用加号（-XX:+OptionName）启用，使用减号（-XX:-OptionName）禁用。
对于需要参数的选项，参数可以用空格、冒号（：）或等号（=）与选项名分隔，或者参数可以直接跟在选项后面（每个选项的确切语法不同）。如果希望指定字节大小，可以不使用后缀，也可以使用后缀k或k表示千字节（KB），m或m表示兆字节（MB），g或g表示千兆字节（GB）。例如，要将大小设置为8GB，可以指定8g、8192m、8388608k或8589934592作为参数。如果希望指定百分比，请使用0到1之间的数字（例如，指定0.25作为25%）。

## Standard Options

These are the most commonly used options that are supported by all implementations of the JVM.
这些是所有JVM实现都支持的最常用选项。

### -agentlib:libname[=options]
Loads the specified native agent library. After the library name, a comma-separated list of options specific to the library can be used.

If the option -agentlib:foo is specified, then the JVM attempts to load the library named libfoo.so in the location specified by the LD_LIBRARY_PATH system variable (on OS X this variable is DYLD_LIBRARY_PATH).

The following example shows how to load the heap profiling tool (HPROF) library and get sample CPU information every 20 ms, with a stack depth of 3:

-agentlib:hprof=cpu=samples,interval=20,depth=3
The following example shows how to load the Java Debug Wire Protocol (JDWP) library and listen for the socket connection on port 8000, suspending the JVM before the main class loads:

-agentlib:jdwp=transport=dt_socket,server=y,address=8000
For more information about the native agent libraries, refer to the following:

The java.lang.instrument package description at http://docs.oracle.com/javase/8/docs/api/java/lang/instrument/package-summary.html

Agent Command Line Options in the JVM Tools Interface guide at http://docs.oracle.com/javase/8/docs/platform/jvmti/jvmti.html#starting
加载指定的本机代理库。在库名称之后，可以使用特定于库的选项的逗号分隔列表。

如果指定了-agentlib:foo选项，则JVM将尝试在LD_library_PATH系统变量指定的位置加载名为libfoo.so的库（在OS X上，此变量为DYLD_library_PATH）。

下面的示例演示如何加载堆分析工具（HPROF）库，并在堆栈深度为3的情况下每隔20毫秒获取一次CPU信息示例：
-agentlib:hprof=cpu=samples,interval=20,depth=3

下面的示例演示如何加载Java调试连线协议（JDWP）库并侦听端口8000上的套接字连接，在主类加载之前挂起JVM：
-agentlib:jdwp=transport=dt_socket,server=y,address=8000

有关本机代理库的详细信息，请参阅以下内容：
http://docs.oracle.com/javase/8/docs/api/java/lang/instrument/package-summary.html上的java.lang.instrument包说明

JVM工具界面指南中的代理命令行选项，网址为http://docs.oracle.com/javase/8/docs/platform/jvmti/jvmti.html


### -agentpath:pathname[=options]
Loads the native agent library specified by the absolute path name. This option is equivalent to -agentlib but uses the full path and file name of the library.
加载由绝对路径名指定的本机代理库。此选项相当于-agentlib，但使用库的完整路径和文件名。

-client
Selects the Java HotSpot Client VM. The 64-bit version of the Java SE Development Kit (JDK) currently ignores this option and instead uses the Server JVM.

For default JVM selection, see Server-Class Machine Detection at
http://docs.oracle.com/javase/8/docs/technotes/guides/vm/server-class.html
选择 Java HotSpot Client VM.。64位版本的Java SE开发工具包（JDK）目前忽略了这个选项，直接使用sever模式。
有关默认的JVM选择，请参阅 http://docs.oracle.com/javase/8/docs/technotes/guides/vm/server-class.html

### -Dproperty=value
Sets a system property value. The property variable is a string with no spaces that represents the name of the property. The value variable is a string that represents the value of the property. If value is a string with spaces, then enclose it in quotation marks (for example -Dfoo="foo bar").
设置系统属性值。属性变量是一个字符串，没有表示属性名称的空格。值变量是表示属性值的字符串。如果值是带空格的字符串，则将其括在引号中（例如-Dfoo=“foo bar”）。

### -d32
Runs the application in a 32-bit environment. If a 32-bit environment is not installed or is not supported, then an error will be reported. By default, the application is run in a 32-bit environment unless a 64-bit system is used.
在32位环境中运行应用程序。如果未安装或不支持32位环境，则将报告错误。默认情况下，应用程序在32位环境中运行，除非使用64位系统。

### -d64
Runs the application in a 64-bit environment. If a 64-bit environment is not installed or is not supported, then an error will be reported. By default, the application is run in a 32-bit environment unless a 64-bit system is used.
Currently only the Java HotSpot Server VM supports 64-bit operation, and the -server option is implicit with the use of -d64. The -client option is ignored with the use of -d64. This is subject to change in a future release.
在64位环境中运行应用程序。如果未安装或不支持64位环境，则将报告错误。默认情况下，应用程序在32位环境中运行，除非使用64位系统。
目前只有Java HotSpot Server虚拟机支持64位操作，-server选项在使用-d64时是隐式的。使用-d64将忽略-client选项。这将在以后的版本中进行更改。

###-disableassertions[:[packagename]...|:classname]
### -da[:[packagename]...|:classname]
Disables assertions. By default, assertions are disabled in all packages and classes.
With no arguments, -disableassertions (-da) disables assertions in all packages and classes. With the packagename argument ending in ..., the switch disables assertions in the specified package and any subpackages. If the argument is simply ..., then the switch disables assertions in the unnamed package in the current working directory. With the classname argument, the switch disables assertions in the specified class.
The -disableassertions (-da) option applies to all class loaders and to system classes (which do not have a class loader). There is one exception to this rule: if the option is provided with no arguments, then it does not apply to system classes. This makes it easy to disable assertions in all classes except for system classes. The -disablesystemassertions option enables you to disable assertions in all system classes.
To explicitly enable assertions in specific packages or classes, use the -enableassertions (-ea) option. Both options can be used at the same time. For example, to run the MyClass application with assertions enabled in package com.wombat.fruitbat (and any subpackages) but disabled in class com.wombat.fruitbat.Brickbat, use the following command:
```java -ea:com.wombat.fruitbat... -da:com.wombat.fruitbat.Brickbat MyClass```
禁用断言。默认情况下，在所有包和类中都禁用断言。
不带参数，-disableassertions（-da）禁用所有包和类中的断言。packagename参数以…结尾时，开关将禁用指定包和任何子包中的断言。如果参数只是…，则开关将禁用当前工作目录中未命名包中的断言。使用classname参数，开关将禁用指定类中的断言。
-disableassertions（-da）选项适用于所有类装入器和系统类（它们没有类装入器）。这个规则有一个例外：如果选项没有参数，那么它不适用于系统类。这使得在除了系统类之外的所有类中禁用断言变得很容易。使用-disable system assertions选项可以禁用所有系统类中的断言。
要显式启用特定包或类中的断言，请使用-enablessertions（-ea）选项。两个选项都可以同时使用。例如，要在包com.wombat.ruitbat（和任何子包）中启用断言但在类com.wombat.ruitbat.Brickbat中禁用断言的情况下运行MyClass应用程序，请使用以下命令：

```java -ea:com.wombat.fruitbat... -da:com.wombat.fruitbat.Brickbat MyClass```

### -disablesystemassertions
### -dsa
Disables assertions in all system classes.
在所有系统类中禁用断言。

### -enableassertions[:[packagename]...|:classname]
### -ea[:[packagename]...|:classname]
Enables assertions. By default, assertions are disabled in all packages and classes.
With no arguments, -enableassertions (-ea) enables assertions in all packages and classes. With the packagename argument ending in ..., the switch enables assertions in the specified package and any subpackages. If the argument is simply ..., then the switch enables assertions in the unnamed package in the current working directory. With the classname argument, the switch enables assertions in the specified class.
The -enableassertions (-ea) option applies to all class loaders and to system classes (which do not have a class loader). There is one exception to this rule: if the option is provided with no arguments, then it does not apply to system classes. This makes it easy to enable assertions in all classes except for system classes. The -enablesystemassertions option provides a separate switch to enable assertions in all system classes.
To explicitly disable assertions in specific packages or classes, use the -disableassertions (-da) option. If a single command contains multiple instances of these switches, then they are processed in order before loading any classes. For example, to run the MyClass application with assertions enabled only in package com.wombat.fruitbat (and any subpackages) but disabled in class com.wombat.fruitbat.Brickbat, use the following command:
```java -ea:com.wombat.fruitbat... -da:com.wombat.fruitbat.Brickbat MyClass```
启用断言。默认情况下，在所有包和类中都禁用断言。
不带参数，-enablessertions（-ea）在所有包和类中启用断言。packagename参数以…结尾时，开关启用指定包和任何子包中的断言。如果参数是简单的…，那么开关将启用当前工作目录中未命名包中的断言。使用classname参数，开关启用指定类中的断言。
-enablessertions（-ea）选项适用于所有类装入器和系统类（它们没有类装入器）。这个规则有一个例外：如果选项没有参数，那么它不适用于系统类。这使得在除系统类之外的所有类中启用断言变得容易。-enablesystemassertions选项提供了一个单独的开关，用于在所有系统类中启用断言。
要显式禁用特定包或类中的断言，请使用-disable assertions（-da）选项。如果一个命令包含这些开关的多个实例，则在加载任何类之前，将按顺序对它们进行处理。例如，要在包com.wombat.ruitbat（和任何子包）中启用断言但在类com.wombat.ruitbat.Brickbat中禁用断言的情况下运行MyClass应用程序，请使用以下命令：
```java -ea:com.wombat.fruitbat... -da:com.wombat.fruitbat.Brickbat MyClass```

### -enablesystemassertions
### -esa
Enables assertions in all system classes.
在所有系统类中启用断言。

### -help
### -?
Displays usage information for the java command without actually running the JVM.

### -jar filename
Executes a program encapsulated in a JAR file. The filename argument is the name of a JAR file with a manifest that contains a line in the form Main-Class:classname that defines the class with the public static void main(String[] args) method that serves as your application's starting point.
When you use the -jar option, the specified JAR file is the source of all user classes, and other class path settings are ignored.
For more information about JAR files, see the following resources:

jar(1)
The Java Archive (JAR) Files guide at http://docs.oracle.com/javase/8/docs/technotes/guides/jar/index.html
Lesson: Packaging Programs in JAR Files at http://docs.oracle.com/javase/tutorial/deployment/jar/index.html
执行封装在JAR文件中的程序。file name参数是具有清单的JAR文件的名称，清单中包含Main Class:classname形式的行，该行使用作为应用程序起点的public static void Main（String[]args）方法定义类。
使用-jar选项时，指定的jar文件是所有用户类的源，其他类路径设置将被忽略。
有关JAR文件的更多信息，请参阅以下参考资料：
- jar(1) https://docs.oracle.com/javase/8/docs/technotes/tools/unix/jar.html#BGBEJEEG
- Java Archive（JAR）文件指南，网址：http://docs.oracle.com/javase/8/docs/technotes/guides/JAR/index.html
- Lesson: Packaging Programs in JAR Files at http://docs.oracle.com/javase/tutorial/deployment/jar/index.html

### -javaagent:jarpath[=options]
Loads the specified Java programming language agent. For more information about instrumenting Java applications, see the java.lang.instrument package description in the Java API documentation at http://docs.oracle.com/javase/8/docs/api/java/lang/instrument/package-summary.html
加载指定的Java编程语言代理。有关检测Java应用程序的更多信息，请参阅Java API文档中的Java.lang.instrument包说明，网址为http://docs.oracle.com/javase/8/docs/API/Java/lang/instrument/package-summary.html

### -jre-restrict-search
Includes user-private JREs in the version search.

### -no-jre-restrict-search
Excludes user-private JREs from the version search.

### -server
Selects the Java HotSpot Server VM. The 64-bit version of the JDK supports only the Server VM, so in that case the option is implicit.
64位版本的JDK只支持-server模式，因此在这种情况下，该选项是隐式设置的。

For default JVM selection, see Server-Class Machine Detection at
http://docs.oracle.com/javase/8/docs/technotes/guides/vm/server-class.html

### -showversion
Displays version information and continues execution of the application. This option is equivalent to the -version option except that the latter instructs the JVM to exit after displaying version information.
显示版本信息并继续执行应用程序。此选项等效于-version选项，只不过-version显示版本信息之后退出。

### -splash:imgname
Shows the splash screen with the image specified by imgname. For example, to show the splash.gif file from the images directory when starting your application, use the following option:
显示由imgname指定的图像的启动屏幕。例如，要在启动应用程序时显示images目录中的splash.gif文件，请使用以下选项：

### -splash:images/splash.gif
-verbose:class
Displays information about each loaded class.

-verbose:gc
Displays information about each garbage collection (GC) event.

-verbose:jni
Displays information about the use of native methods and other Java Native Interface (JNI) activity.

-version
Displays version information and then exits. This option is equivalent to the -showversion option except that the latter does not instruct the JVM to exit after displaying version information.

-version:release
Specifies the release version to be used for running the application. If the version of the java command called does not meet this specification and an appropriate implementation is found on the system, then the appropriate implementation will be used.

The release argument specifies either the exact version string, or a list of version strings and ranges separated by spaces. A version string is the developer designation of the version number in the following form: 1.x.0_u (where x is the major version number, and u is the update version number). A version range is made up of a version string followed by a plus sign (+) to designate this version or later, or a part of a version string followed by an asterisk (*) to designate any version string with a matching prefix. Version strings and ranges can be combined using a space for a logical OR combination, or an ampersand (&) for a logical AND combination of two version strings/ranges. For example, if running the class or JAR file requires either JRE 6u13 (1.6.0_13), or any JRE 6 starting from 6u10 (1.6.0_10), specify the following:

-version:"1.6.0_13 1.6* & 1.6.0_10+"
Quotation marks are necessary only if there are spaces in the release parameter.

For JAR files, the preference is to specify version requirements in the JAR file manifest rather than on the command line.





-agentlib:libname[=options]

 
-agentpath:pathname[=options]

-client


-Dproperty=value


-d32

-d64
在64位环境中运行应用程序。如果未安装或不支持64位环境，则将报告错误。默认情况下，应用程序在32位环境中运行，除非使用64位系统。
目前只有Java HotSpot Server虚拟机支持64位操作，-server选项在使用-d64时是隐式的。使用-d64将忽略-client选项。这将在以后的版本中进行更改。



-disableassertions[:[packagename]...|:classname]
-da[:[packagename]...|:classname]

禁用断言。默认情况下，在所有包和类中都禁用断言。

不带参数，-disableassertions（-da）禁用所有包和类中的断言。packagename参数以…结尾时，开关将禁用指定包和任何子包中的断言。如果参数只是…，则开关将禁用当前工作目录中未命名包中的断言。使用classname参数，开关将禁用指定类中的断言。

-disableassertions（-da）选项适用于所有类装入器和系统类（它们没有类装入器）。这个规则有一个例外：如果选项没有参数，那么它不适用于系统类。这使得在除了系统类之外的所有类中禁用断言变得很容易。使用-disable system assertions选项可以禁用所有系统类中的断言。

要显式启用特定包或类中的断言，请使用-enablessertions（-ea）选项。两个选项都可以同时使用。例如，要在包com.wombat.ruitbat（和任何子包）中启用断言但在类com.wombat.ruitbat.Brickbat中禁用断言的情况下运行MyClass应用程序，请使用以下命令：

java -ea:com.wombat.fruitbat... -da:com.wombat.fruitbat.Brickbat MyClass


-enablesystemassertions
-esa
在所有系统类中启用断言。


-help
-?
在不实际运行JVM的情况下显示java命令的使用信息。


-jar filename


-javaagent:jarpath[=options]

加载指定的Java编程语言代理。有关检测Java应用程序的更多信息，请参阅Java API文档中的Java.lang.instrument包说明，网址为http://docs.oracle.com/javase/8/docs/API/Java/lang/instrument/package-summary.html


-jre-restrict-search
在版本搜索中包含用户专用JRE。


-no-jre-restrict-search
从版本搜索中排除用户专用JRE。


-server
选择Java热点服务器虚拟机。64位版本的JDK只支持服务器VM，因此在这种情况下，该选项是隐式的。



有关默认的JVM选择，请参阅

http://docs.oracle.com/javase/8/docs/technotes/guides/vm/server-class.html



-显示版本

显示版本信息并继续执行应用程序。此选项等效于--版本选项，除了后者指示JVM在显示版本信息之后退出。



-飞溅：imgname

显示由imgname指定的图像的启动屏幕。例如，要在启动应用程序时显示images目录中的splash.gif文件，请使用以下选项：



-飞溅：images/splash.gif

-详细：类

显示有关每个加载类的信息。



-详细：gc

显示有关每个垃圾收集（GC）事件的信息。



-详细：jni

显示有关使用本机方法和其他Java本机接口（JNI）活动的信息。



-版本

显示版本信息，然后退出。此选项相当于-SuffEdio选项，除了后者不指示JVM在显示版本信息之后退出。



-版本：发布

指定用于运行应用程序的版本。如果调用的java命令的版本不符合此规范，并且在系统上找到了适当的实现，则将使用适当的实现。



release参数指定精确的版本字符串，或由空格分隔的版本字符串和范围列表。版本字符串是开发人员对版本号的指定，格式如下：1.x.0_（其中x是主要版本号，u是更新版本号）。版本范围由版本字符串后跟加号（＋）来指定此版本或更高版本，或由版本字符串的一部分后跟星号（*）来指定具有匹配前缀的任何版本字符串组成。版本字符串和范围可以使用空格来表示逻辑或组合，或者使用与号（&）来表示两个版本字符串/范围的逻辑和组合。例如，如果运行类或JAR文件需要JRE 6u13（1.6.0_13）或任何从6u10（1.6.0_10）开始的JRE 6，请指定以下内容：



-版本：“1.6.0_13 1.6*&1.6.0_10+”

只有当release参数中有空格时，引号才是必需的。



对于JAR文件，首选项是在JAR文件清单中而不是在命令行中指定版本要求。