# GradleIntroduce

Android Gradle 用法

[Android 官方gradle用户指南（Gradle Plugin User Guide）](http://tools.android.com/tech-docs/new-build-system/user-guide)


* 根目录下的 setting.gradle 当中主要用来include 子模块
include ':app'
* 根目录下的 build.gradle 包含一些通用的配置，这些配置可以在各个子模块中使用。
* 根目录下的 gradle.properties 文件属性 可以定义一些属性 build.gradle 中直接用就可以了
* 根目录下 local.properties 设置android的sdk和ndk路径。

提高Gradle 运行速度 在 gradle.properites 中进行如下配置

*  org.gradle.parallel = true //如果你的项目没有时序要求，打开这个选项可以并发处理多个任务，充分利用硬件资源。
*  org.gradle.daemon = true //守护进程可以使编译的时间大大缩短
* org.gradle.jvmargs=-Xms256m -Xmx1024m  //Gradle是运行在java虚拟机上的，这个指定了这个虚拟机的堆内存初始化为256M 最大为1G
