
jvm相关参数官方已经有了详尽的说明，由于是英文的，对于大多数程序员来说有一定的门槛，故进行整理翻译了一下。
官方文章链接：https://docs.oracle.com/javase/8/docs/technotes/tools/unix/java.html


Java HotSpot VM Options

# Launches a Java application.

## Synopsis  简介
java [options] classname [args]
java [options] -jar filename [args]
- options  Command-line options separated by spaces. See Options. 选项命令行选项用空格分隔。请参见选项
- classname  The name of the class to be launched.  要启动的类的名称。
- filename  The name of the Java Archive (JAR) file to be called. Used only with the -jar option.  要调用的Java存档（JAR）文件的名称。仅与-jar选项一起使用。
- args  The arguments passed to the main() method separated by spaces.  传递给main（）方法的参数，用空格分隔。

## Description
The java command starts a Java application. It does this by starting the Java Runtime Environment (JRE), loading the specified class, and calling that class's main() method. The method must be declared public and static, it must not return any value, and it must accept a String array as a parameter. The method declaration has the following form:
java命令启动一个java应用程序。它通过启动Java运行时环境（JRE）、加载指定的类并调用该类的main（）方法来实现。方法必须声明为public和static，不能返回任何值，并且必须接受字符串数组作为参数。方法声明的格式如下：

```public static void main(String[] args)```

The java command can be used to launch a JavaFX application by loading a class that either has a main() method or that extends javafx.application.Application. In the latter case, the launcher constructs an instance of the Application class, calls its init() method, and then calls the start(javafx.stage.Stage) method.
java命令可用于通过加载具有main（）方法或扩展JavaFX application类来启动JavaFX应用程序。在后一种情况下，启动程序构造应用程序类的实例，调用其init（）方法，然后调用start（javafx.stage.stage）方法。

By default, the first argument that is not an option of the java command is the fully qualified name of the class to be called. If the -jar option is specified, its argument is the name of the JAR file containing class and resource files for the application. The startup class must be indicated by the Main-Class manifest header in its source code.
默认情况下，java命令选项的第一个参数是要调用的类的全路径。如果指定了-jar选项，则其参数是包含应用程序的类和资源文件的jar文件的名称。启动类必须由jar文件中的META_INF/MANIFEST.MF Main-Class参数来指定。

The JRE searches for the startup class (and other classes used by the application) in three sets of locations: the bootstrap class path, the installed extensions, and the user's class path.
JRE会在三个位置中搜索启动类（以及应用程序使用的其他类）：启动类路径、扩展类路径和用户定义的类路径。

Arguments after the class file name or the JAR file name are passed to the main() method.
启动命令中紧接着类的全路径或JAR文件名之后的参数会传递给类的main（）方法中。

# Options
The java command supports a wide range of options that can be divided into the following categories:
java命令支持多种选项，可分为以下类别：

Standard Options   标准选项
- Non-Standard Options   非标准选项
- Advanced Runtime Options  高级运行时选项
- Advanced JIT Compiler Options   高级JIT编译器选项
- Advanced Serviceability Options   高级可维护性选项
- Advanced Garbage Collection Options    高级垃圾收集选项

Standard options are guaranteed to be supported by all implementations of the Java Virtual Machine (JVM). They are used for common actions, such as checking the version of the JRE, setting the class path, enabling verbose output, and so on.
Java虚拟机（JVM）的所有实现都保证支持标准选项。它们用于常见的操作，例如检查JRE的版本、设置类路径、启用详细输出等等。

Non-standard options are general purpose options that are specific to the Java HotSpot Virtual Machine, so they are not guaranteed to be supported by all JVM implementations, and are subject to change. These options start with -X.
非标准选项是特定于Java HotSpot虚拟机的通用选项，因此它们不能保证得到所有JVM实现的支持，并且可能会发生更改。这些选项以-X开头。

Advanced options are not recommended for casual use. These are developer options used for tuning specific areas of the Java HotSpot Virtual Machine operation that often have specific system requirements and may require privileged access to system configuration parameters. They are also not guaranteed to be supported by all JVM implementations, and are subject to change. Advanced options start with -XX.
不建议使用高级选项。这些是开发人员选项，用于调整Java热点虚拟机操作的特定区域，这些区域通常具有特定的系统要求，并且可能需要对系统配置参数进行特权访问。它们也不能保证得到所有JVM实现的支持，并且可能会发生更改。高级选项从-XX开始。

To keep track of the options that were deprecated or removed in the latest release, there is a section named Deprecated and Removed Options at the end of the document.
为了跟踪在最新版本中已弃用或删除的选项，文档末尾有一个名为deprecated and removed options的部分。

Boolean options are used to either enable a feature that is disabled by default or disable a feature that is enabled by default. Such options do not require a parameter. Boolean -XX options are enabled using the plus sign (-XX:+OptionName) and disabled using the minus sign (-XX:-OptionName).
布尔选项用于启用默认禁用的功能或禁用默认启用的功能。这样的选项不需要参数。布尔-XX选项使用加号（-XX:+OptionName）启用，使用减号（-XX:-OptionName）禁用。

For options that require an argument, the argument may be separated from the option name by a space, a colon (:), or an equal sign (=), or the argument may directly follow the option (the exact syntax differs for each option). If you are expected to specify the size in bytes, you can use no suffix, or use the suffix k or K for kilobytes (KB), m or M for megabytes (MB), g or G for gigabytes (GB). For example, to set the size to 8 GB, you can specify either 8g, 8192m, 8388608k, or 8589934592 as the argument. If you are expected to specify the percentage, use a number from 0 to 1 (for example, specify 0.25 for 25%).
对于需要参数的选项，参数可以用空格、冒号（：）或等号（=）与选项名分隔，或者参数可以直接跟在选项后面（每个选项的确切语法不同）。如果希望指定字节大小，可以不使用后缀，也可以使用后缀k或k表示千字节（KB），m或m表示兆字节（MB），g或g表示千兆字节（GB）。例如，要将大小设置为8GB，可以指定8g、8192m、8388608k或8589934592作为参数。如果希望指定百分比，请使用0到1之间的数字（例如，指定0.25作为25%）。

---
## Standard Options

These are the most commonly used options that are supported by all implementations of the JVM.
这些是所有JVM实现都支持的最常用选项。

### -agentlib:libname[=options]
Loads the specified native agent library. After the library name, a comma-separated list of options specific to the library can be used.
加载指定的本机代理库。在库名称之后，可以使用特定于库的选项的逗号分隔列表。

If the option -agentlib:foo is specified, then the JVM attempts to load the library named libfoo.so in the location specified by the LD_LIBRARY_PATH system variable (on OS X this variable is DYLD_LIBRARY_PATH).
如果指定了-agentlib:foo选项，则JVM将尝试在LD_library_PATH系统变量指定的位置加载名为libfoo.so的库（在OS X上，此变量为DYLD_library_PATH）。

The following example shows how to load the heap profiling tool (HPROF) library and get sample CPU information every 20 ms, with a stack depth of 3:
下面的示例演示如何加载堆分析工具（HPROF）库，并在堆栈深度为3的情况下每隔20毫秒获取一次CPU信息示例：
```-agentlib:hprof=cpu=samples,interval=20,depth=3```

The following example shows how to load the Java Debug Wire Protocol (JDWP) library and listen for the socket connection on port 8000, suspending the JVM before the main class loads:
下面的示例演示如何加载Java调试连线协议（JDWP）库并侦听端口8000上的套接字连接，在主类加载之前挂起JVM：
```-agentlib:jdwp=transport=dt_socket,server=y,address=8000```

For more information about the native agent libraries, refer to the following:
有关本机代理库的详细信息，请参阅以下内容：
The java.lang.instrument package description at http://docs.oracle.com/javase/8/docs/api/java/lang/instrument/package-summary.html

JVM工具接口指南中的代理命令行选项，网址为http://docs.oracle.com/javase/8/docs/platform/jvmti/jvmti.html
Agent Command Line Options in the JVM Tools Interface guide at http://docs.oracle.com/javase/8/docs/platform/jvmti/jvmti.html#starting

### -agentpath:pathname[=options]
Loads the native agent library specified by the absolute path name. This option is equivalent to -agentlib but uses the full path and file name of the library.
加载由绝对路径名指定的本机代理库。此选项相当于-agentlib，但使用库的完整路径和文件名。

-client
Selects the Java HotSpot Client VM. The 64-bit version of the Java SE Development Kit (JDK) currently ignores this option and instead uses the Server JVM.
选择 Java HotSpot Client VM.。64位版本的Java SE开发工具包（JDK）目前忽略了这个选项，直接使用sever模式。

For default JVM selection, see Server-Class Machine Detection at
http://docs.oracle.com/javase/8/docs/technotes/guides/vm/server-class.html
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

### -verbose:gc
Displays information about each garbage collection (GC) event.
显示有关每个垃圾收集（GC）事件的信息。

### -verbose:jni
Displays information about the use of native methods and other Java Native Interface (JNI) activity.
显示有关使用本机方法和其他Java本机接口（JNI）活动的信息。

### -version
Displays version information and then exits. This option is equivalent to the -showversion option except that the latter does not instruct the JVM to exit after displaying version information.
显示版本信息，然后退出。此选项相当于-showversion选项，只不过后者显示版本信息之后并不退出。

### -version:release
Specifies the release version to be used for running the application. If the version of the java command called does not meet this specification and an appropriate implementation is found on the system, then the appropriate implementation will be used.
The release argument specifies either the exact version string, or a list of version strings and ranges separated by spaces. A version string is the developer designation of the version number in the following form: 1.x.0_u (where x is the major version number, and u is the update version number). A version range is made up of a version string followed by a plus sign (+) to designate this version or later, or a part of a version string followed by an asterisk (*) to designate any version string with a matching prefix. Version strings and ranges can be combined using a space for a logical OR combination, or an ampersand (&) for a logical AND combination of two version strings/ranges. For example, if running the class or JAR file requires either JRE 6u13 (1.6.0_13), or any JRE 6 starting from 6u10 (1.6.0_10), specify the following:
指定用于运行应用程序的版本。如果调用的java命令的版本不符合此规范，并且在系统上找到了适当的实现，则将使用适当的实现。
release参数指定精确的版本字符串，或由空格分隔的版本字符串和范围列表。版本字符串是开发人员对版本号的指定，格式如下：1.x.0_（其中x是主要版本号，u是更新版本号）。版本范围由版本字符串后跟加号（＋）来指定此版本或更高版本，或由版本字符串的一部分后跟星号（*）来指定具有匹配前缀的任何版本字符串组成。版本字符串和范围可以使用空格来表示逻辑或组合，或者使用与号（&）来表示两个版本字符串/范围的逻辑和组合。例如，如果运行类或JAR文件需要JRE 6u13（1.6.0_13）或任何从6u10（1.6.0_10）开始的JRE 6，请指定以下内容：

 ```-version:"1.6.0_13 1.6* & 1.6.0_10+"```

Quotation marks are necessary only if there are spaces in the release parameter.
只有当release参数中有空格时，引号才是必需的。

For JAR files, the preference is to specify version requirements in the JAR file manifest rather than on the command line.
对于JAR文件，首选项是在JAR文件清单中而不是在命令行中指定版本要求。

---
## Non-Standard Options  非标准选项
                      
These options are general purpose options that are specific to the Java HotSpot Virtual Machine.
这些选项是特定于Java热点虚拟机的通用选项。

### -X
Displays help for all available -X options.
显示所有可用-X选项的说明。

### -Xbatch
Disables background compilation. By default, the JVM compiles the method as a background task, running the method in interpreter mode until the background compilation is finished. The -Xbatch flag disables background compilation so that compilation of all methods proceeds as a foreground task until completed.
禁用后台编译。默认情况下，JVM将该方法编译为后台任务，在解释器模式下运行该方法，直到后台编译完成。-Xbatch标志禁用后台编译，以便所有方法的编译作为前台任务进行，直到完成为止。

This option is equivalent to -XX:-BackgroundCompilation.
此选项相当于-XX:-BackgroundCompilation。

### -Xbootclasspath:path
Specifies a list of directories, JAR files, and ZIP archives separated by colons (:) to search for boot class files. These are used in place of the boot class files included in the JDK.
指定用冒号（：）分隔的目录、JAR文件和ZIP存档的列表，以搜索引导类文件。这些文件用于代替JDK中包含的引导类文件。

Do not deploy applications that use this option to override a class in rt.jar, because this violates the JRE binary code license.
不要部署使用此选项重写rt.jar中的类的应用程序，因为这违反了JRE二进制代码许可证。

### -Xbootclasspath/a:path
Specifies a list of directories, JAR files, and ZIP archives separated by colons (:) to append to the end of the default bootstrap class path.
指定要附加到默认引导类路径末尾的目录、JAR文件和以冒号（：）分隔的ZIP存档的列表。

Do not deploy applications that use this option to override a class in rt.jar, because this violates the JRE binary code license.
不要部署使用此选项重写rt.jar中的类的应用程序，因为这违反了JRE二进制代码许可证。

### -Xbootclasspath/p:path
Specifies a list of directories, JAR files, and ZIP archives separated by colons (:) to prepend to the front of the default bootstrap class path.
指定要附加到默认引导类路径前面的目录、JAR文件和以冒号（：）分隔的ZIP存档的列表。

Do not deploy applications that use this option to override a class in rt.jar, because this violates the JRE binary code license.

### -Xcheck:jni
Performs additional checks for Java Native Interface (JNI) functions. Specifically, it validates the parameters passed to the JNI function and the runtime environment data before processing the JNI request. Any invalid data encountered indicates a problem in the native code, and the JVM will terminate with an irrecoverable error in such cases. Expect a performance degradation when this option is used.
对Java本机接口（JNI）函数执行附加检查。具体来说，它在处理JNI请求之前验证传递给JNI函数的参数和运行时环境数据。遇到的任何无效数据都表示本机代码有问题，在这种情况下，JVM将以不可恢复的错误终止。使用此选项时，预期性能会降低。

### -Xcomp
Forces compilation of methods on first invocation. By default, the Client VM (-client) performs 1,000 interpreted method invocations and the Server VM (-server) performs 10,000 interpreted method invocations to gather information for efficient compilation. Specifying the -Xcomp option disables interpreted method invocations to increase compilation performance at the expense of efficiency.
在第一次调用时强制编译方法。默认情况下，客户端VM（-Client）执行1000个解释方法调用，服务器VM（-Server）执行10000个解释方法调用，以收集有效编译所需的信息。指定-Xcomp选项将禁用解释方法调用以提高编译性能，但会降低效率。

You can also change the number of interpreted method invocations before compilation using the -XX:CompileThreshold option.
还可以在编译之前使用-XX:CompileThreshold选项更改解释方法调用的次数。

### -Xdebug
Does nothing. Provided for backward compatibility.
什么都不做。提供向后兼容性。

### -Xdiag
Shows additional diagnostic messages.
显示其他诊断信息。

### -Xfuture
Enables strict class-file format checks that enforce close conformance to the class-file format specification. Developers are encouraged to use this flag when developing new code because the stricter checks will become the default in future releases.
启用严格的类文件格式检查，以强制严格遵守类文件格式规范。鼓励开发人员在开发新代码时使用此标志，因为在将来的版本中，更严格的检查将成为默认检查。

### -Xint
Runs the application in interpreted-only mode. Compilation to native code is disabled, and all bytecode is executed by the interpreter. The performance benefits offered by the just in time (JIT) compiler are not present in this mode.
以仅解释模式运行应用程序。对本机代码的编译被禁用，所有字节码都由解释器执行。（JIT）即时编译器提供的性能优势在此模式中不存在。

### -Xinternalversion
Displays more detailed JVM version information than the -version option, and then exits.
显示比“版本”选项更详细的JVM版本信息，然后退出。

### -Xloggc:filename
Sets the file to which verbose GC events information should be redirected for logging. The information written to this file is similar to the output of -verbose:gc with the time elapsed since the first GC event preceding each logged event. The -Xloggc option overrides -verbose:gc if both are given with the same java command.
设置要将详细GC事件信息重定向到其中进行日志记录的文件。写入此文件的信息类似于-verbose:gc的输出，其中包含自每个记录的事件之前的第一个gc事件以来经过的时间。-Xloggc选项重写-verbose:gc，如果这两个选项都是用同一个java命令给出的。

Example:
-Xloggc:garbage-collection.log
-Xmaxjitcodesize=size
Specifies the maximum code cache size (in bytes) for JIT-compiled code. Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes. The default maximum code cache size is 240 MB; if you disable tiered compilation with the option -XX:-TieredCompilation, then the default size is 48 MB:
指定JIT编译代码的最大代码缓存大小（以字节为单位）。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。默认最大代码缓存大小为240 MB；如果禁用选项-XX:-TiErdEd汇编的分层编译，则默认大小为48 MB：

### -Xmaxjitcodesize=240m
This option is equivalent to -XX:ReservedCodeCacheSize.
此选项相当于-XX:ReservedCodeCacheSize。

### -Xmixed
Executes all bytecode by the interpreter except for hot methods, which are compiled to native code.
由解释器执行所有字节码，但编译为本机代码的热方法除外。

### -Xmnsize
Sets the initial and maximum size (in bytes) of the heap for the young generation (nursery). Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes.
指定年青代大小（以字节为单位）。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。

The young generation region of the heap is used for new objects. GC is performed in this region more often than in other regions. If the size for the young generation is too small, then a lot of minor garbage collections will be performed. If the size is too large, then only full garbage collections will be performed, which can take a long time to complete. Oracle recommends that you keep the size for the young generation between a half and a quarter of the overall heap size.
堆的年轻一代区域用于新对象。GC在这个区域的执行频率高于其他区域。如果年轻一代的大小太小，那么将执行许多小的垃圾收集。如果大小太大，则只执行完整的垃圾回收，这可能需要很长时间才能完成。Oracle建议您将年轻一代的大小保持在整个堆大小的一半到四分之一之间。

The following examples show how to set the initial and maximum size of young generation to 256 MB using various units:
下面的示例演示如何使用各种单元将初始一代和最大大小的年轻一代设置为256 MB：

-Xmn256m
-Xmn262144k
-Xmn268435456
Instead of the -Xmn option to set both the initial and maximum size of the heap for the young generation, you can use -XX:NewSize to set the initial size and -XX:MaxNewSize to set the maximum size.
代替Xmn选项来设置年轻一代堆的初始大小和最大大小，可以使用-x:NeWestSead来设置初始大小和-XX:Max NeWSIZE来设置最大大小。

### -Xmssize
Sets the initial size (in bytes) of the heap. This value must be a multiple of 1024 and greater than 1 MB. Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes.
设置堆的初始大小（字节）。此值必须是1024的倍数且大于1 MB。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。

The following examples show how to set the size of allocated memory to 6 MB using various units:

-Xms6291456
-Xms6144k
-Xms6m
If you do not set this option, then the initial size will be set as the sum of the sizes allocated for the old generation and the young generation. The initial size of the heap for the young generation can be set using the -Xmn option or the -XX:NewSize option.

-Xmxsize
Specifies the maximum size (in bytes) of the memory allocation pool in bytes. This value must be a multiple of 1024 and greater than 2 MB. Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes. The default value is chosen at runtime based on system configuration. For server deployments, -Xms and -Xmx are often set to the same value. See the section "Ergonomics" in Java SE HotSpot Virtual Machine Garbage Collection Tuning Guide at http://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/index.html.
以字节为单位指定内存分配池的最大大小（以字节为单位）。此值必须是1024的倍数且大于2 MB。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。默认值在运行时根据系统配置选择。对于服务器部署，-Xms和-Xmx通常设置为相同的值。请参阅http://docs.oracle.com/Java SE/8/docs/technotes/guides/vm/gctuning/index.html上Java SE HotSpot虚拟机垃圾收集优化指南中的“人体工程学”部分。

The following examples show how to set the maximum allowed size of allocated memory to 80 MB using various units:

-Xmx83886080
-Xmx81920k
-Xmx80m
The -Xmx option is equivalent to -XX:MaxHeapSize.

### -Xnoclassgc
Disables garbage collection (GC) of classes. This can save some GC time, which shortens interruptions during the application run.
禁用类的垃圾收集（GC）。这可以节省一些GC时间，从而缩短应用程序运行期间的中断。

When you specify -Xnoclassgc at startup, the class objects in the application will be left untouched during GC and will always be considered live. This can result in more memory being permanently occupied which, if not used carefully, will throw an out of memory exception.
当您在启动时指定-Xnoclassgc时，应用程序中的类对象将在GC期间保持不变，并且将始终被视为活动的。这会导致更多的内存被永久占用，如果不小心使用，将抛出内存不足异常。


### -Xprof
Profiles the running program and sends profiling data to standard output. This option is provided as a utility that is useful in program development and is not intended to be used in production systems.
分析正在运行的程序并将分析数据发送到标准输出。此选项是作为一个实用程序提供的，在程序开发中很有用，不打算在生产系统中使用。

### -Xrs
Reduces the use of operating system signals by the JVM.
减少了JVM对操作系统信号的使用。

Shutdown hooks enable orderly shutdown of a Java application by running user cleanup code (such as closing database connections) at shutdown, even if the JVM terminates abruptly.
关闭挂钩通过在关闭时运行用户清理代码（例如关闭数据库连接）来实现Java应用程序的有序关闭，即使JVM突然终止。

The JVM catches signals to implement shutdown hooks for unexpected termination. The JVM uses SIGHUP, SIGINT, and SIGTERM to initiate the running of shutdown hooks.
JVM捕获信号以实现意外终止的关闭挂钩。JVM使用SIGHUP、SIGINT和SIGTERM启动关闭挂钩的运行。

The JVM uses a similar mechanism to implement the feature of dumping thread stacks for debugging purposes. The JVM uses SIGQUIT to perform thread dumps.
JVM使用类似的机制来实现转储线程堆栈以进行调试的功能。JVM使用SIGQUIT来执行线程转储。

Applications embedding the JVM frequently need to trap signals such as SIGINT or SIGTERM, which can lead to interference with the JVM signal handlers. The -Xrs option is available to address this issue. When -Xrs is used, the signal masks for SIGINT, SIGTERM, SIGHUP, and SIGQUIT are not changed by the JVM, and signal handlers for these signals are not installed.
嵌入JVM的应用程序经常需要捕获SIGINT或SIGTERM等信号，这可能会导致对JVM信号处理程序的干扰。可以使用-Xrs选项来解决此问题。使用-Xrs时，JVM不会更改SIGINT、SIGTERM、SIGHUP和SIGQUIT的信号掩码，也不会安装这些信号的信号处理程序。

There are two consequences of specifying -Xrs:
指定-Xrs有两个结果：

SIGQUIT thread dumps are not available.
SIGQUIT线程转储不可用。

User code is responsible for causing shutdown hooks to run, for example, by calling System.exit() when the JVM is to be terminated.
当JVM将被终止时，用户代码负责导致关闭钩子运行，例如，通过调用 System.exit() 调用。

### -Xshare:mode
Sets the class data sharing (CDS) mode. Possible mode arguments for this option include the following:
设置类数据共享（CDS）模式。此选项可能的模式参数包括：

auto

Use CDS if possible. This is the default value for Java HotSpot 32-Bit Client VM.
如果可能，请使用CDS。这是Java热点32位客户端虚拟机的默认值。

on

Require the use of CDS. Print an error message and exit if class data sharing cannot be used.
需要使用CDS。如果无法使用类数据共享，则打印错误消息并退出。

off

Do not use CDS. This is the default value for Java HotSpot 32-Bit Server VM, Java HotSpot 64-Bit Client VM, and Java HotSpot 64-Bit Server VM.
不要使用CDS。这是Java HotSpot 32位服务器虚拟机、Java HotSpot 64位客户端虚拟机和Java HotSpot 64位服务器虚拟机的默认值。


dump
Manually generate the CDS archive. Specify the application class path as described in "Setting the Class Path".
手动生成CDS存档。按照“设置类路径”中的说明指定应用程序类路径。

You should regenerate the CDS archive with each new JDK release.
您应该在每个新的JDK版本中重新生成CDS存档。

### -XshowSettings:category
Shows settings and continues. Possible category arguments for this option include the following:
显示设置并继续。此选项的可能类别参数包括：

all

Shows all categories of settings. This is the default value.
显示所有设置类别。这是默认值。

locale

Shows settings related to locale.
显示与区域设置相关的设置。

properties

Shows settings related to system properties.

vm
Shows the settings of the JVM.
显示与系统属性相关的设置。


### -Xsssize
Sets the thread stack size (in bytes). Append the letter k or K to indicate KB, m or M to indicate MB, g or G to indicate GB. The default value depends on the platform:
设置线程堆栈大小（字节）。附加字母k或k表示KB，m或m表示MB，g或g表示GB。默认值取决于平台：

Linux/ARM (32-bit): 320 KB

Linux/i386 (32-bit): 320 KB

Linux/x64 (64-bit): 1024 KB

OS X (64-bit): 1024 KB

Oracle Solaris/i386 (32-bit): 320 KB

Oracle Solaris/x64 (64-bit): 1024 KB

The following examples set the thread stack size to 1024 KB in different units:

-Xss1m
-Xss1024k
-Xss1048576
This option is equivalent to -XX:ThreadStackSize.


### -Xusealtsigs
Use alternative signals instead of SIGUSR1 and SIGUSR2 for JVM internal signals. This option is equivalent to -XX:+UseAltSigs.
对JVM内部信号使用替代信号，而不是SIGUSR1和SIGUSR2。此选项相当于-XX:+UseAltSigs。

### -Xverify:mode
Sets the mode of the bytecode verifier. Bytecode verification ensures that class files are properly formed and satisfy the constraints listed in section 4.10, Verification of class Files in the The Java Virtual Machine Specification.
设置字节码验证程序的模式。字节码验证确保类文件的格式正确，并满足Java虚拟机规范中第4.10节“类文件验证”中列出的约束。

Do not turn off verification as this reduces the protection provided by Java and could cause problems due to ill-formed class files.
不要关闭验证，因为这会降低Java提供的保护，并可能由于类文件格式不正确而导致问题。

Possible mode arguments for this option include the following:
此选项可能的模式参数包括：

remote

Verifies all bytecodes not loaded by the bootstrap class loader. This is the default behavior if you do not specify the -Xverify option.
验证引导类加载器未加载的所有字节码。如果不指定-Xverify选项，则这是默认行为。

all

Enables verification of all bytecodes.
启用对所有字节码的验证。


none

Disables verification of all bytecodes. Use of -Xverify:none is unsupported.
禁用所有字节码的验证。不支持使用-Xverify:none。


 
