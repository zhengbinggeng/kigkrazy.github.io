---
title: 安卓个人开发规范开发规范
categories:
 - android
tags:
 - android
 - 絮叨
---

### 代码规范
开发时候请严格遵照下面的规范进行代码开发。[Android开发规范](https://github.com/Blankj/AndroidStandardDevelop#5-%E8%B5%84%E6%BA%90%E6%96%87%E4%BB%B6%E8%A7%84%E8%8C%83)  
阅读文章的时候请注意：**各种变量、包、类、资源的命名方式，团队成员的代码风格统一。**

### 代码架构方式
代码架构方式通常按照`MVP`的方式架构。
#### MVP架构介绍
MVP是单词Model View Presenter的首字母的缩写，分别表示数据层、视图层、发布层，它是MVC架构的一种演变。作为一种新的模式，MVP与MVC有着一个重大的区别：在MVP中View并不直接使用Model，它们之间的通信是通过Presenter (MVC中的Controller)来进行的，所有的交互都发生在Presenter内部，而在MVC中View会直接从Model中读取数据而不是通过 Controller。
* View: 对于View层也是视图层，在View层中只负责对数据的展示，提供友好的界面与用户进行交互。在Android开发中通常将Activity或者Fragment作为View层。
* Model: 对于Model层也是数据层。它区别于MVC架构中的Model，在这里不仅仅只是数据模型。在MVP架构中Model它负责对数据的存取操作，例如对数据库的读写，网络的数据的请求等。
* Presenter:对于Presenter层他是连接View层与Model层的桥梁并对业务逻辑进行处理。在MVP架构中Model与View无法直接进行交互。所以在Presenter层它会从Model层获得所需要的数据，进行一些适当的处理后交由View层进行显示。这样通过Presenter将View与Model进行隔离，使得View和Model之间不存在耦合，同时也将业务逻辑从View中抽离。

##### MVP相关资料
[官方示例](https://github.com/googlesamples/android-architecture)  
[MVP架构模式详解](https://www.jianshu.com/p/4b754ea48a40)  
[Android架构（一）MVP架构在Android中的实践](http://blog.csdn.net/johnny901114/article/details/54783106)

##### 分包方式
一般我会分为以下几个包：
* app 存放本程序的Application
* bean 存放实体类
* model 数据存取，以及网络交互相关的类
* constant 存放常量，以及一些枚举类
* presenter 存放`MVP`架构中的`P`层类
* view 存放activity以及Fragement
* util 存放工具类
* feature 功能模块。一般存放一些主要的技术功能模块
* service 服务类
* broadcast 广播注册类

##### 关于MVP架构的一些个人想法
MVP架构在小型项目中有时候会增加很多冗余代码。比如一个activity通常会带一个`VIEW`的接口类，这在我们日常的开发中有可能觉得是脱裤子放屁——多此一举。
这点也是MVP架构最受争议的一点。关于这点个人有以下看法：
1. 项目中应该尽量按照MVP架构进行开发，MVP主要功能是让代码层次更加清晰，添加不多的代码能够使层次更分明是值得付出的代价。
2. 根据项目以及功能的复杂度可以适当的省略`VIEW`接口，直接在activity中直接调用写相应的逻辑。**这是一个折中优化的方法。**

### 第三方依赖库的选择
说下代码开发中的一个原则：**常用功能尽量选择开源的成熟第三方库，而不是自己造轮子。**
##### 为什么要尽量引用第三方库
因为第三方开源库已经经过了广大开发人员的使用以及验证BUG出现的几率比较小，同时这能使我们代码写更少的代码，保持代码的整洁。  
因此，代码开发中经常会使用到一些常用的功能：**文件读写**，**网络请求**等，这些常见的功能很多时候都已经有前辈帮我们写好了，我们尽量找出库而不自己写。

|功能|框架|说明|
|:---:|:---:|:---:|
|常用工具类|[andrutil][1001]|一个通用的工具类库集合，里面包含了`gson`、`commons-io`等，下面介绍的几个常用类库都包含在这里类库里面，所以一般我们只需要以来这个库即可将常用工具类全部依赖了|
|常用工具类|[AndroidUtilCode][1002]|一个安卓常用工具类的大杂烩，大而全的工具类库。已经包含在`andrutil`的依赖中|
|网络请求|RxJava+retrofit|一个强大的异步网络请求库|
|数据存储|[greenDAO][1003]|轻量又实用的sqlite库，用于存放各种本地配置|
|反射类库|[joor][1004]|小巧又方便的JAVA反射调用类库|
|BUG检测|[leakcanary][1006]|一款内存检测框架|
|UI开发|[QMUI_Android][1005]|腾讯开源的一个UI库，就算不用也有很多在UI开发时候可以参考的点|

以上常用工具类只需要引用`andrutil`就可全部依赖。

### 附加文章
[Android 流行框架查速表](https://www.ctolib.com/cheatsheets-Android-ch.html)

[1001]: https://github.com/kigkrazy/andrutil
[1002]: https://github.com/Blankj/AndroidUtilCode
[1003]: https://github.com/greenrobot/greenDAO
[1004]: https://github.com/jOOQ/jOOR
[1005]: https://github.com/QMUI/QMUI_Android
[1006]: https://github.com/square/leakcanary