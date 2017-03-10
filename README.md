# GradleIntroduce






## Android Gradle 用法


[Android 官方gradle用户指南（Gradle Plugin User Guide）](http://tools.android.com/tech-docs/new-build-system/user-guide)



##Android Gradle 用法

* 根目录下的 setting.gradle 当中主要用来include 子模块
include ':app'
* 根目录下的 build.gradle 包含一些通用的配置，这些配置可以在各个子模块中使用。
* 根目录下的 gradle.properties 文件属性 可以定义一些属性 build.gradle 中直接用就可以了
* 根目录下 local.properties 设置android的sdk和ndk路径。

提高Gradle 运行速度 在 gradle.properites 中进行如下配置

*  org.gradle.parallel = true //如果你的项目没有时序要求，打开这个选项可以并发处理多个任务，充分利用硬件资源。
*  org.gradle.daemon = true //守护进程可以使编译的时间大大缩短
* org.gradle.jvmargs=-Xms256m -Xmx1024m  //Gradle是运行在java虚拟机上的，这个指定了这个虚拟机的堆内存初始化为256M 最大为1G

##创建子模块

* 右键 open module settings  点击加号创建module 选择你要创建的模块 android library
* 创建完成之后添加依赖， 在  module settings 中 dependcencis 中点加号选择module Library
添加已创建的模块

##添加.so链接库

* 将你的app需要集成的百度地图之类的 so动态库 放到libs文件夹下
* 在build.gradle(Module:app)文件，在android节点下添加

```
sourceSets {
    main {
        jniLibs.srcDirs = ['libs']
    }
}
```

* compileSdkVersion 的 版本要与 appcompat_v7 的版本对应，如果v7库的版本compileSdkVersion的版本则不能保证所有API版本的兼容性

## Android Gradle git 提交 .gitignore 文件配置

[github 官方各种语言的gitignore 文件](https://github.com/github/gitignore/blob/master/Android.gitignore)

可以在本仓库中直接下载Android.gitignore 文件

几个人一起开发的时候可以在.gitignore 文件中屏蔽了 gradle.properties 文件 ，然后每个人配置自己本地的
buildToolsVersion 和 gradle plugin 版本 还有一些配置

#### gradle.properties
```

# Project-wide Gradle settings.

# IDE (e.g. Android Studio) users:
# Gradle settings configured through the IDE *will override*
# any settings specified in this file.

# For more details on how to configure your build environment visit
# http://www.gradle.org/docs/current/userguide/build_environment.html

# Specifies the JVM arguments used for the daemon process.
# The setting is particularly useful for tweaking memory settings.
# Default value: -Xmx10248m -XX:MaxPermSize=256m
# org.gradle.jvmargs=-Xmx2048m

# When configured, Gradle will run in incubating parallel mode.
# This option should only be used with decoupled projects. More details, visit
# http://www.gradle.org/docs/current/userguide/multi_project_builds.html#sec:decoupled_projects
# org.gradle.parallel=true
# org.gradle.daemon = true
gradlePlugin = com.android.tools.build:gradle:2.2.3
buildSDKVersion = 25.0.1


```

#### build.gradle
```

/**
 * gradlePlugin  本地的gradle 插件版本
 * buildSDKVersion 本地编译版本
 * 这两个值都定义在gradle.propertres 中 在.gitignore 已屏蔽提交
 */

buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath gradlePlugin
    }
}

ext{
    buildToolsVersion = buildSDKVersion
}

allprojects {
    repositories {
        jcenter()
    }
}

```

各modules 中的build.gradle 跟本项目一致

关于Gradle的一些应用也可以在
[Android Studio 指南](https://developer.android.google.cn/studio/write/vector-asset-studio.html#about)
查看

大家可以Star一下   后面遇到什么好玩的功能我会直接在上面补充 谢谢

----


偶尔写了点小文章[ScottFu](http://blog.csdn.net/qq_22797039)

关注微信公众号，每天都有优质技术文章，搞笑GIF图片推送哦。

![这里写图片描述](http://img.blog.csdn.net/20161226090130556?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjI3OTcwMzk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
