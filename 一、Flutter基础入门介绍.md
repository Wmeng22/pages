

## 一、Flutter介绍

* Flutter 是谷歌公司开发的一款开源、免费的移动 UI 框架，可以让我们快速的在 Android 和 iOS 上构建高质量 App。它最大的特点就是跨平台、以及高性能。 它的性能相比 RN、Ionic 这样的框架要好一些。 
* Flutter 基于谷歌的 dart 语言，建议先学习 Dart 语言的基本语法。然后再进入 Flutter 的学习
* 优点：性能与构建思路几乎最接近原生开发的框架，UI跨平台稳定，Google作为一个轮子大厂，直接在两个平台上重写了各自的UIKit，对接到平台底层，减少UI层的多层转换，UI性能可以比肩原生，这个优势在滑动和播放动画时尤为明显
* 缺点：假装跨平台，躲不开原生代码，ui死亡嵌套，较年轻，相比 Ionic、以及 RN 这样的 老框架来说社区不是特别完善。还有就是学习成本高。希望未来社区能更加完善、让我们的学习成本 更低。


## 二、Windows 上面搭建 Flutter Android 运行环境 

### （一）、 电脑上面安装配置 JDK 

* 1、下载安装 JDK 
       https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html 

* 2、配置 JDK 

     * （1）系统变量里面新增 JAVA_HOME，设置值为 java sdk 根目录：

     * ![image-20201029165259286](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201029165259286.png)

     * （2）系统变量找到 Path 在 Path 环境变量里面增加如下代码

       ;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin

       ![image-20201029165510960](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201029165510960.png)

       

### （二）、 电脑上下载安装 Android Studio

启动Android Studio，然后执行“Android Studio安装向导”。安装Android SDK，Android SDK平台工具和Android SDK构建工具，这是Flutter为Android开发时所必需的

![image-20201102114117419](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201102114117419.png)

### （三）、电脑上面下载配置 Flutter Sdk

* 1、下载 Flutter SDK 
  https://flutter.dev/docs/development/tools/sdk/releases#windows 
* 2、把下载好的 Flutter SDK 随便减压到你想安装 Sdk 的目录如（E:\flutter_windows\flutter）

![image-20201029170431006](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201029170431006.png)

* 3、把 Flutter 安装目录的 bin 目录配置到环境变量。 
  如图所示需要把 E:\flutter_windows\flutter\bin 目录配置到 path 环境变量里面

  ![image-20201029170551100](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201029170551100.png)

### （四）、运行 flutter doctor 命令检测环境是否配置成功

![image-20201029170748693](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201029170748693.png)



运行的时候可能会提示下面错误：

![image-20201029170908209](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201029170908209.png)



这时候可运行命令：flutter doctor --android-licenses 
注意：提示输入 Y/N 的地方全部输入 Y

### （五）、创建 Flutter 项目

1、在Android Studio上创建

2、通过命令行创建：flutter create flutterdemo

## 三、Flutter 目录结构介绍 

## （一）、Flutter 目录结构



![image-20201029172148787](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201029172148787.png)

| 文件夹       | 作用                                               |
| ------------ | -------------------------------------------------- |
| android      | android 平台相关代码                               |
| ios          | ios 平台相关代码                                   |
| lib          | flutter 相关代码，我们主要编写的代码就在这个文件夹 |
| test         | 用于存放测试代码                                   |
| pubspec.yaml | 配置文件，一般存放一些第三方库的依赖。             |



## （二）、Flutter 入口文件、入口方法

每一个 flutter 项目的 lib 目录里面都有一个 main.dart 这个文件就是 flutter 的入口文件 main.dart 里面的

```js
void main(){
  runApp(MyApp());
  //判断如果是Android版本的话 设置Android状态栏透明沉浸式
  if (Platform.isAndroid) {
    //沉浸式状态栏
    SystemUiOverlayStyle systemUiOverlayStyle =
    SystemUiOverlayStyle(statusBarColor: Colors.transparent);
    SystemChrome.setSystemUIOverlayStyle(systemUiOverlayStyle);
  }
  // 强制竖屏
  SystemChrome.setPreferredOrientations([
    DeviceOrientation.portraitUp,
    DeviceOrientation.portraitDown
  ]);
}
```

其中的 main 方法是 dart 的入口方法。runApp 方法是 flutter 的入口方法。 MyApp 是自定义的一个组件

## （三）、pubspec.yaml

`pubspec.yaml`是Flutter项目的核心配置文件，类似于Android项目中的build.gradle配置文件.

```js
//name很重要，如果修改了name所有的dart的文件的import前引用的本地的文件啊的包名都需要修改
name: flutterdemo
description: A new Flutter application.
 
dependencies:
  flutter:
    sdk: flutter
 
 //添加依赖packages ^表示适配和当前大版本一致的版本，~表示适配和当前小版本一致的版本
  cupertino_icons: ^0.1.2
  permission_handler: ^5.0.0+hotfix.5
  fluro: ^1.6.3
  dio: ^3.0.9
  flutter_screenutil: ^1.0.2
  flutter_swiper : ^1.1.6
  fluttertoast: ^4.0.1
  path_provider: ^1.6.8
  shared_preferences: ^0.5.7+2
  device_info: 0.4.1+1
  gallery_saver: ^2.0.1
  camera:
  flutter_qr_reader: ^1.0.3
  fluwx: ^1.0.4
  flutter_alipay: ^1.0.0
 
dev_dependencies:
  flutter_test:
    sdk: flutter
 
  //启用国际化
  flutter_localizations:
    sdk: flutter
 

 
flutter:
 
  
  //添加资源，不单单是图片，images是个和pubspec.yaml配置文件同级的目录，如果不同级，需要添加..
  assets:
        - images/park.jpg
        - images/lake.jpg
        - images/touxiang.jpg
//文件夹方式
        - assets/login/
        - assets/index/
        - assets/bottom/
 
  //字体设置
   fonts:
     - family: Schyler
       fonts:
       - asset: fonts/Schyler-Regular.ttf
        - asset: fonts/Schyler-Italic.ttf
           style: italic
     - family: Trajan Pro
       fonts:
      - asset: fonts/TrajanPro.ttf
      - asset: fonts/TrajanPro_Bold.ttf
        weight: 700

```

pubspec.yaml做了更改之后保存，vscode会自动下载资源，如果下载不了，可使用flutter pub  get 下载

注：在添加原生插件依赖时配置相应权限，安卓需要在AndroidManifest.xml配置权限，ios需要在Info.plist配置权限

## （四）、Flutter Widget

Flutter Widget采用现代响应式框架构建，这是从 [React](http://facebook.github.io/react/) 中获得的灵感，中心思想是用widget构建你的UI。 Widget描述了他们的视图在给定其当前配置和状态时应该看起来像什么。当widget的状态发生变化时，widget会重新构建UI，Flutter会对比前后变化的不同， 以确定底层渲染树从一个状态转换到下一个状态所需的最小更改（译者语：类似于React/Vue中虚拟DOM的diff算法）。

```js
import 'package:flutter/material.dart';

void main() {
  runApp(
    new Center(
      child: new Text(
        'Hello, world!',
        textDirection: TextDirection.ltr,
      ),
    ),
  );
}
```

Flutter有一套丰富、强大的基础widget，其中以下是很常用的：

- [`Text`](https://docs.flutter.io/flutter/widgets/Text-class.html)：该 widget 可让创建一个带格式的文本。
- [`Row`](https://docs.flutter.io/flutter/widgets/Row-class.html)、 [`Column`](https://docs.flutter.io/flutter/widgets/Column-class.html)： 这些具有弹性空间的布局类Widget可让您在水平（Row）和垂直（Column）方向上创建灵活的布局。其设计是基于web开发中的Flexbox布局模型。
- [`Stack`](https://docs.flutter.io/flutter/widgets/Stack-class.html)： 取代线性布局 (译者语：和Android中的LinearLayout相似)，[`Stack`](https://docs.flutter.io/flutter/widgets/Stack-class.html)允许子 widget 堆叠， 你可以使用 [`Positioned`](https://docs.flutter.io/flutter/widgets/Positioned-class.html) 来定位他们相对于`Stack`的上下左右四条边的位置。Stacks是基于Web开发中的绝度定位（absolute positioning )布局模型设计的。
- [`Container`](https://docs.flutter.io/flutter/widgets/Container-class.html)： [`Container`](https://docs.flutter.io/flutter/widgets/Container-class.html) 可让您创建矩形视觉元素。container 可以装饰为一个[`BoxDecoration`](https://docs.flutter.io/flutter/painting/BoxDecoration-class.html), 如 background、一个边框、或者一个阴影。 [`Container`](https://docs.flutter.io/flutter/widgets/Container-class.html) 也可以具有边距（margins）、填充(padding)和应用于其大小的约束(constraints)。另外， [`Container`](https://docs.flutter.io/flutter/widgets/Container-class.html)可以使用矩阵在三维空间中对其进行变换。

## 四、Vscode 调试 Flutter 项目

* 如果你习惯用 Android Studio 的话可以直接用 Android Studio 直接开发 Flutter。但是 Android Studio 比较耗费电脑资源，所以比较推荐使用 Vscode

  ![image-20201102142507842](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201102142507842.png)

* Vscode 中安装 Flutter 插件 Dart 插件

  ![image-20201030105548408](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201030105548408.png)

  ![image-20201030105617591](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201030105617591.png)

* 运行 Flutter 项目： 

  ``` js
  flutter run
  ```

* r 键：点击后热加载，也就算是重新加载。

* p 键：显示网格，这个可以很好的掌握布局情况，工作中很有用

* o 键：切换 android 和 ios 的预览模式

* q 键：退出调试预览模式

* 开发过程中如果报错，可运行flutter clean

## 五、Flutter打包apk

* 运行flutter build apk (flutter build 默认会包含 --release选项)
* 打包好的发布APK位于/build/app/outputs/apk/app-release.apk















