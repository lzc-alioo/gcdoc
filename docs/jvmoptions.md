
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

- remote

Verifies all bytecodes not loaded by the bootstrap class loader. This is the default behavior if you do not specify the -Xverify option.
验证引导类加载器未加载的所有字节码。如果不指定-Xverify选项，则这是默认行为。

- all

Enables verification of all bytecodes.
启用对所有字节码的验证。


- none

Disables verification of all bytecodes. Use of -Xverify:none is unsupported.
禁用所有字节码的验证。不支持使用-Xverify:none。


 
# Advanced Runtime Options 高级运行时选项
These options control the runtime behavior of the Java HotSpot VM.
这些选项控制Java HotSpot VM的运行时行为。

## -XX:+CheckEndorsedAndExtDirs
Enables the option to prevent the java command from running a Java application if it uses the endorsed-standards override mechanism or the extension mechanism. This option checks if an application is using one of these mechanisms by checking the following:
如果java命令使用认可的标准重写机制或扩展机制，则启用此选项以阻止其运行java应用程序。此选项通过检查以下内容来检查应用程序是否正在使用这些机制之一：

The java.ext.dirs or java.endorsed.dirs system property is set.
已设置java.ext.dirs或java.endorded.dirs系统属性。

The lib/endorsed directory exists and is not empty.
lib /已签名的目录存在并且不是空的。

The lib/ext directory contains any JAR files other than those of the JDK.
lib/ext目录包含除JDK以外的任何JAR文件。

The system-wide platform-specific extension directory contains any JAR files.
系统范围内特定于平台的扩展目录包含任何JAR文件。

## -XX:+DisableAttachMechanism
Enables the option that disables the mechanism that lets tools attach to the JVM. By default, this option is disabled, meaning that the attach mechanism is enabled and you can use tools such as jcmd, jstack, jmap, and jinfo.
启用禁用允许工具附加到JVM的机制的选项。默认情况下，此选项处于禁用状态，这意味着已启用附加机制，您可以使用诸如jcmd、jstack、jmap和jinfo之类的工具。

## -XX:ErrorFile=filename
Specifies the path and file name to which error data is written when an irrecoverable error occurs. By default, this file is created in the current working directory and named hs_err_pidpid.log where pid is the identifier of the process that caused the error. The following example shows how to set the default log file (note that the identifier of the process is specified as %p):
指定发生不可恢复的错误时错误数据写入的路径和文件名。默认情况下，此文件在当前工作目录中创建，名为hs_err_pid pid.log，其中pid是导致错误的进程的标识符。下面的示例演示如何设置默认日志文件（请注意，进程的标识符指定为%p）：

    -XX:ErrorFile=./hs_err_pid%p.log
The following example shows how to set the error log to /var/log/java/java_error.log:
下面的示例演示如何将错误日志设置为/var/log/java/java_error.log：

    -XX:ErrorFile=/var/log/java/java_error.log
If the file cannot be created in the specified directory (due to insufficient space, permission problem, or another issue), then the file is created in the temporary directory for the operating system. The temporary directory is /tmp.
如果无法在指定目录中创建文件（由于空间不足、权限问题或其他问题），则在操作系统的临时目录中创建该文件。临时目录是/tmp。

    -XX:+FailOverToOldVerifier
Enables automatic failover to the old verifier when the new type checker fails. By default, this option is disabled and it is ignored (that is, treated as disabled) for classes with a recent bytecode version. You can enable it for classes with older versions of the bytecode.

## -XX:+FlightRecorder
Enables the use of the Java Flight Recorder (JFR) during the runtime of the application. This is a commercial feature that works in conjunction with the -XX:+UnlockCommercialFeatures option as follows:
在应用程序运行时启用Java飞行记录器（JFR）。这是一个与-XX:+UnlockCommercialFeatures选项结合使用的商业功能，如下所示：

    java -XX:+UnlockCommercialFeatures -XX:+FlightRecorder
If this option is not provided, Java Flight Recorder can still be enabled in a running JVM by providing the appropriate jcmd diagnostic commands.
如果没有提供此选项，那么仍然可以通过提供适当的jcmd诊断命令在运行的JVM中启用Java Flight Recorder。


## -XX:-FlightRecorder
Disables the use of the Java Flight Recorder (JFR) during the runtime of the application. This is a commercial feature that works in conjunction with the -XX:+UnlockCommercialFeatures option as follows:
在应用程序运行时禁用Java飞行记录器（JFR）。这是一个与-XX:+UnlockCommercialFeatures选项结合使用的商业功能，如下所示：

    java -XX:+UnlockCommercialFeatures -XX:-FlightRecorder
If this option is provided, Java Flight Recorder cannot be enabled in a running JVM.
如果提供此选项，则无法在运行的JVM中启用Java Flight Recorder。

    -XX:FlightRecorderOptions=parameter=value
Sets the parameters that control the behavior of JFR. This is a commercial feature that works in conjunction with the -XX:+UnlockCommercialFeatures option. This option can be used only when JFR is enabled (that is, the -XX:+FlightRecorder option is specified).
设置控制JFR行为的参数。这是一个与-XX:+UnlockCommercialFeatures选项结合使用的商业功能。此选项只能在启用JFR时使用（即指定了-XX:+FlightRecorder选项）。

The following list contains all available JFR parameters:
以下列表包含所有可用的JFR参数：

    defaultrecording={true|false}
Specifies whether the recording is a continuous background recording or if it runs for a limited time. By default, this parameter is set to false (recording runs for a limited time). To make the recording run continuously, set the parameter to true.
指定录制是连续后台录制还是运行时间有限。默认情况下，此参数设置为false（录制运行的时间有限）。要使录制连续运行，请将参数设置为true。

    disk={true|false}
Specifies whether JFR should write a continuous recording to disk. By default, this parameter is set to false (continuous recording to disk is disabled). To enable it, set the parameter to true, and also set defaultrecording=true.
指定JFR是否应将连续记录写入磁盘。默认情况下，此参数设置为false（禁用对磁盘的连续录制）。要启用它，请将参数设置为true，并将defaultrecording设置为true。

    dumponexit={true|false}
Specifies whether a dump file of JFR data should be generated when the JVM terminates in a controlled manner. By default, this parameter is set to false (dump file on exit is not generated). To enable it, set the parameter to true, and also set defaultrecording=true.
指定当JVM以受控方式终止时，是否应生成JFR数据的转储文件。默认情况下，此参数设置为false（未生成出口的转储文件）。要启用它，请将参数设置为true，并将defaultrecording设置为true。

The dump file is written to the location defined by the dumponexitpath parameter.
转储文件被写入由DimPosiExtPATH参数定义的位置。

    dumponexitpath=path
Specifies the path and name of the dump file with JFR data that is created when the JVM exits in a controlled manner if you set the dumponexit=true parameter. Setting the path makes sense only if you also set defaultrecording=true.
指定当JVM以控制方式退出时创建的具有JFR数据的转储文件的路径和名称，如果您设置了DimpOutsExt=真参数。仅当同时设置defaultrecording=true时，设置路径才有意义。

If the specified path is a directory, the JVM assigns a file name that shows the creation date and time. If the specified path includes a file name and if that file already exists, the JVM creates a new file by appending the date and time stamp to the specified file name.
如果指定的路径是目录，JVM将分配一个显示创建日期和时间的文件名。如果指定的路径包含一个文件名，如果该文件已经存在，则JVM将日期和时间戳追加到指定的文件名，从而创建一个新文件。

    globalbuffersize=size
Specifies the total amount of primary memory (in bytes) used for data retention. Append k or K, to specify the size in KB, m or M to specify the size in MB, g or G to specify the size in GB. By default, the size is set to 462848 bytes.
指定用于数据保留的主内存总量（字节）。追加k或k，以指定大小（KB）、m或m，以指定大小（MB）、g或g，以指定大小（GB）。默认情况下，大小设置为462848字节。

loglevel={quiet|error|warning|info|debug|trace}
Specify the amount of data written to the log file by JFR. By default, it is set to info.

    maxage=time
Specifies the maximum age of disk data to keep for the default recording. Append s to specify the time in seconds, m for minutes, h for hours, or d for days (for example, specifying 30s means 30 seconds). By default, the maximum age is set to 15 minutes (15m).
指定为默认记录保留的磁盘数据的最大年龄。附加s以秒为单位指定时间，m表示分钟，h表示小时，d表示天（例如，指定30s表示30秒）。默认情况下，最大年龄设置为15分钟（15m）。

This parameter is valid only if you set the disk=true parameter.
仅当设置disk=true参数时，此参数才有效。

    maxchunksize=size
Specifies the maximum size (in bytes) of the data chunks in a recording. Append k or K, to specify the size in KB, m or M to specify the size in MB, g or G to specify the size in GB. By default, the maximum size of data chunks is set to 12 MB.
指定记录中数据块的最大大小（以字节为单位）。追加k或k，以指定大小（KB）、m或m，以指定大小（MB）、g或g，以指定大小（GB）。默认情况下，数据块的最大大小设置为12 MB。

    maxsize=size
Specifies the maximum size (in bytes) of disk data to keep for the default recording. Append k or K, to specify the size in KB, m or M to specify the size in MB, g or G to specify the size in GB. By default, the maximum size of disk data is not limited, and this parameter is set to 0.
指定为缺省记录保留的磁盘数据的最大大小（以字节为单位）。追加k或k，以指定大小（KB）、m或m，以指定大小（MB）、g或g，以指定大小（GB）。默认情况下，磁盘数据的最大大小不受限制，并且该参数设置为0。

This parameter is valid only if you set the disk=true parameter.
仅当设置disk=true参数时，此参数才有效。

    repository=path
Specifies the repository (a directory) for temporary disk storage. By default, the system's temporary directory is used.
指定用于临时磁盘存储的存储库（目录）。默认情况下，使用系统的临时目录。

    samplethreads={true|false}
Specifies whether thread sampling is enabled. Thread sampling occurs only if the sampling event is enabled along with this parameter. By default, this parameter is enabled.
指定是否启用线程采样。仅当采样事件与此参数一起启用时，才会发生线程采样。默认情况下，此参数处于启用状态。

    settings=path
Specifies the path and name of the event settings file (of type JFC). By default, the default.jfc file is used, which is located in JAVA_HOME/jre/lib/jfr.
指定事件设置文件（JFC类型）的路径和名称。默认情况下，使用default.jfc文件，该文件位于JAVA_HOME/jre/lib/jfr中。

    stackdepth=depth
Stack depth for stack traces by JFR. By default, the depth is set to 64 method calls. The maximum is 2048, minimum is 1.
JFR的堆栈跟踪的堆栈深度。默认情况下，深度设置为64个方法调用。最大值为2048，最小值为1。

    threadbuffersize=size
Specifies the per-thread local buffer size (in bytes). Append k or K, to specify the size in KB, m or M to specify the size in MB, g or G to specify the size in GB. Higher values for this parameter allow more data gathering without contention to flush it to the global storage. It can increase application footprint in a thread-rich environment. By default, the local buffer size is set to 5 KB.
指定每个线程的本地缓冲区大小（字节）。追加k或k，以指定大小（KB）、m或m，以指定大小（MB）、g或g，以指定大小（GB）。此参数的值越高，允许在不争用的情况下收集更多数据，以将其刷新到全局存储。它可以在线程丰富的环境中增加应用程序占用空间。默认情况下，本地缓冲区大小设置为5 KB。

You can specify values for multiple parameters by separating them with a comma. For example, to instruct JFR to write a continuous recording to disk, and set the maximum size of data chunks to 10 MB, specify the following:
可以通过用逗号分隔多个参数来指定值。例如，为了指示JFR将连续记录写入磁盘，并将数据块的最大大小设置为10 MB，请指定以下内容：

    -XX:FlightRecorderOptions=defaultrecording=true,disk=true,maxchunksize=10M

## -XX:LargePageSizeInBytes=size
On Solaris, sets the maximum size (in bytes) for large pages used for Java heap. The size argument must be a power of 2 (2, 4, 8, 16, ...). Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes. By default, the size is set to 0, meaning that the JVM chooses the size for large pages automatically.
在Solaris上，设置用于Java堆的大页面的最大大小（以字节为单位）。size参数必须是2（2、4、8、16，…）的幂。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。默认情况下，大小设置为0，这意味着JVM自动为大页面选择大小。

The following example illustrates how to set the large page size to 4 megabytes (MB):
以下示例演示如何将大页面大小设置为4 MB：

    -XX:LargePageSizeInBytes=4m
    -XX:MaxDirectMemorySize=size
Sets the maximum total size (in bytes) of the New I/O (the java.nio package) direct-buffer allocations. Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes. By default, the size is set to 0, meaning that the JVM chooses the size for NIO direct-buffer allocations automatically.
设置新的I/O（JavaNIO包）直接缓冲区分配的最大总大小（以字节为单位）。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。默认情况下，大小设置为0，这意味着JVM自动选择NIO直接缓冲区分配的大小。

The following examples illustrate how to set the NIO size to 1024 KB in different units:
以下示例演示如何以不同的单位将NIO大小设置为1024 KB：

    -XX:MaxDirectMemorySize=1m
    -XX:MaxDirectMemorySize=1024k
    -XX:MaxDirectMemorySize=1048576
    -XX:NativeMemoryTracking=mode
Specifies the mode for tracking JVM native memory usage. Possible mode arguments for this option include the following:
指定跟踪JVM本机内存使用情况的模式。此选项可能的模式参数包括：

    off
Do not track JVM native memory usage. This is the default behavior if you do not specify the -XX:NativeMemoryTracking option.
不要跟踪JVM本机内存使用情况。如果不指定-XX:NativeMemoryTracking选项，则这是默认行为。

    summary
Only track memory usage by JVM subsystems, such as Java heap, class, code, and thread.
只跟踪JVM子系统（如Java堆、类、代码和线程）的内存使用情况。

    detail
In addition to tracking memory usage by JVM subsystems, track memory usage by individual CallSite, individual virtual memory region and its committed regions.
除了跟踪JVM子系统的内存使用情况外，还跟踪单个调用站点、单个虚拟内存区域及其提交区域的内存使用情况。

## -XX:ObjectAlignmentInBytes=alignment
Sets the memory alignment of Java objects (in bytes). By default, the value is set to 8 bytes. The specified value should be a power of two, and must be within the range of 8 and 256 (inclusive). This option makes it possible to use compressed pointers with large Java heap sizes.
设置Java对象的内存对齐方式（字节）。默认情况下，该值设置为8字节。指定的值应为2的幂，并且必须在8和256（含）的范围内。此选项使使用具有较大Java堆大小的压缩指针成为可能。

The heap size limit in bytes is calculated as:
以字节为单位的堆大小限制计算如下：

    4GB * ObjectAlignmentInBytes

Note: As the alignment value increases, the unused space between objects will also increase. As a result, you may not realize any benefits from using compressed pointers with large Java heap sizes.
注意：随着对齐值的增加，对象之间未使用的空间也会增加。因此，您可能没有意识到使用具有较大Java堆大小的压缩指针有任何好处。

## -XX:OnError=string
Sets a custom command or a series of semicolon-separated commands to run when an irrecoverable error occurs. If the string contains spaces, then it must be enclosed in quotation marks.
设置当发生不可恢复的错误时要运行的自定义命令或一系列分号分隔的命令。如果字符串包含空格，则必须用引号括起来。

The following example shows how the -XX:OnError option can be used to run the gcore command to create the core image, and the debugger is started to attach to the process in case of an irrecoverable error (the %p designates the current process):
以下示例显示如何使用-XX:OnError选项运行gcore命令以创建核心映像，并在出现不可恢复的错误时启动调试器以附加到进程（由%p指定当前进程）：

    -XX:OnError="gcore %p;dbx - %p"
    
## -XX:OnOutOfMemoryError=string
Sets a custom command or a series of semicolon-separated commands to run when an OutOfMemoryError exception is first thrown. If the string contains spaces, then it must be enclosed in quotation marks. For an example of a command string, see the description of the -XX:OnError option.
设置自定义命令或一系列分号分隔的命令，以便在首次引发OutOfMemoryError异常时运行。如果字符串包含空格，则必须用引号括起来。有关命令字符串的示例，请参见-XX:OnError选项的说明。

## -XX:+PerfDataSaveToFile
If enabled, saves jstat(1) binary data when the Java application exits. This binary data is saved in a file named hsperfdata_<pid>, where <pid> is the process identifier of the Java application you ran. Use jstat to display the performance data contained in this file as follows:
如果启用，则在Java应用退出时保存JSTAT（1）二进制数据。这个二进制数据保存在一个名为hsperfdata<pid>的文件中，其中<pid>是您运行的Java应用程序的进程标识符。使用jstat显示此文件中包含的性能数据，如下所示：

    jstat -class file:///<path>/hsperfdata_<pid>
    jstat -gc file:///<path>/hsperfdata_<pid>

# -XX:+PrintCommandLineFlags
Enables printing of ergonomically selected JVM flags that appeared on the command line. It can be useful to know the ergonomic values set by the JVM, such as the heap space size and the selected garbage collector. By default, this option is disabled and flags are not printed.
允许打印出现在命令行上的符合人体工程学的选定JVM标志。了解由JVM设置的符合人体工程学的值（例如堆空间大小和所选的垃圾收集器）是很有用的。默认情况下，此选项处于禁用状态，不打印标志。

## -XX:+PrintNMTStatistics
Enables printing of collected native memory tracking data at JVM exit when native memory tracking is enabled (see -XX:NativeMemoryTracking). By default, this option is disabled and native memory tracking data is not printed.
当启用原生内存跟踪时，可以在JVM出口处打印收集的本地内存跟踪数据（请参阅。默认情况下，此选项处于禁用状态，不会打印本机内存跟踪数据。

## -XX:+RelaxAccessControlCheck
Decreases the amount of access control checks in the verifier. By default, this option is disabled, and it is ignored (that is, treated as disabled) for classes with a recent bytecode version. You can enable it for classes with older versions of the bytecode.
减少验证器中访问控制检查的数量。默认情况下，此选项处于禁用状态，对于具有最新字节码版本的类，此选项将被忽略（即视为禁用）。您可以为具有旧版本字节码的类启用它。

## -XX:+ResourceManagement
Enables the use of Resource Management during the runtime of the application.
允许在应用程序运行时使用资源管理。

This is a commercial feature that requires you to also specify the -XX:+UnlockCommercialFeatures option as follows:
这是一个商业特性，要求您还指定-XX:+UnlockCommercialFeatures选项，如下所示：

    java -XX:+UnlockCommercialFeatures -XX:+ResourceManagement


## -XX:ResourceManagementSampleInterval=value (milliseconds)
Sets the parameter that controls the sampling interval for Resource Management measurements, in milliseconds.
设置用于控制资源管理度量的采样间隔的参数（以毫秒为单位）。

This option can be used only when Resource Management is enabled (that is, the -XX:+ResourceManagement option is specified).
此选项只能在启用资源管理时使用（即指定了-XX:+Resource Management选项）。

## -XX:SharedArchiveFile=path
Specifies the path and name of the class data sharing (CDS) archive file
指定类数据共享（CDS）存档文件的路径和名称

## -XX:SharedClassListFile=file_name
Specifies the text file that contains the names of the class files to store in the class data sharing (CDS) archive. This file contains the full name of one class file per line, except slashes (/) replace dots (.). For example, to specify the classes java.lang.Object and hello.Main, create a text file that contains the following two lines:
指定包含要存储在类数据共享（CDS）存档中的类文件的名称的文本文件。此文件包含每行一个类文件的全名，除了斜线（/）替换点（.）。例如，要指定java.lang.Object和hello.Main类，请创建包含以下两行的文本文件：


    java/lang/Object
    hello/Main
The class files that you specify in this text file should include the classes that are commonly used by the application. They may include any classes from the application, extension, or bootstrap class paths.
在此文本文件中指定的类文件应包括应用程序常用的类。它们可以包括应用程序、扩展或引导类路径中的任何类。


## -XX:+ShowMessageBoxOnError
Enables displaying of a dialog box when the JVM experiences an irrecoverable error. This prevents the JVM from exiting and keeps the process active so that you can attach a debugger to it to investigate the cause of the error. By default, this option is disabled.
允许在JVM遇到不可恢复的错误时显示对话框。这样可以防止JVM退出并保持进程的活动性，这样您就可以将调试器附加到它来调查错误的原因。默认情况下，此选项处于禁用状态。

## -XX:StartFlightRecording=parameter=value
Starts a JFR recording for the Java application. This is a commercial feature that works in conjunction with the -XX:+UnlockCommercialFeatures option. This option is equivalent to the JFR.start diagnostic command that starts a recording during runtime. You can set the following parameters when starting a JFR recording:
为Java应用程序启动JFR记录。这是一个与-XX:+UnlockCommercialFeatures选项结合使用的商业功能。此选项相当于JFR.start diagnostic命令，该命令在运行时启动录制。开始JFR录制时，可以设置以下参数：

    compress={true|false}
Specifies whether to compress the JFR recording log file (of type JFR) on the disk using the gzip file compression utility. This parameter is valid only if the filename parameter is specified. By default it is set to false (recording is not compressed). To enable compression, set the parameter to true.
指定是否使用gzip文件压缩实用程序压缩磁盘上的JFR记录日志文件（JFR类型）。仅当指定了filename参数时，此参数才有效。默认设置为false（录制不压缩）。要启用压缩，请将参数设置为true。

    defaultrecording={true|false}
Specifies whether the recording is a continuous background recording or if it runs for a limited time. By default, this parameter is set to false (recording runs for a limited time). To make the recording run continuously, set the parameter to true.
指定录制是连续后台录制还是运行时间有限。默认情况下，此参数设置为false（录制运行的时间有限）。要使录制连续运行，请将参数设置为true。

    delay=time
Specifies the delay between the Java application launch time and the start of the recording. Append s to specify the time in seconds, m for minutes, h for hours, or d for days (for example, specifying 10m means 10 minutes). By default, there is no delay, and this parameter is set to 0.
指定Java应用程序启动时间与录制开始之间的延迟。附加s以秒为单位指定时间，m表示分钟，h表示小时，d表示天（例如，指定10m表示10分钟）。默认情况下，没有延迟，此参数设置为0。

    dumponexit={true|false}
Specifies whether a dump file of JFR data should be generated when the JVM terminates in a controlled manner. By default, this parameter is set to false (dump file on exit is not generated). To enable it, set the parameter to true.
指定当JVM以受控方式终止时，是否应生成JFR数据的转储文件。默认情况下，此参数设置为false（未生成出口的转储文件）。要启用它，请将参数设置为true。

The dump file is written to the location defined by the filename parameter.
转储文件将写入filename参数定义的位置。

Example:

```   
 -XX:StartFlightRecording=name=test,filename=D:\test.jfr,dumponexit=true
```

    duration=time
Specifies the duration of the recording. Append s to specify the time in seconds, m for minutes, h for hours, or d for days (for example, specifying 5h means 5 hours). By default, the duration is not limited, and this parameter is set to 0.
指定录制的持续时间。附加s以秒为单位指定时间，m表示分钟，h表示小时，d表示天（例如，指定5h表示5小时）。默认情况下，持续时间不受限制，此参数设置为0。

    filename=path
Specifies the path and name of the JFR recording log file.
指定JFR记录日志文件的路径和名称。

    name=identifier
Specifies the identifier for the JFR recording. By default, it is set to Recording x.
指定JFR记录的标识符。默认设置为录制x。

    maxage=time
Specifies the maximum age of disk data to keep for the default recording. Append s to specify the time in seconds, m for minutes, h for hours, or d for days (for example, specifying 30s means 30 seconds). By default, the maximum age is set to 15 minutes (15m).
指定为默认记录保留的磁盘数据的最大年龄。附加s以秒为单位指定时间，m表示分钟，h表示小时，d表示天（例如，指定30s表示30秒）。默认情况下，最大年龄设置为15分钟（15m）。

    maxsize=size
Specifies the maximum size (in bytes) of disk data to keep for the default recording. Append k or K, to specify the size in KB, m or M to specify the size in MB, g or G to specify the size in GB. By default, the maximum size of disk data is not limited, and this parameter is set to 0.
指定为缺省记录保留的磁盘数据的最大大小（以字节为单位）。追加k或k，以指定大小（KB）、m或m，以指定大小（MB）、g或g，以指定大小（GB）。默认情况下，磁盘数据的最大大小不受限制，并且该参数设置为0。

    settings=path
Specifies the path and name of the event settings file (of type JFC). By default, the default.jfc file is used, which is located in JAVA_HOME/jre/lib/jfr.
指定事件设置文件（JFC类型）的路径和名称。默认情况下，使用default.jfc文件，该文件位于JAVA_HOME/jre/lib/jfr中。

You can specify values for multiple parameters by separating them with a comma. For example, to save the recording to test.jfr in the current working directory, and instruct JFR to compress the log file, specify the following:
可以通过用逗号分隔多个参数来指定值。例如，要将记录保存到当前工作目录中的test.jfr，并指示jfr压缩日志文件，请指定以下内容：

```-XX:StartFlightRecording=filename=test.jfr,compress=true```

    -XX:ThreadStackSize=size
Sets the thread stack size (in bytes). Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes. The default value depends on the platform:
设置线程堆栈大小（字节）。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。默认值取决于平台：

Linux/ARM (32-bit): 320 KB

Linux/i386 (32-bit): 320 KB

Linux/x64 (64-bit): 1024 KB

OS X (64-bit): 1024 KB

Oracle Solaris/i386 (32-bit): 320 KB

Oracle Solaris/x64 (64-bit): 1024 KB

The following examples show how to set the thread stack size to 1024 KB in different units:
以下示例演示如何以不同的单位将线程堆栈大小设置为1024 KB：

-XX:ThreadStackSize=1m
-XX:ThreadStackSize=1024k
-XX:ThreadStackSize=1048576
This option is equivalent to -Xss.
此选项相当于-Xss。

## -XX:+TraceClassLoading

Enables tracing of classes as they are loaded. By default, this option is disabled and classes are not traced.
启用类加载时的跟踪。默认情况下，此选项被禁用，并且不跟踪类。

## -XX:+TraceClassLoadingPreorder

Enables tracing of all loaded classes in the order in which they are referenced. By default, this option is disabled and classes are not traced.
启用按引用顺序跟踪所有加载的类。默认情况下，此选项被禁用，并且不跟踪类。

## -XX:+TraceClassResolution

Enables tracing of constant pool resolutions. By default, this option is disabled and constant pool resolutions are not traced.
启用对恒定池分辨率的跟踪。默认情况下，此选项处于禁用状态，并且不会跟踪固定池分辨率。

## -XX:+TraceClassUnloading
Enables tracing of classes as they are unloaded. By default, this option is disabled and classes are not traced.
允许在类卸载时跟踪它们。默认情况下，此选项被禁用，并且不跟踪类。

## -XX:+TraceLoaderConstraints
Enables tracing of the loader constraints recording. By default, this option is disabled and loader constraints recording is not traced.
启用加载程序约束记录的跟踪。默认情况下，此选项被禁用，并且不会跟踪加载程序约束记录。

## -XX:+UnlockCommercialFeatures
Enables the use of commercial features. Commercial features are included with Oracle Java SE Advanced or Oracle Java SE Suite packages, as defined on the Java SE Products page at http://www.oracle.com/technetwork/java/javase/terms/products/index.html
允许使用商业功能。商业特性包含在Oracle Java SE Advanced或Oracle Java SE Suite软件包中，如http://www.Oracle.com/technetwork/Java/Java SE/terms/Products/index.html上的Java SE产品页面所定义

By default, this option is disabled and the JVM runs without the commercial features. Once they were enabled for a JVM process, it is not possible to disable their use for that process.
默认情况下，此选项被禁用，并且JVM运行时没有商业特性。一旦为JVM进程启用了它们，就不可能禁用它们对该进程的使用。

If this option is not provided, commercial features can still be unlocked in a running JVM by using the appropriate jcmd diagnostic commands.
如果未提供此选项，则仍然可以使用适当的jcmd诊断命令在运行的JVM中解锁商业特性。

## -XX:+UseAltSigs
Enables the use of alternative signals instead of SIGUSR1 and SIGUSR2 for JVM internal signals. By default, this option is disabled and alternative signals are not used. This option is equivalent to -Xusealtsigs.
允许对JVM内部信号使用替代信号，而不是SIGUSR1和SIGUSR2。默认情况下，此选项被禁用，并且不使用替代信号。此选项相当于-xusailtsigs。

## -XX:+UseAppCDS
Enables application class data sharing (AppCDS). To use AppCDS, you must also specify values for the options -XX:SharedClassListFile and -XX:SharedArchiveFile during both CDS dump time (see the option -Xshare:dump) and application run time.
启用应用程序类数据共享（AppCD）。要使用AppCDS，还必须在CDS转储时间（请参阅选项-Xshare:dump）和应用程序运行时为选项-XX:SharedClassListFile和-XX:SharedArchiveFile指定值。

This is a commercial feature that requires you to also specify the -XX:+UnlockCommercialFeatures option. This is also an experimental feature; it may change in future releases.
这是一个商业特性，要求您还指定-XX:+UnlockCommercialFeatures选项。这也是一个实验特性；在将来的版本中可能会有所改变。

See "Application Class Data Sharing".
请参阅“应用程序类数据共享”。

## -XX:-UseBiasedLocking
Disables the use of biased locking. Some applications with significant amounts of uncontended synchronization may attain significant speedups with this flag enabled, whereas applications with certain patterns of locking may see slowdowns. For more information about the biased locking technique, see the example in Java Tuning White Paper at http://www.oracle.com/technetwork/java/tuning-139912.html#section4.2.5
禁用偏置锁定的使用。一些具有大量非竞争同步的应用程序在启用此标志时可能会获得显著的加速，而具有某些锁定模式的应用程序可能会看到减速。有关偏向锁定技术的更多信息，请参阅Java Tuning白皮书中的示例，网址为http://www.oracle.com/technetwork/Java/Tuning-139912.html#section4.2.5

By default, this option is enabled.
默认情况下，此选项处于启用状态。

## -XX:-UseCompressedOops
Disables the use of compressed pointers. By default, this option is enabled, and compressed pointers are used when Java heap sizes are less than 32 GB. When this option is enabled, object references are represented as 32-bit offsets instead of 64-bit pointers, which typically increases performance when running the application with Java heap sizes less than 32 GB. This option works only for 64-bit JVMs.
禁用压缩指针的使用。默认情况下，此选项处于启用状态，当Java堆大小小于32 GB时使用压缩指针。启用此选项后，对象引用将表示为32位偏移量，而不是64位指针，这通常会在运行Java堆大小小于32 GB的应用程序时提高性能。此选项仅适用于64位JVM。

It is also possible to use compressed pointers when Java heap sizes are greater than 32GB. See the -XX:ObjectAlignmentInBytes option.
当Java堆大小大于32GB时，也可以使用压缩指针。请参阅-XX:ObjectAlignmentInBytes选项。

## -XX:+UseHugeTLBFS
This option for Linux is the equivalent of specifying -XX:+UseLargePages. This option is disabled by default. This option pre-allocates all large pages up-front, when memory is reserved; consequently the JVM cannot dynamically grow or shrink large pages memory areas; see -XX:UseTransparentHugePages if you want this behavior.
Linux的这个选项相当于指定-XX:+UseLargePages。默认情况下禁用此选项。此选项在保留内存时预先分配所有大页；因此，JVM无法动态地增大或缩小大页内存区域；如果需要此行为，请参阅-XX:UseTransparentHugePages。

For more information, see "Large Pages".
有关详细信息，请参阅“大页”。

## -XX:+UseLargePages
Enables the use of large page memory. By default, this option is disabled and large page memory is not used.
启用大页内存的使用。默认情况下，此选项被禁用，并且不使用大页内存。

For more information, see "Large Pages".

## -XX:+UseMembar
Enables issuing of membars on thread state transitions. This option is disabled by default on all platforms except ARM servers, where it is enabled. (It is recommended that you do not disable this option on ARM servers.)
允许在线程状态转换时发出membar。默认情况下，除启用此选项的ARM服务器外，所有平台上都禁用此选项。（建议不要在ARM服务器上禁用此选项。）

## -XX:+UsePerfData
Enables the perfdata feature. This option is enabled by default to allow JVM monitoring and performance testing. Disabling it suppresses the creation of the hsperfdata_userid directories. To disable the perfdata feature, specify -XX:-UsePerfData.
启用perfdata功能。默认情况下，此选项被启用以允许JVM监视和性能测试。禁用它将禁止创建hsperfdata\u userid目录。要禁用perfdata功能，请指定-XX:-UsePerfData。

## -XX:+UseTransparentHugePages
On Linux, enables the use of large pages that can dynamically grow or shrink. This option is disabled by default. You may encounter performance problems with transparent huge pages as the OS moves other pages around to create huge pages; this option is made available for experimentation.
在Linux上，允许使用可以动态增长或收缩的大页面。默认情况下禁用此选项。当操作系统移动其他页面以创建大页面时，可能会遇到透明大页面的性能问题；此选项可用于实验。

For more information, see "Large Pages".

## -XX:+AllowUserSignalHandlers
Enables installation of signal handlers by the application. By default, this option is disabled and the application is not allowed to install signal handlers.
允许应用程序安装信号处理程序。默认情况下，此选项被禁用，应用程序不允许安装信号处理程序。

Advanced JIT Compiler Options
These options control the dynamic just-in-time (JIT) compilation performed by the Java HotSpot VM.
这些选项控制Java热点VM执行的动态实时（JIT）编译。

## -XX:+AggressiveOpts
Enables the use of aggressive performance optimization features, which are expected to become default in upcoming releases. By default, this option is disabled and experimental performance features are not used.
允许使用积极的性能优化功能，这些功能预计将在即将发布的版本中成为默认功能。默认情况下，此选项被禁用，并且不使用实验性能功能。

## -XX:AllocateInstancePrefetchLines=lines
Sets the number of lines to prefetch ahead of the instance allocation pointer. By default, the number of lines to prefetch is set to 1:
设置要在实例分配指针之前预取的行数。默认情况下，要预取的行数设置为1：

    -XX:AllocateInstancePrefetchLines=1
Only the Java HotSpot Server VM supports this option.
只有Java热点服务器VM支持此选项。


## -XX:AllocatePrefetchDistance=size
Sets the size (in bytes) of the prefetch distance for object allocation. Memory about to be written with the value of new objects is prefetched up to this distance starting from the address of the last allocated object. Each Java thread has its own allocation point.
设置对象分配的预取距离的大小（字节）。将要用新对象的值写入的内存从上次分配对象的地址开始预取到此距离。每个Java线程都有自己的分配点。

Negative values denote that prefetch distance is chosen based on the platform. Positive values are bytes to prefetch. Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes. The default value is set to -1.
负值表示根据平台选择预取距离。正值是要预取的字节。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。默认值设置为-1。

The following example shows how to set the prefetch distance to 1024 bytes:
下面的示例演示如何将预取距离设置为1024字节：

    -XX:AllocatePrefetchDistance=1024
Only the Java HotSpot Server VM supports this option.
只有Java热点服务器VM支持此选项。

## -XX:AllocatePrefetchInstr=instruction
Sets the prefetch instruction to prefetch ahead of the allocation pointer. Only the Java HotSpot Server VM supports this option. Possible values are from 0 to 3. The actual instructions behind the values depend on the platform. By default, the prefetch instruction is set to 0:
将预取指令设置为在分配指针之前预取。只有Java热点服务器VM支持此选项。可能的值为0到3。值后面的实际指令取决于平台。默认情况下，预取指令设置为0：

## -XX:AllocatePrefetchInstr=0
Only the Java HotSpot Server VM supports this option.
只有Java热点服务器VM支持此选项。

## -XX:AllocatePrefetchLines=lines
Sets the number of cache lines to load after the last object allocation by using the prefetch instructions generated in compiled code. The default value is 1 if the last allocated object was an instance, and 3 if it was an array.
通过使用编译代码中生成的预取指令，设置上次对象分配后要加载的缓存行数。如果最后分配的对象是实例，则默认值为1；如果是数组，则默认值为3。

The following example shows how to set the number of loaded cache lines to 5:
下面的示例演示如何将加载的缓存线数设置为5：

    -XX:AllocatePrefetchLines=5
Only the Java HotSpot Server VM supports this option.
只有Java热点服务器VM支持此选项。


## -XX:AllocatePrefetchStepSize=size
Sets the step size (in bytes) for sequential prefetch instructions. Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes. By default, the step size is set to 16 bytes:
设置顺序预取指令的步长（字节）。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。默认情况下，步长设置为16字节：

    -XX:AllocatePrefetchStepSize=16
Only the Java HotSpot Server VM supports this option.
只有Java热点服务器VM支持此选项。


## -XX:AllocatePrefetchStyle=style
Sets the generated code style for prefetch instructions. The style argument is an integer from 0 to 3:
设置预取指令的生成代码样式。样式参数是从0到3的整数：

### 0
Do not generate prefetch instructions. 不要生成预取指令。
                                       
### 1
Execute prefetch instructions after each allocation. This is the default parameter.
每次分配后执行预取指令。这是默认参数。

### 2
Use the thread-local allocation block (TLAB) watermark pointer to determine when prefetch instructions are executed.
使用线程本地分配块（TLAB）水印指针确定何时执行预取指令。

### 3
Use BIS instruction on SPARC for allocation prefetch.
在SPARC上使用BIS指令进行分配预取。


Only the Java HotSpot Server VM supports this option.
只有Java热点服务器VM支持此选项。


## -XX:+BackgroundCompilation
Enables background compilation. This option is enabled by default. To disable background compilation, specify -XX:-BackgroundCompilation (this is equivalent to specifying -Xbatch).
启用后台编译。默认情况下，此选项处于启用状态。要禁用后台编译，请指定-XX:-BackgroundCompilation（这相当于指定-Xbatch）。

## -XX:CICompilerCount=threads
Sets the number of compiler threads to use for compilation. By default, the number of threads is set to 2 for the server JVM, to 1 for the client JVM, and it scales to the number of cores if tiered compilation is used. The following example shows how to set the number of threads to 2:
设置要用于编译的编译器线程数。默认情况下，服务器JVM的线程数设置为2，客户端JVM的线程数设置为1，如果使用分层编译，则线程数将根据核心数进行调整。下面的示例演示如何将线程数设置为2：

    -XX:CICompilerCount=2
    
## -XX:CodeCacheMinimumFreeSpace=size
Sets the minimum free space (in bytes) required for compilation. Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes. When less than the minimum free space remains, compiling stops. By default, this option is set to 500 KB. The following example shows how to set the minimum free space to 1024 MB:
设置编译所需的最小可用空间（字节）。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。当剩余的可用空间小于最小值时，编译将停止。默认情况下，此选项设置为500 KB。下面的示例演示如何将最小可用空间设置为1024 MB：

    -XX:CodeCacheMinimumFreeSpace=1024m

## -XX:CompileCommand=command,method[,option]
Specifies a command to perform on a method. For example, to exclude the indexOf() method of the String class from being compiled, use the following:
指定要对方法执行的命令。例如，要从编译中排除字符串类的indexOf（）方法，请使用以下命令：

    -XX:CompileCommand=exclude,java/lang/String.indexOf
Note that the full class name is specified, including all packages and subpackages separated by a slash (/). For easier cut and paste operations, it is also possible to use the method name format produced by the -XX:+PrintCompilation and -XX:+LogCompilation options:
注意，指定了完整的类名，包括用斜线（/）分隔的所有包和子包。为了简化剪切和粘贴操作，还可以使用-XX:+PrintCompilation和-XX:+LogCompilation选项生成的方法名格式：


    -XX:CompileCommand=exclude,java.lang.String::indexOf
If the method is specified without the signature, the command will be applied to all methods with the specified name. However, you can also specify the signature of the method in the class file format. In this case, you should enclose the arguments in quotation marks, because otherwise the shell treats the semicolon as command end. For example, if you want to exclude only the indexOf(String) method of the String class from being compiled, use the following:
如果指定的方法没有签名，则该命令将应用于具有指定名称的所有方法。但是，也可以用类文件格式指定方法的签名。在这种情况下，应该将参数括在引号中，否则shell将分号视为命令结尾。例如，如果只想排除正在编译的String类的indexOf（String）方法，请使用以下命令：


    -XX:CompileCommand="exclude,java/lang/String.indexOf,(Ljava/lang/String;)I"
You can also use the asterisk (*) as a wildcard for class and method names. For example, to exclude all indexOf() methods in all classes from being compiled, use the following:
也可以使用星号（*）作为类和方法名的通配符。例如，要从编译中排除所有类中的所有indexOf（）方法，请使用以下命令：


    -XX:CompileCommand=exclude,*.indexOf
The commas and periods are aliases for spaces, making it easier to pass compiler commands through a shell. You can pass arguments to -XX:CompileCommand using spaces as separators by enclosing the argument in quotation marks:
逗号和句点是空格的别名，使编译器命令更容易通过shell传递。通过将参数括在引号中，可以使用空格作为分隔符将参数传递给-XX:CompileCommand：


    -XX:CompileCommand="exclude java/lang/String indexOf"
Note that after parsing the commands passed on the command line using the -XX:CompileCommand options, the JIT compiler then reads commands from the .hotspot_compiler file. You can add commands to this file or specify a different file using the -XX:CompileCommandFile option.
注意，在使用-XX:CompileCommand选项分析命令行上传递的命令之后，JIT编译器将从.hotspot_编译器文件中读取命令。您可以向该文件添加命令，也可以使用-XX:CompileCommandFile选项指定其他文件。


To add several commands, either specify the -XX:CompileCommand option multiple times, or separate each argument with the newline separator (\n). The following commands are available:
若要添加多个命令，请多次指定-XX:CompileCommand选项，或使用换行分隔符（\n）分隔每个参数。以下命令可用：


### break
Set a breakpoint when debugging the JVM to stop at the beginning of compilation of the specified method.
在调试JVM时设置断点，以便在编译指定方法的开始时停止。

### compileonly
Exclude all methods from compilation except for the specified method. As an alternative, you can use the -XX:CompileOnly option, which allows to specify several methods.
从编译中排除除指定方法之外的所有方法。作为替代方案，您可以使用-XX:CompileOnly选项，该选项允许指定多个方法。

### dontinline
Prevent inlining of the specified method.
防止指定方法的内联。


### exclude
Exclude the specified method from compilation.
从编译中排除指定的方法。


### help
Print a help message for the -XX:CompileCommand option.
打印-XX:CompileCommand选项的帮助消息。


### inline
Attempt to inline the specified method.
尝试内联指定的方法。


### log
Exclude compilation logging (with the -XX:+LogCompilation option) for all methods except for the specified method. By default, logging is performed for all compiled methods.
排除除指定方法之外的所有方法的编译日志记录（使用-XX:+LogCompilation选项）。默认情况下，对所有编译的方法执行日志记录。


### option
This command can be used to pass a JIT compilation option to the specified method in place of the last argument (option). The compilation option is set at the end, after the method name. For example, to enable the BlockLayoutByFrequency option for the append() method of the StringBuffer class, use the following:
此命令可用于将JIT编译选项传递给指定的方法，以代替最后一个参数（选项）。编译选项设置在方法名之后的末尾。例如，要为StringBuffer类的append（）方法启用BlockLayoutByFrequency选项，请使用以下命令：


    -XX:CompileCommand=option,java/lang/StringBuffer.append,BlockLayoutByFrequency
You can specify multiple compilation options, separated by commas or spaces.
可以指定多个编译选项，用逗号或空格分隔。


### print
Print generated assembler code after compilation of the specified method.
在编译指定方法后打印生成的汇编程序代码。


### quiet
Do not print the compile commands. By default, the commands that you specify with the -XX:CompileCommand option are printed; for example, if you exclude from compilation the indexOf() method of the String class, then the following will be printed to standard output:
不要打印编译命令。默认情况下，将打印使用-XX:CompileCommand选项指定的命令；例如，如果从编译中排除字符串类的indexOf（）方法，则以下命令将打印到标准输出：


CompilerOracle: exclude java/lang/String.indexOf
You can suppress this by specifying the -XX:CompileCommand=quiet option before other -XX:CompileCommand options.
可以通过在其他-XX:CompileCommand选项之前指定-XX:CompileCommand=quiet选项来禁止此操作。


## -XX:CompileCommandFile=filename
Sets the file from which JIT compiler commands are read. By default, the .hotspot_compiler file is used to store commands performed by the JIT compiler.
设置从中读取JIT编译器命令的文件。默认情况下，.hotspot_编译器文件用于存储JIT编译器执行的命令。


Each line in the command file represents a command, a class name, and a method name for which the command is used. For example, this line prints assembly code for the toString() method of the String class:
命令文件中的每一行代表一个命令、一个类名和一个使用该命令的方法名。例如，此行打印字符串类的toString（）方法的程序集代码：


    print java/lang/String toString
For more information about specifying the commands for the JIT compiler to perform on methods, see the -XX:CompileCommand option.
有关指定JIT编译器对方法执行的命令的详细信息，请参阅-XX:CompileCommand选项。


## -XX:CompileOnly=methods
Sets the list of methods (separated by commas) to which compilation should be restricted. Only the specified methods will be compiled. Specify each method with the full class name (including the packages and subpackages). For example, to compile only the length() method of the String class and the size() method of the List class, use the following:
设置编译应限制到的方法列表（用逗号分隔）。只编译指定的方法。使用完整类名指定每个方法（包括包和子包）。例如，要只编译String类的length（）方法和List类的size（）方法，请使用以下命令：

    -XX:CompileOnly=java/lang/String.length,java/util/List.size
Note that the full class name is specified, including all packages and subpackages separated by a slash (/). For easier cut and paste operations, it is also possible to use the method name format produced by the -XX:+PrintCompilation and -XX:+LogCompilation options:
注意，指定了完整的类名，包括用斜线（/）分隔的所有包和子包。为了简化剪切和粘贴操作，还可以使用-XX:+PrintCompilation和-XX:+LogCompilation选项生成的方法名格式：


    -XX:CompileOnly=java.lang.String::length,java.util.List::size
Although wildcards are not supported, you can specify only the class or package name to compile all methods in that class or package, as well as specify just the method to compile methods with this name in any class:
尽管不支持通配符，但您只能指定类或包名称来编译该类或包中的所有方法，也可以仅指定在任何类中使用此名称编译方法的方法：


    -XX:CompileOnly=java/lang/String
    -XX:CompileOnly=java/lang
    -XX:CompileOnly=.length
    -XX:CompileThreshold=invocations
Sets the number of interpreted method invocations before compilation. By default, in the server JVM, the JIT compiler performs 10,000 interpreted method invocations to gather information for efficient compilation. For the client JVM, the default setting is 1,500 invocations. This option is ignored when tiered compilation is enabled; see the option -XX:+TieredCompilation. The following example shows how to set the number of interpreted method invocations to 5,000:

## -XX:CompileThreshold=5000
You can completely disable interpretation of Java methods before compilation by specifying the -Xcomp option.
设置编译前解释的方法调用数。默认情况下，在服务器JVM中，JIT编译器执行10000次解释的方法调用，以收集有效编译所需的信息。对于客户端JVM，默认设置为1500次调用。启用分层编译时将忽略此选项；请参阅选项-XX:+tieredcomplilation。下面的示例演示如何将解释的方法调用数设置为5000：

## -XX:+DoEscapeAnalysis
Enables the use of escape analysis. This option is enabled by default. To disable the use of escape analysis, specify -XX:-DoEscapeAnalysis. Only the Java HotSpot Server VM supports this option.
启用转义分析的使用。默认情况下，此选项处于启用状态。要禁用转义分析的使用，请指定-XX:-DoEscapeAnalysis。只有Java热点服务器VM支持此选项。


## -XX:InitialCodeCacheSize=size
Sets the initial code cache size (in bytes). Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes. The default value is set to 500 KB. The initial code cache size should be not less than the system's minimal memory page size. The following example shows how to set the initial code cache size to 32 KB:
设置初始代码缓存大小（字节）。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。默认值设置为500 KB。初始代码缓存大小不应小于系统的最小内存页大小。下面的示例演示如何将初始代码缓存大小设置为32 KB：


## -XX:InitialCodeCacheSize=32k
## -XX:+Inline
Enables method inlining. This option is enabled by default to increase performance. To disable method inlining, specify -XX:-Inline.
启用方法内联。默认情况下会启用此选项以提高性能。要禁用方法内联，请指定-XX:-Inline。


## -XX:InlineSmallCode=size
Sets the maximum code size (in bytes) for compiled methods that should be inlined. Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes. Only compiled methods with the size smaller than the specified size will be inlined. By default, the maximum code size is set to 1000 bytes:
设置应内联的编译方法的最大代码大小（以字节为单位）。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。只有小于指定大小的已编译方法才会被内联。默认情况下，最大代码大小设置为1000字节：


    -XX:InlineSmallCode=1000
## -XX:+LogCompilation
Enables logging of compilation activity to a file named hotspot.log in the current working directory. You can specify a different log file path and name using the -XX:LogFile option.
启用将编译活动记录到当前工作目录中名为hotspot.log的文件。您可以使用-XX:log file选项指定不同的日志文件路径和名称。


By default, this option is disabled and compilation activity is not logged. The -XX:+LogCompilation option has to be used together with the -XX:UnlockDiagnosticVMOptions option that unlocks diagnostic JVM options.
默认情况下，此选项被禁用，编译活动不被记录。-XX:+LogCompilation选项必须与-XX:UnlockDiagnosticVMOptions选项一起使用，该选项将解除对诊断JVM选项的锁定。


You can enable verbose diagnostic output with a message printed to the console every time a method is compiled by using the -XX:+PrintCompilation option.
通过使用-XX:+PrintCompilation选项，每次编译方法时，都可以使用打印到控制台的消息启用详细诊断输出。


## -XX:MaxInlineSize=size
Sets the maximum bytecode size (in bytes) of a method to be inlined. Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes. By default, the maximum bytecode size is set to 35 bytes:
设置要内联的方法的最大字节码大小（以字节为单位）。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。默认情况下，最大字节码大小设置为35字节：


    -XX:MaxInlineSize=35
    
## -XX:MaxNodeLimit=nodes
Sets the maximum number of nodes to be used during single method compilation. By default, the maximum number of nodes is set to 65,000:
设置在单个方法编译期间要使用的节点的最大数目。默认情况下，节点的最大数量设置为65000：


    -XX:MaxNodeLimit=65000
## -XX:MaxTrivialSize=size
Sets the maximum bytecode size (in bytes) of a trivial method to be inlined. Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes. By default, the maximum bytecode size of a trivial method is set to 6 bytes:
设置要内联的平凡方法的最大字节码大小（以字节为单位）。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。默认情况下，平凡方法的最大字节码大小设置为6字节：

    -XX:MaxTrivialSize=6

## -XX:+OptimizeStringConcat
Enables the optimization of String concatenation operations. This option is enabled by default. To disable the optimization of String concatenation operations, specify -XX:-OptimizeStringConcat. Only the Java HotSpot Server VM supports this option.
启用字符串连接操作的优化。默认情况下，此选项处于启用状态。要禁用字符串连接操作的优化，请指定-XX:-OptimizeStringConcat。只有Java热点服务器VM支持此选项。


## -XX:+PrintAssembly
Enables printing of assembly code for bytecoded and native methods by using the external disassembler.so library. This enables you to see the generated code, which may help you to diagnose performance issues.
允许使用外部反汇编程序.so库打印字节编码和本机方法的程序集代码。这使您能够看到生成的代码，这可能有助于诊断性能问题。

By default, this option is disabled and assembly code is not printed. The -XX:+PrintAssembly option has to be used together with the -XX:UnlockDiagnosticVMOptions option that unlocks diagnostic JVM options.
默认情况下，此选项处于禁用状态，不会打印程序集代码。-XX:+printpassembly选项必须与-XX:UnlockDiagnosticVMOptions选项一起使用，该选项将解除对诊断JVM选项的锁定。

## -XX:+PrintCompilation
Enables verbose diagnostic output from the JVM by printing a message to the console every time a method is compiled. This enables you to see which methods actually get compiled. By default, this option is disabled and diagnostic output is not printed.
通过以下方式启用从JVM的详细诊断输出

You can also log compilation activity to a file by using the -XX:+LogCompilation option.
还可以使用-XX:+log compilation选项将编译活动记录到文件中。


## -XX:+PrintInlining
Enables printing of inlining decisions. This enables you to see which methods are getting inlined.
启用内联决策的打印。这使您能够看到哪些方法是内联的。

By default, this option is disabled and inlining information is not printed. The -XX:+PrintInlining option has to be used together with the -XX:+UnlockDiagnosticVMOptions option that unlocks diagnostic JVM options.
默认情况下，此选项处于禁用状态，不会打印内联信息。-XX:+printinline选项必须与-XX:+UnlockDiagnosticVMOptions选项一起使用，后者将解除对诊断JVM选项的锁定。

## -XX:ReservedCodeCacheSize=size
Sets the maximum code cache size (in bytes) for JIT-compiled code. Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes. The default maximum code cache size is 240 MB; if you disable tiered compilation with the option -XX:-TieredCompilation, then the default size is 48 MB. This option has a limit of 2 GB; otherwise, an error is generated. The maximum code cache size should not be less than the initial code cache size; see the option -XX:InitialCodeCacheSize. This option is equivalent to -Xmaxjitcodesize.
为JIT编译代码设置最大代码缓存大小（以字节为单位）。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。默认最大代码缓存大小为240 MB；如果禁用选项-XX:-TiErdEd汇编的分层编译，则默认大小为48 MB。此选项的限制为2 GB；否则，将生成错误。最大代码缓存大小不应小于初始代码缓存大小；请参阅选项-XX：InitialCodeCacheSize。此选项相当于-Xmaxjitcodesize。

## -XX:RTMAbortRatio=abort_ratio
The RTM abort ratio is specified as a percentage (%) of all executed RTM transactions. If a number of aborted transactions becomes greater than this ratio, then the compiled code will be deoptimized. This ratio is used when the -XX:+UseRTMDeopt option is enabled. The default value of this option is 50. This means that the compiled code will be deoptimized if 50% of all transactions are aborted.
RTM中止比率指定为所有执行的RTM事务的百分比。如果中止的事务数大于此比率，则编译的代码将被取消优化。此比率在启用-XX:+UseRTMDeopt选项时使用。此选项的默认值为50。这意味着，如果50%的事务被中止，编译后的代码将被取消优化。

## -XX:RTMRetryCount=number_of_retries
RTM locking code will be retried, when it is aborted or busy, the number of times specified by this option before falling back to the normal locking mechanism. The default value for this option is 5. The -XX:UseRTMLocking option must be enabled.
当RTM锁定代码被中止或繁忙时，将重试该选项在返回正常锁定机制之前指定的次数。此选项的默认值为5。必须启用-XX:UseRTMLocking选项。

## -XX:-TieredCompilation
Disables the use of tiered compilation. By default, this option is enabled. Only the Java HotSpot Server VM supports this option.
禁止使用分层编译。默认情况下，此选项处于启用状态。只有Java热点服务器VM支持此选项。

## -XX:+UseAES
Enables hardware-based AES intrinsics for Intel, AMD, and SPARC hardware. Intel Westmere (2010 and newer), AMD Bulldozer (2011 and newer), and SPARC (T4 and newer) are the supported hardware. UseAES is used in conjunction with UseAESIntrinsics.
为英特尔、AMD和SPARC硬件提供基于硬件的AES内核。英特尔韦斯特米尔（2010和较新），AMD推土机（2011和更新），和SPARC（T4和更新）是支持的硬件。UseAES与useasentrinsics一起使用。


## -XX:+UseAESIntrinsics
UseAES and UseAESIntrinsics flags are enabled by default and are supported only for Java HotSpot Server VM 32-bit and 64-bit. To disable hardware-based AES intrinsics, specify -XX:-UseAES -XX:-UseAESIntrinsics. For example, to enable hardware AES, use the following flags:
UseAES和useasentrinsics标志在默认情况下是启用的，并且仅支持Java热点服务器VM 32位和64位。要禁用基于硬件的AES内部函数，请指定-XX:-UseAES-XX:-useasintrinsics。例如，要启用硬件AES，请使用以下标志：

    -XX:+UseAES -XX:+UseAESIntrinsics
To support UseAES and UseAESIntrinsics flags for 32-bit and 64-bit use -server option to choose Java HotSpot Server VM. These flags are not supported on Client VM.
要支持32位和64位的UseAES和useasintrinsics标志，请使用-server选项选择Java热点服务器虚拟机。客户端虚拟机不支持这些标志。

## -XX:+UseCodeCacheFlushing
Enables flushing of the code cache before shutting down the compiler. This option is enabled by default. To disable flushing of the code cache before shutting down the compiler, specify -XX:-UseCodeCacheFlushing.
允许在关闭编译器之前刷新代码缓存。默认情况下，此选项处于启用状态。要在关闭编译器之前禁用代码缓存刷新，请指定-XX:-UseCodeCacheFlushing。

## -XX:+UseCondCardMark
Enables checking of whether the card is already marked before updating the card table. This option is disabled by default and should only be used on machines with multiple sockets, where it will increase performance of Java applications that rely heavily on concurrent operations. Only the Java HotSpot Server VM supports this option.
启用在更新卡表之前检查卡是否已标记。此选项在默认情况下是禁用的，应该只在具有多个套接字的计算机上使用，因为它将提高严重依赖并发操作的Java应用程序的性能。只有Java热点服务器VM支持此选项。

## -XX:+UseRTMDeopt
Auto-tunes RTM locking depending on the abort ratio. This ratio is specified by -XX:RTMAbortRatio option. If the number of aborted transactions exceeds the abort ratio, then the method containing the lock will be deoptimized and recompiled with all locks as normal locks. This option is disabled by default. The -XX:+UseRTMLocking option must be enabled.
自动调谐RTM锁定取决于中止比。此比率由-XX:rtmabortario选项指定。如果中止的事务数超过中止比率，则包含锁的方法将被取消优化，并将所有锁重新编译为普通锁。默认情况下禁用此选项。必须启用-XX:+UseRTMLocking选项。

## -XX:+UseRTMLocking
Generate Restricted Transactional Memory (RTM) locking code for all inflated locks, with the normal locking mechanism as the fallback handler. This option is disabled by default. Options related to RTM are only available for the Java HotSpot Server VM on x86 CPUs that support Transactional Synchronization Extensions (TSX).
为所有膨胀的锁生成受限事务内存（RTM）锁定代码，使用常规锁定机制作为回退处理程序。默认情况下禁用此选项。与RTM相关的选项仅适用于支持事务同步扩展（TSX）的x86 cpu上的Java热点服务器VM。


RTM is part of Intel's TSX, which is an x86 instruction set extension and facilitates the creation of multithreaded applications. RTM introduces the new instructions XBEGIN, XABORT, XEND, and XTEST. The XBEGIN and XEND instructions enclose a set of instructions to run as a transaction. If no conflict is found when running the transaction, the memory and register modifications are committed together at the XEND instruction. The XABORT instruction can be used to explicitly abort a transaction and the XEND instruction to check if a set of instructions are being run in a transaction.
RTM是Intel的TSX的一部分，它是x86指令集扩展，有助于创建多线程应用程序。RTM引入了新的指令XBEGIN、XABORT、XEND和XTEST。XBEGIN和XEND指令包含一组要作为事务运行的指令。如果在运行事务时未发现冲突，则在XEND指令中将内存和寄存器修改一起提交。XABORT指令可用于显式中止事务，XEND指令可用于检查事务中是否正在运行一组指令。

A lock on a transaction is inflated when another thread tries to access the same transaction, thereby blocking the thread that did not originally request access to the transaction. RTM requires that a fallback set of operations be specified in case a transaction aborts or fails. An RTM lock is a lock that has been delegated to the TSX's system.
当另一个线程试图访问同一个事务时，事务上的锁会膨胀，从而阻止最初未请求访问该事务的线程。RTM要求在事务中止或失败时指定一组回退操作。RTM锁是已委派给TSX系统的锁。

RTM improves performance for highly contended locks with low conflict in a critical region (which is code that must not be accessed by more than one thread concurrently). RTM also improves the performance of coarse-grain locking, which typically does not perform well in multithreaded applications. (Coarse-grain locking is the strategy of holding locks for long periods to minimize the overhead of taking and releasing locks, while fine-grained locking is the strategy of trying to achieve maximum parallelism by locking only when necessary and unlocking as soon as possible.) Also, for lightly contended locks that are used by different threads, RTM can reduce false cache line sharing, also known as cache line ping-pong. This occurs when multiple threads from different processors are accessing different resources, but the resources share the same cache line. As a result, the processors repeatedly invalidate the cache lines of other processors, which forces them to read from main memory instead of their cache.
RTM提高了关键区域（即不能由多个线程同时访问的代码）中冲突较少的高争用锁的性能。RTM还提高了粗粒度锁的性能，而粗粒度锁在多线程应用程序中通常性能不佳。（粗粒度锁定是一种长期持有锁的策略，以尽量减少获取和释放锁的开销，而细粒度锁定则是尽量在必要的时候锁定并尽量解锁）来达到最大并行性的策略，RTM可以减少伪缓存线共享，也称为缓存线乒乓。当来自不同处理器的多个线程访问不同的资源，但资源共享同一缓存线时，就会发生这种情况。因此，处理器会反复使其他处理器的缓存线失效，从而迫使它们从主存而不是缓存中读取数据。

## -XX:+UseSHA
Enables hardware-based intrinsics for SHA crypto hash functions for SPARC hardware. UseSHA is used in conjunction with the UseSHA1Intrinsics, UseSHA256Intrinsics, and UseSHA512Intrinsics options.
为SPARC硬件启用SHAR-CONTITH散列函数的基于硬件的本质。UseSHA与UseSHA1Intrinsics、UseSHA256Intrinsics和UseSHA512Intrinsics选项一起使用。

The UseSHA and UseSHA*Intrinsics flags are enabled by default, and are supported only for Java HotSpot Server VM 64-bit on SPARC T4 and newer.
默认情况下，启用UseSHA和UESHA*PrimeNICs标志，并且仅支持SPARC T4和更新的Java热点服务器VM 64位。

This feature is only applicable when using the sun.security.provider.Sun provider for SHA operations.
此功能仅在使用sun.security.provider.sun provider进行SHA操作时适用。


To disable all hardware-based SHA intrinsics, specify -XX:-UseSHA. To disable only a particular SHA intrinsic, use the appropriate corresponding option. For example: -XX:-UseSHA256Intrinsics.
要禁用所有基于硬件的SHA内部函数，请指定-XX:-UseSHA。要仅禁用特定的SHA内在函数，请使用相应的选项。例如：-XX:-usesa256intrinsics。


## -XX:+UseSHA1Intrinsics
Enables intrinsics for SHA-1 crypto hash function.
为SHA-1加密哈希函数启用内部函数。


## -XX:+UseSHA256Intrinsics
Enables intrinsics for SHA-224 and SHA-256 crypto hash functions.
为SHA-224和SHA-256加密哈希函数启用内部函数。


## -XX:+UseSHA512Intrinsics
Enables intrinsics for SHA-384 and SHA-512 crypto hash functions.
为SHA-384和SHA-512加密哈希函数启用内部函数。


## -XX:+UseSuperWord
Enables the transformation of scalar operations into superword operations. This option is enabled by default. To disable the transformation of scalar operations into superword operations, specify -XX:-UseSuperWord. Only the Java HotSpot Server VM supports this option.
允许将标量操作转换为超级字操作。默认情况下，此选项处于启用状态。若要禁用将标量操作转换为超级字操作，请指定-XX:-UseSuperWord。只有Java热点服务器VM支持此选项。

---

# Advanced Serviceability Options 高级可维护性选项
These options provide the ability to gather system information and perform extensive debugging.
这些选项提供了收集系统信息和执行大量调试的能力。


## -XX:+ExtendedDTraceProbes
Enables additional dtrace tool probes that impact the performance. By default, this option is disabled and dtrace performs only standard probes.
启用影响性能的其他dtrace工具探测。默认情况下，此选项被禁用，dtrace只执行标准探测。


## -XX:+HeapDumpOnOutOfMemoryError
Enables the dumping of the Java heap to a file in the current directory by using the heap profiler (HPROF) when a java.lang.OutOfMemoryError exception is thrown. You can explicitly set the heap dump file path and name using the -XX:HeapDumpPath option. By default, this option is disabled and the heap is not dumped when an OutOfMemoryError exception is thrown.
启用在引发Java.lang.OutOfMemoryError异常时使用堆探查器（HPROF）将Java堆转储到当前目录中的文件。可以显式设置堆转储f


## -XX:HeapDumpPath=path
Sets the path and file name for writing the heap dump provided by the heap profiler (HPROF) when the -XX:+HeapDumpOnOutOfMemoryError option is set. By default, the file is created in the current working directory, and it is named java_pidpid.hprof where pid is the identifier of the process that caused the error. The following example shows how to set the default file explicitly (%p represents the current process identificator):

## -XX:HeapDumpPath=./java_pid%p.hprof
The following example shows how to set the heap dump file to /var/log/java/java_heapdump.hprof:

    -XX:HeapDumpPath=/var/log/java/java_heapdump.hprof


## -XX:LogFile=path
Sets the path and file name where log data is written. By default, the file is created in the current working directory, and it is named hotspot.log.
设置写入日志数据的路径和文件名。默认情况下，文件是在当前工作目录中创建的，名为hotspot.log。

The following example shows how to set the log file to /var/log/java/hotspot.log:
下面的示例演示如何将日志文件设置为/var/log/java/hotspot.log：


    -XX:LogFile=/var/log/java/hotspot.log
-XX:+PrintClassHistogram
Enables printing of a class instance histogram after a Control+C event (SIGTERM). By default, this option is disabled.
启用在控件+C事件（SIGTERM）之后打印类实例直方图。默认情况下，此选项处于禁用状态。


Setting this option is equivalent to running the jmap -histo command, or the jcmd pid GC.class_histogram command, where pid is the current Java process identifier.
设置此选项相当于运行jmap-histo命令或jcmd pid GC.class_histogram命令，其中pid是当前Java进程标识符。


## -XX:+PrintConcurrentLocks
Enables printing of java.util.concurrent locks after a Control+C event (SIGTERM). By default, this option is disabled.
启用在Control+C事件（SIGTERM）之后打印java.util.concurrent锁。默认情况下，此选项处于禁用状态。

Setting this option is equivalent to running the jstack -l command or the jcmd pid Thread.print -l command, where pid is the current Java process identifier.
设置此选项相当于运行jstack-l命令或jcmd pid Thread.print -l 命令，其中pid是当前Java进程标识符。

## -XX:+UnlockDiagnosticVMOptions
Unlocks the options intended for diagnosing the JVM. By default, this option is disabled and diagnostic options are not available.
解锁用于诊断JVM的选项。默认情况下，此选项被禁用，诊断选项不可用。

---

# Advanced Garbage Collection Options 高级垃圾收集选项

These options control how garbage collection (GC) is performed by the Java HotSpot VM.
这些选项控制Java热点VM如何执行垃圾收集（GC）。


## -XX:+AggressiveHeap
Enables Java heap optimization. This sets various parameters to be optimal for long-running jobs with intensive memory allocation, based on the configuration of the computer (RAM and CPU). By default, the option is disabled and the heap is not optimized.
启用Java堆优化。这将根据计算机（RAM和CPU）的配置，为具有密集内存分配的长时间运行作业设置各种最佳参数。默认情况下，该选项被禁用，堆未优化。

## -XX:+AlwaysPreTouch
Enables touching of every page on the Java heap during JVM initialization. This gets all pages into the memory before entering the main() method. The option can be used in testing to simulate a long-running system with all virtual memory mapped to physical memory. By default, this option is disabled and all pages are committed as JVM heap space fills.
允许在JVM初始化期间触摸Java堆上的每个页面。这会在输入main（）方法之前将所有页都放入内存。此选项可用于测试以模拟所有虚拟内存映射到物理内存的长时间运行系统。默认情况下，此选项处于禁用状态，所有页面都将作为JVM堆空间填充提交。

## -XX:+CMSClassUnloadingEnabled
Enables class unloading when using the concurrent mark-sweep (CMS) garbage collector. This option is enabled by default. To disable class unloading for the CMS garbage collector, specify -XX:-CMSClassUnloadingEnabled.
使用并发标记扫描（CMS）垃圾收集器时启用类卸载。默认情况下，此选项处于启用状态。要禁用CMS垃圾收集器的类卸载，请指定-XX:-CMSClassUnloadingEnabled。


## -XX:CMSExpAvgFactor=percent
Sets the percentage of time (0 to 100) used to weight the current sample when computing exponential averages for the concurrent collection statistics. By default, the exponential averages factor is set to 25%. The following example shows how to set the factor to 15%:
设置在计算并发集合统计信息的指数平均值时用于加权当前样本的时间百分比（0到100）。默认情况下，指数平均系数设置为25%。下面的示例演示如何将因子设置为15%：

    -XX:CMSExpAvgFactor=15
    
## -XX:CMSInitiatingOccupancyFraction=percent
Sets the percentage of the old generation occupancy (0 to 100) at which to start a CMS collection cycle. The default value is set to -1. Any negative value (including the default) implies that -XX:CMSTriggerRatio is used to define the value of the initiating occupancy fraction.
设置开始CMS收集周期的旧代占用率（0到100）。默认值设置为-1。任何负值（包括默认值）都意味着-XX:cmStrigerRatio用于定义初始占用率的值。

The following example shows how to set the occupancy fraction to 20%:
下面的示例演示如何将占用率设置为20%：

    -XX:CMSInitiatingOccupancyFraction=20
    
## -XX:+CMSScavengeBeforeRemark
Enables scavenging attempts before the CMS remark step. By default, this option is disabled.
在CMS备注步骤之前启用清除尝试。默认情况下，此选项处于禁用状态。

## -XX:CMSTriggerRatio=percent
Sets the percentage (0 to 100) of the value specified by -XX:MinHeapFreeRatio that is allocated before a CMS collection cycle commences. The default value is set to 80%.
设置在CMS收集周期开始之前由-XX:MinHeapFreeRatio指定的值的百分比（0到100）。默认值设置为80%。

The following example shows how to set the occupancy fraction to 75%:
下面的示例演示如何将占用率设置为75%：

    -XX:CMSTriggerRatio=75
    
## -XX:ConcGCThreads=threads
Sets the number of threads used for concurrent GC. The default value depends on the number of CPUs available to the JVM.
设置用于并发GC的线程数。默认值取决于JVM可用的cpu数量。

For example, to set the number of threads for concurrent GC to 2, specify the following option:
例如，要将并发GC的线程数设置为2，请指定以下选项：

    -XX:ConcGCThreads=2
    
    
## -XX:+DisableExplicitGC
Enables the option that disables processing of calls to System.gc(). This option is disabled by default, meaning that calls to System.gc() are processed. If processing of calls to System.gc() is disabled, the JVM still performs GC when necessary.
启用禁用处理对System.gc（）的调用的选项。默认情况下，此选项处于禁用状态，这意味着将处理对System.gc（）的调用。如果对System.gc（）调用的处理被禁用，JVM仍会在必要时执行gc。

## -XX:+ExplicitGCInvokesConcurrent
Enables invoking of concurrent GC by using the System.gc() request. This option is disabled by default and can be enabled only together with the -XX:+UseConcMarkSweepGC option.
通过使用System.GC（）请求启用并发GC的调用。默认情况下，此选项处于禁用状态，只能与-XX:+UseConcMarkSweepGC选项一起启用。

## -XX:+ExplicitGCInvokesConcurrentAndUnloadsClasses
Enables invoking of concurrent GC by using the System.gc() request and unloading of classes during the concurrent GC cycle. This option is disabled by default and can be enabled only together with the -XX:+UseConcMarkSweepGC option.
通过在并发GC周期中使用System.GC（）请求和卸载类来启用并发GC的调用。默认情况下，此选项处于禁用状态，只能与-XX:+UseConcMarkSweepGC选项一起启用。

## -XX:G1HeapRegionSize=size
Sets the size of the regions into which the Java heap is subdivided when using the garbage-first (G1) collector. The value can be between 1 MB and 32 MB. The default region size is determined ergonomically based on the heap size.
设置在使用垃圾优先（G1）收集器时Java堆细分到的区域的大小。该值可以介于1 MB和32 MB之间。默认区域大小是根据堆大小根据人体工程学确定的。

The following example shows how to set the size of the subdivisions to 16 MB:
下面的示例演示如何将子划分的大小设置为16 MB：

    -XX:G1HeapRegionSize=16m
    
## -XX:+G1PrintHeapRegions
Enables the printing of information about which regions are allocated and which are reclaimed by the G1 collector. By default, this option is disabled.
启用打印有关哪些区域被分配以及哪些区域被G1收集器回收的信息。默认情况下，此选项处于禁用状态。

## -XX:G1ReservePercent=percent
Sets the percentage of the heap (0 to 50) that is reserved as a false ceiling to reduce the possibility of promotion failure for the G1 collector. By default, this option is set to 10%.
设置保留为假上限的堆的百分比（0到50），以减少G1收集器升级失败的可能性。默认情况下，此选项设置为10%。

The following example shows how to set the reserved heap to 20%:
下面的示例演示如何将保留堆设置为20%：

    -XX:G1ReservePercent=20
    
## -XX:InitialHeapSize=size
Sets the initial size (in bytes) of the memory allocation pool. This value must be either 0, or a multiple of 1024 and greater than 1 MB. Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes. The default value is chosen at runtime based on system configuration. See the section "Ergonomics" in Java SE HotSpot Virtual Machine Garbage Collection Tuning Guide at http://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/index.html.
设置内存分配池的初始大小（字节）。此值必须为0或1024的倍数且大于1 MB。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。默认值在运行时根据系统配置选择。请参阅http://docs.oracle.com/Java SE/8/docs/technotes/guides/vm/gctuning/index.html上Java SE HotSpot虚拟机垃圾收集优化指南中的“人体工程学”部分。

The following examples show how to set the size of allocated memory to 6 MB using various units:
下面的示例演示如何使用不同的单元将分配的内存大小设置为6MB：

    -XX:InitialHeapSize=6291456
    -XX:InitialHeapSize=6144k
    -XX:InitialHeapSize=6m
If you set this option to 0, then the initial size will be set as the sum of the sizes allocated for the old generation and the young generation. The size of the heap for the young generation can be set using the -XX:NewSize option.
如果将此选项设置为0，则初始大小将设置为分配给旧代和新代的大小之和。可以使用-XX:NewSize选项设置年轻一代的堆大小。

## -XX:InitialSurvivorRatio=ratio
Sets the initial survivor space ratio used by the throughput garbage collector (which is enabled by the -XX:+UseParallelGC and/or -XX:+UseParallelOldGC options). Adaptive sizing is enabled by default with the throughput garbage collector by using the -XX:+UseParallelGC and -XX:+UseParallelOldGC options, and survivor space is resized according to the application behavior, starting with the initial value. If adaptive sizing is disabled (using the -XX:-UseAdaptiveSizePolicy option), then the -XX:SurvivorRatio option should be used to set the size of the survivor space for the entire execution of the application.
设置吞吐量垃圾收集器使用的初始幸存者空间比率（由-XX:+UseParallelGC和/或-XX:+UseParallelOldGC选项启用）。默认情况下，通过使用-XX:+UseParallelGC和-XX:+UseParallelOldGC选项，吞吐量垃圾收集器启用自适应大小调整，幸存者空间从初始值开始根据应用程序行为调整大小。如果禁用了自适应大小调整（使用-XX:-UseAdaptiveSizePolicy选项），则应使用-XX:survivoratio选项为应用程序的整个执行设置幸存者空间的大小。

The following formula can be used to calculate the initial size of survivor space (S) based on the size of the young generation (Y), and the initial survivor space ratio (R):
以下公式可用于根据年轻一代的大小（Y）和初始幸存者空间比（R）计算幸存者空间的初始大小：


S=Y/(R+2)
The 2 in the equation denotes two survivor spaces. The larger the value specified as the initial survivor space ratio, the smaller the initial survivor space size.
方程中的2表示两个幸存者空间。指定为初始幸存者空间比的值越大，初始幸存者空间大小越小。

By default, the initial survivor space ratio is set to 8. If the default value for the young generation space size is used (2 MB), the initial size of the survivor space will be 0.2 MB.
默认情况下，初始幸存者空间比设置为8。如果使用年轻一代空间大小的默认值（2 MB），则幸存者空间的初始大小将为0.2 MB。

The following example shows how to set the initial survivor space ratio to 4:
以下示例说明如何将初始幸存者空间比设置为4：

    -XX:InitialSurvivorRatio=4
    
## -XX:InitiatingHeapOccupancyPercent=percent
Sets the percentage of the heap occupancy (0 to 100) at which to start a concurrent GC cycle. It is used by garbage collectors that trigger a concurrent GC cycle based on the occupancy of the entire heap, not just one of the generations (for example, the G1 garbage collector).
设置堆占用率的百分比（0到100），在该百分比上启动并发GC循环。它由垃圾收集器使用，垃圾收集器根据整个堆的占用率触发并发GC循环，而不仅仅是一代（例如，G1垃圾收集器）。

By default, the initiating value is set to 45%. A value of 0 implies nonstop GC cycles. The following example shows how to set the initiating heap occupancy to 75%:
默认情况下，初始值设置为45%。值为0表示不停止GC循环。下面的示例演示如何将初始堆占用率设置为75%：

    -XX:InitiatingHeapOccupancyPercent=75
    
## -XX:MaxGCPauseMillis=time
Sets a target for the maximum GC pause time (in milliseconds). This is a soft goal, and the JVM will make its best effort to achieve it. By default, there is no maximum pause time value.
设置最大GC暂停时间的目标（以毫秒为单位）。这是一个软目标，JVM将尽最大努力实现它。默认情况下，没有最大暂停时间值。

The following example shows how to set the maximum target pause time to 500 ms:
下面的示例演示如何将最大目标暂停时间设置为500毫秒：

    -XX:MaxGCPauseMillis=500
    
    
## -XX:MaxHeapSize=size
Sets the maximum size (in byes) of the memory allocation pool. This value must be a multiple of 1024 and greater than 2 MB. Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes. The default value is chosen at runtime based on system configuration. For server deployments, -XX:InitialHeapSize and -XX:MaxHeapSize are often set to the same value. See the section "Ergonomics" in Java SE HotSpot Virtual Machine Garbage Collection Tuning Guide at http://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/index.html.
设置内存分配池的最大大小（在“是”）。此值必须是1024的倍数且大于2 MB。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。默认值在运行时根据系统配置选择。对于服务器部署，-XX:InitialHeapSize和-XX:MaxHeapSize通常设置为相同的值。请参阅http://docs.oracle.com/Java SE/8/docs/technotes/guides/vm/gctuning/index.html上Java SE HotSpot虚拟机垃圾收集优化指南中的“人体工程学”部分。

The following examples show how to set the maximum allowed size of allocated memory to 80 MB using various units:
下面的示例演示如何使用不同的单元将分配的内存的最大允许大小设置为80 MB：


    -XX:MaxHeapSize=83886080
    -XX:MaxHeapSize=81920k
    -XX:MaxHeapSize=80m
On Oracle Solaris 7 and Oracle Solaris 8 SPARC platforms, the upper limit for this value is approximately 4,000 MB minus overhead amounts. On Oracle Solaris 2.6 and x86 platforms, the upper limit is approximately 2,000 MB minus overhead amounts. On Linux platforms, the upper limit is approximately 2,000 MB minus overhead amounts.
在Oracle Solaris 7和Oracle Solaris 8 SPARC平台上，这个值的上限是大约4000 MB。在Oracle Solaris 2.6和X86平台上，上限约为2000 MB。在Linux平台上，上限约为2000 MB。

The -XX:MaxHeapSize option is equivalent to -Xmx.
-XX:MaxHeapSize选项相当于-Xmx。

## -XX:MaxHeapFreeRatio=percent
Sets the maximum allowed percentage of free heap space (0 to 100) after a GC event. If free heap space expands above this value, then the heap will be shrunk. By default, this value is set to 70%.
设置GC事件后最大允许百分比的空闲堆空间（0到100）。如果可用堆空间扩展到此值之上，则堆将缩小。默认情况下，此值设置为70%。

The following example shows how to set the maximum free heap ratio to 75%:
下面的示例演示如何将最大空闲堆比率设置为75%：

    -XX:MaxHeapFreeRatio=75
    -XX:MaxMetaspaceSize=size
Sets the maximum amount of native memory that can be allocated for class metadata. By default, the size is not limited. The amount of metadata for an application depends on the application itself, other running applications, and the amount of memory available on the system.
设置可分配给类元数据的本机内存的最大数量。默认情况下，大小不受限制。应用程序的元数据量取决于应用程序本身、其他正在运行的应用程序以及系统上可用的内存量。

The following example shows how to set the maximum class metadata size to 256 MB:
下面的示例演示如何将最大类元数据大小设置为256 MB：

    -XX:MaxMetaspaceSize=256m
    -XX:MaxNewSize=size
Sets the maximum size (in bytes) of the heap for the young generation (nursery). The default value is set ergonomically.
为年轻一代（托儿所）设置堆的最大大小（以字节为单位）。默认值是根据人体工程学设置的。

    -XX:MaxTenuringThreshold=threshold
Sets the maximum tenuring threshold for use in adaptive GC sizing. The largest value is 15. The default value is 15 for the parallel (throughput) collector, and 6 for the CMS collector.
设置用于自适应GC大小调整的最大延展阈值。最大值是15。并行（吞吐量）收集器的默认值为15，CMS收集器的默认值为6。

The following example shows how to set the maximum tenuring threshold to 10:
下面的示例演示如何将最大停留阈值设置为10：

    -XX:MaxTenuringThreshold=10
    -XX:MetaspaceSize=size
Sets the size of the allocated class metadata space that will trigger a garbage collection the first time it is exceeded. This threshold for a garbage collection is increased or decreased depending on the amount of metadata used. The default size depends on the platform.
设置分配的类元数据空间的大小，该空间将在第一次超过垃圾收集时触发垃圾收集。垃圾收集的此阈值根据所使用的元数据的数量增加或减少。默认大小取决于平台。


## -XX:MinHeapFreeRatio=percent
Sets the minimum allowed percentage of free heap space (0 to 100) after a GC event. If free heap space falls below this value, then the heap will be expanded. By default, this value is set to 40%.
设置GC事件后允许的最小可用堆空间百分比（0到100）。如果可用堆空间低于此值，则堆将被扩展。默认情况下，此值设置为40%。

The following example shows how to set the minimum free heap ratio to 25%:
下面的示例演示如何将最小可用堆比率设置为25%：

    -XX:MinHeapFreeRatio=25
    -XX:NewRatio=ratio
Sets the ratio between young and old generation sizes. By default, this option is set to 2. The following example shows how to set the young/old ratio to 1:
设置年轻代和旧代大小之间的比率。默认情况下，此选项设置为2。下面的示例演示如何将新旧比率设置为1：

    -XX:NewRatio=1
    -XX:NewSize=size
Sets the initial size (in bytes) of the heap for the young generation (nursery). Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes.
设置新一代（托儿所）堆的初始大小（字节）。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。

The young generation region of the heap is used for new objects. GC is performed in this region more often than in other regions. If the size for the young generation is too low, then a large number of minor GCs will be performed. If the size is too high, then only full GCs will be performed, which can take a long time to complete. Oracle recommends that you keep the size for the young generation between a half and a quarter of the overall heap size.
堆的年轻一代区域用于新对象。GC在这个区域的执行频率高于其他区域。如果年轻一代的规模太小，那么将执行大量的小型地面军事系统。如果大小太大，则只执行完整的地面军事系统，这可能需要很长时间才能完成。Oracle建议您将年轻一代的大小保持在整个堆大小的一半到四分之一之间。

The following examples show how to set the initial size of young generation to 256 MB using various units:
以下示例说明如何使用各种单位将年轻一代的初始大小设置为256 MB：

    -XX:NewSize=256m
    -XX:NewSize=262144k
    -XX:NewSize=268435456
The -XX:NewSize option is equivalent to -Xmn.
-XX:NewSize选项相当于-Xmn。

## -XX:ParallelGCThreads=threads
Sets the number of threads used for parallel garbage collection in the young and old generations. The default value depends on the number of CPUs available to the JVM.
设置新旧代中用于并行垃圾收集的线程数。默认值取决于JVM可用的cpu数量。

For example, to set the number of threads for parallel GC to 2, specify the following option:

    -XX:ParallelGCThreads=2
    
## -XX:+ParallelRefProcEnabled
Enables parallel reference processing. By default, this option is disabled.
启用并行引用处理。默认情况下，此选项处于禁用状态。

## -XX:+PrintAdaptiveSizePolicy
Enables printing of information about adaptive generation sizing. By default, this option is disabled.
启用打印有关自适应生成大小调整的信息。默认情况下，此选项处于禁用状态。
启用打印自上次暂停（例如GC暂停）以来经过的时间。默认情况下，此选项处于禁用状态。


## -XX:+PrintGC
Enables printing of messages at every GC. By default, this option is disabled.
允许在每个GC上打印消息。默认情况下，此选项处于禁用状态。

## -XX:+PrintGCApplicationConcurrentTime
Enables printing of how much time elapsed since the last pause (for example, a GC pause). By default, this option is disabled.
启用打印自上次暂停（例如GC暂停）以来经过的时间。默认情况下，此选项处于禁用状态。

## -XX:+PrintGCApplicationStoppedTime
Enables printing of how much time the pause (for example, a GC pause) lasted. By default, this option is disabled.
允许打印暂停（例如GC暂停）持续的时间。默认情况下，此选项处于禁用状态。

## -XX:+PrintGCDateStamps
Enables printing of a date stamp at every GC. By default, this option is disabled.
启用在每个GC上打印日期戳。默认情况下，此选项处于禁用状态。

## -XX:+PrintGCDetails
Enables printing of detailed messages at every GC. By default, this option is disabled.
允许在每个GC上打印详细消息。默认情况下，此选项处于禁用状态。


## -XX:+PrintGCTaskTimeStamps
Enables printing of time stamps for every individual GC worker thread task. By default, this option is disabled.
启用为每个GC工作线程任务打印时间戳。默认情况下，此选项处于禁用状态。

## -XX:+PrintGCTimeStamps
Enables printing of time stamps at every GC. By default, this option is disabled.
启用在每个GC上打印时间戳。默认情况下，此选项处于禁用状态。

## -XX:+PrintStringDeduplicationStatistics
Prints detailed deduplication statistics. By default, this option is disabled. See the -XX:+UseStringDeduplication option.
打印详细的重复数据消除统计信息。默认情况下，此选项处于禁用状态。请参阅-XX:+UseStringDeduplication选项。

## -XX:+PrintTenuringDistribution
Enables printing of tenuring age information. The following is an example of the output:
启用寿命信息的打印。以下是输出的示例：

    Desired survivor size 48286924 bytes, new threshold 10 (max 10)
    - age 1: 28992024 bytes, 28992024 total
    - age 2: 1366864 bytes, 30358888 total
    - age 3: 1425912 bytes, 31784800 total
    ...
Age 1 objects are the youngest survivors (they were created after the previous scavenge, survived the latest scavenge, and moved from eden to survivor space). Age 2 objects have survived two scavenges (during the second scavenge they were copied from one survivor space to the next). And so on.
年龄1的物体是最年轻的幸存者（它们是在上一次食腐之后创建的，在最近一次食腐之后幸存下来，并从伊甸园移动到幸存者空间）。年龄2的物体存活了两次食腐（在第二次食腐期间，它们被从一个幸存者空间复制到下一个幸存者空间）。等等。

In the preceding example, 28 992 024 bytes survived one scavenge and were copied from eden to survivor space, 1 366 864 bytes are occupied by age 2 objects, etc. The third value in each row is the cumulative size of objects of age n or less.
在前面的示例中，28 992 024字节在一次清除后存活，并从eden复制到幸存者空间，1366 864字节被年龄2的对象占用，等等。每行中的第三个值是年龄n或更小的对象的累积大小。

By default, this option is disabled.
默认情况下，此选项处于禁用状态。

## -XX:+ScavengeBeforeFullGC
Enables GC of the young generation before each full GC. This option is enabled by default. Oracle recommends that you do not disable it, because scavenging the young generation before a full GC can reduce the number of objects reachable from the old generation space into the young generation space. To disable GC of the young generation before each full GC, specify -XX:-ScavengeBeforeFullGC.
在每次完整GC之前启用年轻一代的GC。默认情况下，此选项处于启用状态。Oracle建议您不要禁用它，因为在完全GC之前清除年轻一代可以将可从旧一代空间访问的对象数量减少到年轻一代空间。要在每次完全GC之前禁用年轻一代的GC，请指定-XX:-ScavengeBeforeFullGC。

## -XX:SoftRefLRUPolicyMSPerMB=time
Sets the amount of time (in milliseconds) a softly reachable object is kept active on the heap after the last time it was referenced. The default value is one second of lifetime per free megabyte in the heap. The -XX:SoftRefLRUPolicyMSPerMB option accepts integer values representing milliseconds per one megabyte of the current heap size (for Java HotSpot Client VM) or the maximum possible heap size (for Java HotSpot Server VM). This difference means that the Client VM tends to flush soft references rather than grow the heap, whereas the Server VM tends to grow the heap rather than flush soft references. In the latter case, the value of the -Xmx option has a significant effect on how quickly soft references are garbage collected.
设置软访问对象上次被引用后在堆上保持活动状态的时间（以毫秒为单位）。默认值是堆中每空闲兆字节的生存期的1秒。-XX:SuffTrFrRuffRyMySyrMB选项接受整数值，每毫秒表示当前堆大小（对于Java热点客户机VM）或最大可能堆大小（对于Java热点服务器VM）。这种差异意味着客户机VM倾向于刷新软引用而不是增大堆，而服务器VM倾向于增大堆而不是刷新软引用。在后一种情况下，-Xmx选项的值对垃圾收集软引用的速度有很大影响。

The following example shows how to set the value to 2.5 seconds:
下面的示例演示如何将该值设置为2.5秒：

    -XX:SoftRefLRUPolicyMSPerMB=2500
    
## -XX:StringDeduplicationAgeThreshold=threshold
String objects reaching the specified age are considered candidates for deduplication. An object's age is a measure of how many times it has survived garbage collection. This is sometimes referred to as tenuring; see the -XX:+PrintTenuringDistribution option. Note that String objects that are promoted to an old heap region before this age has been reached are always considered candidates for deduplication. The default value for this option is 3. See the -XX:+UseStringDeduplication option.
达到指定期限的字符串对象被视为重复数据删除的候选对象。对象的年龄是衡量它在垃圾收集中存活了多少次的指标。这有时称为tenuring；请参阅-XX:+PrintTenuringDistribution选项。请注意，在达到此年龄之前提升到旧堆区域的字符串对象始终被视为重复数据删除的候选对象。此选项的默认值为3。请参阅-XX:+UseStringDeduplication选项。

## -XX:SurvivorRatio=ratio
Sets the ratio between eden space size and survivor space size. By default, this option is set to 8. The following example shows how to set the eden/survivor space ratio to 4:
设置伊甸园空间大小和幸存者空间大小之间的比率。默认情况下，此选项设置为8。以下示例说明如何将eden/survivor空间比率设置为4：

    -XX:SurvivorRatio=4
    

## -XX:TargetSurvivorRatio=percent
Sets the desired percentage of survivor space (0 to 100) used after young garbage collection. By default, this option is set to 50%.
设置年轻垃圾收集后使用的幸存者空间的所需百分比（0到100）。默认情况下，此选项设置为50%。


The following example shows how to set the target survivor space ratio to 30%:
下面的例子展示了如何将目标幸存者空间比率设置为30%：


    TargetSurvivorRatio=30
    
## -XX:TLABSize=size
Sets the initial size (in bytes) of a thread-local allocation buffer (TLAB). Append the letter k or K to indicate kilobytes, m or M to indicate megabytes, g or G to indicate gigabytes. If this option is set to 0, then the JVM chooses the initial size automatically.
设置线程本地分配缓冲区（TLAB）的初始大小（字节）。附加字母k或k表示千字节，m或m表示兆字节，g或g表示千兆字节。如果此选项设置为0，则JVM将自动选择初始大小。


The following example shows how to set the initial TLAB size to 512 KB:
下面的示例演示如何将初始TLAB大小设置为512 KB：


    -XX:TLABSize=512k
## -XX:+UseAdaptiveSizePolicy
Enables the use of adaptive generation sizing. This option is enabled by default. To disable adaptive generation sizing, specify -XX:-UseAdaptiveSizePolicy and set the size of the memory allocation pool explicitly (see the -XX:SurvivorRatio option).
启用自适应生成大小调整。默认情况下，此选项处于启用状态。要禁用自适应生成大小调整，请指定-XX:-UseAdaptiveSizePolicy并显式设置内存分配池的大小（请参阅-XX:survivoratio选项）。


## -XX:+UseCMSInitiatingOccupancyOnly
Enables the use of the occupancy value as the only criterion for initiating the CMS collector. By default, this option is disabled and other criteria may be used.
启用使用占用值作为启动CMS收集器的唯一标准。默认情况下，此选项被禁用，并且可以使用其他条件。


## -XX:+UseConcMarkSweepGC
Enables the use of the CMS garbage collector for the old generation. Oracle recommends that you use the CMS garbage collector when application latency requirements cannot be met by the throughput (-XX:+UseParallelGC) garbage collector. The G1 garbage collector (-XX:+UseG1GC) is another alternative.
为旧一代启用CMS垃圾收集器。Oracle建议在吞吐量（-XX:+usepallelgc）垃圾收集器无法满足应用程序延迟要求时使用CMS垃圾收集器。G1垃圾收集器（-XX:+UseG1GC）是另一种选择。

By default, this option is disabled and the collector is chosen automatically based on the configuration of the machine and type of the JVM. When this option is enabled, the -XX:+UseParNewGC option is automatically set and you should not disable it, because the following combination of options has been deprecated in JDK 8: -XX:+UseConcMarkSweepGC -XX:-UseParNewGC.
默认情况下，此选项处于禁用状态，并根据计算机的配置和JVM的类型自动选择收集器。启用此选项时，-XX:+UseParNewGC选项将自动设置，您不应禁用它，因为JDK 8中不赞成使用以下选项组合：-XX:+UseConcMarkSweepGC-XX:-UseParNewGC。


## -XX:+UseG1GC
Enables the use of the garbage-first (G1) garbage collector. It is a server-style garbage collector, targeted for multiprocessor machines with a large amount of RAM. It meets GC pause time goals with high probability, while maintaining good throughput. The G1 collector is recommended for applications requiring large heaps (sizes of around 6 GB or larger) with limited GC latency requirements (stable and predictable pause time below 0.5 seconds).
启用垃圾优先（G1）垃圾收集器的使用。它是一个服务器类型的垃圾收集器，目标是具有大量RAM的多处理器计算机。它以高概率满足GC暂停时间目标，同时保持良好的吞吐量。G1收集器推荐用于需要大堆（大小约为6gb或更大）且GC延迟要求有限（稳定且可预测的暂停时间低于0.5秒）的应用程序。

By default, this option is disabled and the collector is chosen automatically based on the configuration of the machine and type of the JVM.
默认情况下，此选项处于禁用状态，并根据计算机的配置和JVM的类型自动选择收集器。


## -XX:+UseGCOverheadLimit
Enables the use of a policy that limits the proportion of time spent by the JVM on GC before an OutOfMemoryError exception is thrown. This option is enabled, by default and the parallel GC will throw an OutOfMemoryError if more than 98% of the total time is spent on garbage collection and less than 2% of the heap is recovered. When the heap is small, this feature can be used to prevent applications from running for long periods of time with little or no progress. To disable this option, specify -XX:-UseGCOverheadLimit.
允许使用限制JVM在抛出OutOfMemoryError异常之前在GC上花费的时间比例的策略。默认情况下，此选项处于启用状态，如果在垃圾收集上花费的时间超过总时间的98%，并且恢复的堆不到2%，则并行GC将抛出OutOfMemory错误。当堆很小时，此功能可用于防止应用程序长时间运行而几乎没有进展。要禁用此选项，请指定-XX:-usegcoverdlimit。


## -XX:+UseNUMA
Enables performance optimization of an application on a machine with nonuniform memory architecture (NUMA) by increasing the application's use of lower latency memory. By default, this option is disabled and no optimization for NUMA is made. The option is only available when the parallel garbage collector is used (-XX:+UseParallelGC).
通过增加应用程序对低延迟内存的使用，在具有非均匀内存体系结构（NUMA）的计算机上实现应用程序的性能优化。默认情况下，此选项被禁用，并且没有对NUMA进行优化。此选项仅在使用并行垃圾收集器时可用（-XX:+usepallelgc）。


## -XX:+UseParallelGC
Enables the use of the parallel scavenge garbage collector (also known as the throughput collector) to improve the performance of your application by leveraging multiple processors.
允许使用并行清除垃圾收集器（也称为吞吐量收集器）通过利用多个处理器来提高应用程序的性能。


By default, this option is disabled and the collector is chosen automatically based on the configuration of the machine and type of the JVM. If it is enabled, then the -XX:+UseParallelOldGC option is automatically enabled, unless you explicitly disable it.
默认情况下，此选项处于禁用状态，并根据计算机的配置和JVM的类型自动选择收集器。如果启用了它，那么-XX:+usepalleloldgc选项将自动启用，除非显式禁用它。


## -XX:+UseParallelOldGC
Enables the use of the parallel garbage collector for full GCs. By default, this option is disabled. Enabling it automatically enables the -XX:+UseParallelGC option.
启用对完整gc使用并行垃圾收集器。默认情况下，此选项处于禁用状态。启用它会自动启用-XX:+usepallelgc选项。


## -XX:+UseParNewGC
Enables the use of parallel threads for collection in the young generation. By default, this option is disabled. It is automatically enabled when you set the -XX:+UseConcMarkSweepGC option. Using the -XX:+UseParNewGC option without the -XX:+UseConcMarkSweepGC option was deprecated in JDK 8.
允许在年轻一代中使用并行线程进行收集。默认情况下，此选项处于禁用状态。当您设置-XX:+UseConcMarkSweepGC选项时，它将自动启用。在JDK 8中不推荐使用-XX:+UseParNewGC选项而不使用-XX:+UseConcMarkSweepGC选项。


## -XX:+UseSerialGC
Enables the use of the serial garbage collector. This is generally the best choice for small and simple applications that do not require any special functionality from garbage collection. By default, this option is disabled and the collector is chosen automatically based on the configuration of the machine and type of the JVM.
启用串行垃圾收集器的使用。对于不需要垃圾收集任何特殊功能的小型简单应用程序，这通常是最佳选择。默认情况下，此选项处于禁用状态，并根据计算机的配置和JVM的类型自动选择收集器。


## -XX:+UseSHM
On Linux, enables the JVM to use shared memory to setup large pages.
在Linux上，使JVM能够使用共享内存来设置大页面。


For more information, see "Large Pages".

## -XX:+UseStringDeduplication
Enables string deduplication. By default, this option is disabled. To use this option, you must enable the garbage-first (G1) garbage collector. See the -XX:+UseG1GC option.
启用字符串重复数据消除。默认情况下，此选项处于禁用状态。要使用此选项，必须启用垃圾优先（G1）垃圾收集器。请参阅-XX:+UseG1GC选项。

String deduplication reduces the memory footprint of String objects on the Java heap by taking advantage of the fact that many String objects are identical. Instead of each String object pointing to its own character array, identical String objects can point to and share the same character array.
字符串重复数据消除利用了许多字符串对象是相同的这一事实，从而减少了Java堆中字符串对象的内存占用。不同于每个字符串对象指向自己的字符数组，相同的字符串对象可以指向并共享同一个字符数组。

## -XX:+UseTLAB
Enables the use of thread-local allocation blocks (TLABs) in the young generation space. This option is enabled by default. To disable the use of TLABs, specify -XX:-UseTLAB.
允许在年轻代空间中使用线程本地分配块（TLAB）。默认情况下，此选项处于启用状态。要禁用tlab的使用，请指定-XX:-UseTLAB。


---

# Deprecated and Removed Options 不推荐和删除的选项
                                 
These options were included in the previous release, but have since been considered unnecessary.
这些选项包含在前一版本中，但后来被认为是不必要的。


## -Xincgc
Enables incremental garbage collection. This option was deprecated in JDK 8 with no replacement.
启用增量垃圾收集。JDK 8中不推荐使用此选项，但没有替换项。


## -Xrunlibname
Loads the specified debugging/profiling library. This option was superseded by the -agentlib option.
加载指定的调试/分析库。此选项已被-agentlib选项取代。


## -XX:CMSIncrementalDutyCycle=percent
Sets the percentage of time (0 to 100) between minor collections that the concurrent collector is allowed to run. This option was deprecated in JDK 8 with no replacement, following the deprecation of the -XX:+CMSIncrementalMode option.
设置允许并发收集器运行的次要集合之间的时间百分比（0到100）。此选项在JDK 8中被弃用，但没有替换，这是由于-XX:+CMSIncrementalMode选项被弃用。


## -XX:CMSIncrementalDutyCycleMin=percent
Sets the percentage of time (0 to 100) between minor collections that is the lower bound for the duty cycle when -XX:+CMSIncrementalPacing is enabled. This option was deprecated in JDK 8 with no replacement, following the deprecation of the -XX:+CMSIncrementalMode option.
设置启用-XX:+CMSIncrementalPacing时，次要集合之间的时间百分比（0到100），该百分比是占空比的下限。此选项在JDK 8中被弃用，但没有替换，这是由于-XX:+CMSIncrementalMode选项被弃用。


## -XX:+CMSIncrementalMode
Enables the incremental mode for the CMS collector. This option was deprecated in JDK 8 with no replacement, along with other options that start with CMSIncremental.
启用CMS收集器的增量模式。这个选项在JDK 8中被弃用，没有替换，还有其他以CMSIncremental开头的选项。


## -XX:CMSIncrementalOffset=percent
Sets the percentage of time (0 to 100) by which the incremental mode duty cycle is shifted to the right within the period between minor collections. This option was deprecated in JDK 8 with no replacement, following the deprecation of the -XX:+CMSIncrementalMode option.
设置在次要集合之间的时段内增量模式占空比右移的时间百分比（0到100）。此选项在JDK 8中被弃用，但没有替换，这是由于-XX:+CMSIncrementalMode选项被弃用。


## -XX:+CMSIncrementalPacing
Enables automatic adjustment of the incremental mode duty cycle based on statistics collected while the JVM is running. This option was deprecated in JDK 8 with no replacement, following the deprecation of the -XX:+CMSIncrementalMode option.
启用基于JVM运行时收集的统计信息自动调整增量模式占空比。此选项在JDK 8中被弃用，但没有替换，这是由于-XX:+CMSIncrementalMode选项被弃用。


## -XX:CMSIncrementalSafetyFactor=percent
Sets the percentage of time (0 to 100) used to add conservatism when computing the duty cycle. This option was deprecated in JDK 8 with no replacement, following the deprecation of the -XX:+CMSIncrementalMode option.
设置计算占空比时用于添加稳健性的时间百分比（0到100）。此选项在JDK 8中被弃用，但没有替换，这是由于-XX:+CMSIncrementalMode选项被弃用。


## -XX:CMSInitiatingPermOccupancyFraction=percent
Sets the percentage of the permanent generation occupancy (0 to 100) at which to start a GC. This option was deprecated in JDK 8 with no replacement.
设置启动GC的永久发电占用率（0到100）。JDK 8中不推荐使用此选项，但没有替换项。


## -XX:MaxPermSize=size
Sets the maximum permanent generation space size (in bytes). This option was deprecated in JDK 8, and superseded by the -XX:MaxMetaspaceSize option.
设置最大永久生成空间大小（以字节为单位）。此选项在JDK 8中被弃用，并被-XX:maxmataspacesize选项取代。


## -XX:PermSize=size
Sets the space (in bytes) allocated to the permanent generation that triggers a garbage collection if it is exceeded. This option was deprecated un JDK 8, and superseded by the -XX:MetaspaceSize option.
设置分配给永久生成的空间（以字节为单位），如果超过该空间，将触发垃圾回收。这个选项在un JDK 8中被弃用，取而代之的是-XX:MetaspaceSize选项。


## -XX:+UseSplitVerifier
Enables splitting of the verification process. By default, this option was enabled in the previous releases, and verification was split into two phases: type referencing (performed by the compiler) and type checking (performed by the JVM runtime). This option was deprecated in JDK 8, and verification is now split by default without a way to disable it.
启用验证过程的拆分。默认情况下，此选项在早期版本中已启用，验证分为两个阶段：类型引用（由编译器执行）和类型检查（由JVM运行时执行）。这个选项在JDK 8中被弃用，现在默认情况下验证被拆分，而没有禁用它的方法。


## -XX:+UseStringCache
Enables caching of commonly allocated strings. This option was removed from JDK 8 with no replacement.
启用常用分配字符串的缓存。此选项已从JDK 8中删除，无需替换。


Performance Tuning Examples  性能调整示例

The following examples show how to use experimental tuning flags to either optimize throughput or to provide lower response time.
下面的示例演示如何使用实验性的调整标志来优化吞吐量或提供较低的响应时间。


Example 1 - Tuning for Higher Throughput  调整以获得更高的吞吐量
java -d64 -server -XX:+AggressiveOpts -XX:+UseLargePages -Xmn10g  -Xms26g -Xmx26g
Example 2 - Tuning for Lower Response Time  调低响应时间
java -d64 -XX:+UseG1GC -Xms26g Xmx26g -XX:MaxGCPauseMillis=500 -XX:+PrintGCTimeStamp


---

# Large Pages
Also known as huge pages, large pages are memory pages that are significantly larger than the standard memory page size (which varies depending on the processor and operating system). Large pages optimize processor Translation-Lookaside Buffers.
也被称为大页面，大页面是明显大于标准内存页面大小（根据处理器和操作系统的不同而有所不同）的内存页面。大页优化处理器转换查找缓冲区。

A Translation-Lookaside Buffer (TLB) is a page translation cache that holds the most-recently used virtual-to-physical address translations. TLB is a scarce system resource. A TLB miss can be costly as the processor must then read from the hierarchical page table, which may require multiple memory accesses. By using a larger memory page size, a single TLB entry can represent a larger memory range. There will be less pressure on TLB, and memory-intensive applications may have better performance.
Translation Lookaside Buffer（TLB）是一个页面转换缓存，它保存最近使用的虚拟到物理地址转换。TLB是一种稀缺的系统资源。TLB未命中可能代价高昂，因为处理器必须从分层页表中读取数据，这可能需要多次内存访问。通过使用较大的内存页大小，单个TLB条目可以表示较大的内存范围。对TLB的压力较小，内存密集型应用程序可能具有更好的性能。

However, large pages page memory can negatively affect system performance. For example, when a large mount of memory is pinned by an application, it may create a shortage of regular memory and cause excessive paging in other applications and slow down the entire system. Also, a system that has been up for a long time could produce excessive fragmentation, which could make it impossible to reserve enough large page memory. When this happens, either the OS or JVM reverts to using regular pages.
但是，大页面内存会对系统性能产生负面影响。例如，当一个应用程序固定了大量内存时，它可能会造成常规内存不足，并导致其他应用程序中的分页过多，从而降低整个系统的速度。另外，一个运行了很长时间的系统可能会产生过多的碎片，这可能会导致无法保留足够大的页面内存。当这种情况发生时，OS或JVM将恢复为使用常规页面。


## Large Pages Support
Solaris and Linux support large pages.
Solaris和Linux支持大页面。


## olaris

Solaris 9 and later include Multiple Page Size Support (MPSS); no additional configuration is necessary. See http://www.oracle.com/technetwork/server-storage/solaris10/overview/solaris9-features-scalability-135663.html.
Solaris 9及更高版本包含多页大小支持（MPSS）；无需额外配置。请参见http://www.oracle.com/technetwork/server-storage/solaris10/overview/solaris9-features-scalability-135663.html。


## Linux

The 2.6 kernel supports large pages. Some vendors have backported the code to their 2.4-based releases. To check if your system can support large page memory, try the following:
2.6内核支持大页面。一些供应商已经将代码移植到了基于2.4的版本中。要检查系统是否支持大页内存，请尝试以下操作：

```

# cat /proc/meminfo | grep Huge
HugePages_Total: 0
HugePages_Free: 0
Hugepagesize: 2048 kB

```
If the output shows the three "Huge" variables, then your system can support large page memory but it needs to be configured. If the command prints nothing, then your system does not support large pages. To configure the system to use large page memory, login as root, and then follow these steps:
如果输出显示三个“大”变量，那么您的系统可以支持大页面内存，但需要对其进行配置。如果命令不打印任何内容，则系统不支持大页面。要将系统配置为使用大页内存，请以根用户身份登录，然后执行以下步骤：


If you are using the option -XX:+UseSHM (instead of -XX:+UseHugeTLBFS), then increase the SHMMAX value. It must be larger than the Java heap size. On a system with 4 GB of physical RAM (or less), the following will make all the memory sharable:
如果使用选项-XX:+UseSHM（而不是-XX:+UseHugeTLBFS），则增加SHMMAX值。它必须大于Java堆大小。在具有4 GB物理RAM（或更少）的系统上，以下操作将使所有内存都可共享：


```
# echo 4294967295 > /proc/sys/kernel/shmmax

```

If you are using the option -XX:+UseSHM or -XX:+UseHugeTLBFS, then specify the number of large pages. In the following example, 3 GB of a 4 GB system are reserved for large pages (assuming a large page size of 2048kB, then 3 GB = 3 * 1024 MB = 3072 MB = 3072 * 1024 kB = 3145728 kB and 3145728 kB / 2048 kB = 1536):
如果使用-XX:+UseSHM或-XX:+UseHugeTLBFS选项，请指定大页面的数量。在下面的示例中，4GB系统中有3GB是为大页面保留的（假设大页面大小为2048kB，则3GB=3*1024MB=3072MB=3072*1024KB=3145728KB和3145728KB/2048kB=1536）：

```
# echo 1536 > /proc/sys/vm/nr_hugepages

```
Note:

Note that the values contained in /proc will reset after you reboot your system, so may want to set them in an initialization script (for example, rc.local or sysctl.conf).
请注意/proc中包含的值将在重新启动系统后重置，因此可能需要在初始化脚本（例如rc.local或sysctl.conf）中设置它们。

If you configure (or resize) the OS kernel parameters /proc/sys/kernel/shmmax or /proc/sys/vm/nr_hugepages, Java processes may allocate large pages for areas in addition to the Java heap. These steps can allocate large pages for the following areas:
如果您配置（或调整）OS kernel parameters/proc/sys/kernel/shmmax或/proc/sys/vm/nrähugepages，那么除了Java堆之外，Java进程还可以为区域分配大页面。这些步骤可以为以下区域分配大页面：


- Java heap

- Code cache

- The marking bitmap data structure for the parallel GC

Consequently, if you configure the nr_hugepages parameter to the size of the Java heap, then the JVM can fail in allocating the code cache areas on large pages because these areas are quite large in size.
因此，如果将nr_hugepages参数配置为Java堆的大小，那么JVM可能无法在大页面上分配代码缓存区域，因为这些区域的大小相当大。

---

# Application Class Data Sharing  应用程序类数据共享
                                  

Application Class Data Sharing (AppCDS) extends CDS (see https://docs.oracle.com/javase/8/docs/technotes/guides/vm/class-data-sharing.html) to enable classes from the standard extensions directories (specified by the system property java.ext.dirs; see https://docs.oracle.com/javase/8/docs/technotes/guides/extensions/spec.html) and the application class path (see "Setting the Class Path") to be placed in the shared archive. AppCDS reduces the footprint and decreases start-up time of your applications provided that a substantial number of classes are loaded from the application class path.
如果从应用程序类路径加载大量类，AppCDS可以减少应用程序的占用空间并缩短应用程序的启动时间。

This is a commercial feature that requires you to also specify the -XX:+UnlockCommercialFeatures option. This is also an experimental feature; it may change in future releases.
这是一个商业特性，要求您还指定-XX:+UnlockCommercialFeatures选项。这也是一个实验特性；在将来的版本中可能会有所改变。

## Creating a Shared Archive File, and Running an Application with It
创建共享存档文件，并使用它运行应用程序

The following steps create a shared archive file that contains all the classes used by the test.Hello application. The last step runs the application with the shared archive file.

Create a list of all classes used by the test.Hello application. The following command creates a file named hello.classlist that contains a list of all classes used by this application:

    java -Xshare:off -XX:+UnlockCommercialFeatures -XX:DumpLoadedClassList=hello.classlist -XX:+UseAppCDS -cp hello.jar test.Hello

Note that the -cp parameter must contain only JAR files; the -XX:+UseAppCDS option does not support class paths that contain directory names.

Create a shared archive, named hello.jsa, that contains all the classes in hello.classlist:
创建一个名为hello.jsa的共享存档，其中包含hello.classlist中的所有类：

    java -XX:+UnlockCommercialFeatures -Xshare:dump -XX:+UseAppCDS -XX:SharedArchiveFile=hello.jsa -XX:SharedClassListFile=hello.classlist -cp hello.jar

Note that the -cp parameter used at archive creation time must be the same as (or a prefix of) the -cp used at run time.

Run the application test.Hello with the shared archive hello.jsa:

    java -XX:+UnlockCommercialFeatures -Xshare:on -XX:+UseAppCDS -XX:SharedArchiveFile=hello.jsa -cp hello.jar test.Hello

Ensure that you have specified the option -Xshare:on or -Xshare:auto.

Verify that the test.Hello application is using the class contained in the hello.jsa shared archive:

    java -XX:+UnlockCommercialFeatures -Xshare:on -XX:+UseAppCDS -XX:SharedArchiveFile=hello.jsa -cp hello.jar -verbose:class test.Hello

The output of this command should contain the following text:

Loaded test.Hello from shared objects file by sun/misc/Launcher$AppClassLoader

## Sharing a Shared Archive across Multiple Application Processes 
跨多个应用程序进程共享共享存档


You can share the same archive file across multiple applications processes that have the exact same class path or share a common class path prefix. This reduces memory usage as the archive is memory-mapped into the address space of the processes. The operating system automatically shares the read-only pages across these processes.

The following steps create a shared archive that both applications Hello and Hi can use.
下面的步骤创建了一个应用程序Hello和Hi都可以使用的共享归档文件。

Create a list of all classes used by the Hello application and another list for the Hi application:

    java -XX:+UnlockCommercialFeatures -XX:DumpLoadedClassList=hello.classlist -XX:+UseAppCDS -cp common.jar:hello.jar Hello

    java -XX:+UnlockCommercialFeatures -XX:DumpLoadedClassList=hi.classlist -XX:+UseAppCDS -cp common.jar:hi.jar Hi

Note that because the Hello and Hi applications share a common class path prefix (both of their class paths start with common.jar), these two applications can share a shared archive file.

Create a single list of classes used by all the applications that will share the shared archive file.

The following commands combine the files hello.classlist and hi.classlist to one file, common.classlist:

cat hello.classlist hi.classlist > common.classlist

Create a shared archive, named common.jsa, that contains all the classes in common.classlist:

    java -XX:+UnlockCommercialFeatures -Xshare:dump -XX:SharedArchiveFile=common.jsa -XX:+UseAppCDS -XX:SharedClassListFile=common.classlist -cp common.jar

The value of the -cp parameter is the common class path prefix shared by the Hello and Hi applications.

Run the Hello and Hi applications with the same shared archive:

    java -XX:+UnlockCommercialFeatures -Xshare:on -XX:SharedArchiveFile=common.jsa -XX:+UseAppCDS -cp common.jar:hello.jar Hello

    java -XX:+UnlockCommercialFeatures -Xshare:on -XX:SharedArchiveFile=common.jsa -XX:+UseAppCDS -cp common.jar:hi.jar Hi






