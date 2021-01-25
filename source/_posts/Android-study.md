---
title: Android-study
top: false
cover: false
toc: true
mathjax: true
date: 2020-09-25 20:35:49
password:
summary:
tags:
categories:
---

# 移动开发

移动开发技术主要分为原生开发和跨平台开发两种。其中，原生应用是指在某个特定的移动平台上，使用平台所支持的开发工具和语言，直接调用系统提供的API所开发的应用。

## **背景**

**原生开发的主要优势体现在：**

1.可以快速访问本平台的全部功能，比如摄像头、GPS等；

2.原生应用的速度快、性能高，而且可以实现比较复杂的动画和绘制效果，用户体验较好。

**原生开发的缺点也很明显，主要体现在：**

1.开发成本较高，不同的平台必须维护不同的代码，人力成本也会随之增加；

2.有新的功能需要更新时，只能进行版本升级。

随着移动互联网的高速发展，在很多的业务场景下，传统的纯原生开发已经不能满足日益增长的业务需求，主要表现在以下两个方面：

1.应用动态化的需求增大。当需求发生变化，或者是需要增加新的功能时，传统的纯原生应用开发只能通过版本的升级来更新内容，然而应用的上架和审核都需要一定的时间。因此，开发人员迫切地希望进行应用内容的更新时，可以不更新版本，提升工作效率。

2.业务需求变化快，开发成本变高。原生开发一般需要技术团队对iOS、Android两个开发平台进行维护。当版本更新迭代时，开发和测试的成本都会增加。

针对上述两个问题，跨平台框架应运而生。

------

## **跨平台技术简介**

针对上文提到的原生开发所面临的问题，目前在IT界已经诞生了很多跨平台框架，主要分为三类：

1.H5+原生(Cordova、Ionic、微信小程序)；

2.JavaScript开发+原生渲染(React Native、Weex、快应用)；

3.自绘UI+原生(Flutter)。



下面对React Native、Weex和Flutter进行对比

------

**1.React Native**

React Native是Facebook于2015年4月开源的跨平台移动应用开发框架，是Facebook开源的JS框架React在原生移动应用平台的衍生物。React Native使用了react的设计模式，但是其UI渲染、动画效果、网络请求等均是由原生来实现的。开发者编写JS代码，通过React Native的中间层转化为原生控件，并进行操作。也就是说通过JS代码来调用原生的组件，从而实现相应的功能。

React Native实现跨平台的功能，主要由Java、C++和Javascript三层所构成的。其中，C++实现的动态链接库（.so），作为中间适配层桥接，实现了JS端与原生端的双向通信交互。React Native会把应用的JS代码编译成一个JS文件，React Native整体框架目标就是为了解释并运行这个JS脚本文件，如果是JS扩展的API，则直接通过bridge调用native；如果是UI界面，则映射到virtual DOM这个虚拟的JS数据结构中，通过bridge传递到native，然后根据数据设置各个对应的真实native的View。

![img](https://gitee.com/lastlight/MyPictrue/raw/master/img/v2-ff15fe8318cc70fdce432f3186aae5a3_720w.jpg)

------

**2.Weex**

在Weex设计之初，开发者就考虑到，使其能够在三端（iOS、安卓和H5）上均能得到展现。在最上面的DSL，阿里一般称之为Weex文件（.we），通过Transform转换为js-bundle，再部署到服务器，这样服务端就完成了。在客户端，第一层是JS-Framework，最后是RenderRengine。

表面上，Weex是一种客户端技术，但实际上，它串联起了从本地开发、云端部署到分发的整个链路。开发者可以在本地像编写Web页面一样先编写一个APP界面，然后通过命令行工具将之编译为一段JavaScript代码，生成一个Weex的JS bundle。与此同时，开发者可以将生成的JS bundle部署至云端，之后通过网络请求或者预下发的方式加载至用户的移动应用客户端。

在移动应用客户端，Weex SDK会准备一个JavaScript执行环境，在用户打开一个Weex页面时，在该环境中执行相应的JS bundle，并将执行过程中产生的各种命令发送到native端，进行界面渲染、数据存储、网络通信、调用设备及用户交互响应等。如果用户希望使用浏览器访问这个界面，那么他可以在浏览器中打开一个相同的Web页面，这个页面和移动应用使用相同的页面源代码，但被编译成适合Web展示的JS Bundle，通过浏览器里的javaScript引擎及Weex SDK运行起来的。

------

**3.Flutter**
Flutter 是Google推出并开源的移动应用开发框架，主打跨平台、高保真、高性能。开发者可以通过Dart语言进行APP开发，只需要一套代码就可以同时构建Android和iOS应用，并且可以达到与原生应用一样的性能。Flutter还提供了丰富的组件、接口，开发者可以高效地为 Flutter添加native扩展。此外，Flutter还使用了Native引擎渲染视图，为用户提供了良好的体验。

Flutter与用于构建移动应用程序的其它多数框架不同，因为Flutter既不使用WebView，也不使用操作系统的原生控件。相反，Flutter使用自己的高性能渲染引擎来绘制widget。这样不仅可以保证在Android和iOS的UI一致性，而且也可以避免对原生控件依赖而带来的限制和高昂的维护成本。

同时，Flutter使用Skia作为2D引擎渲染，Skia是Google的一个2D图形处理函数库，在字型、坐标转换以及点阵图等方面都有高效而且简洁的表现。Skia是跨平台的，并提供了非常友好的API。由于Android系统已经内置了Skia，所以Flutter在打包APK时，不需要再将Skia打包到APK中，但是iOS系统并未内置Skia，所以在构建API时，必须将Skia一起打包。

------

## **高性能的Flutter**

目前，Flutter程序主要有两种运行方式：静态编译与动态解释。静态编译的程序在执行前，会被全部翻译为机器码，通常将这种类型称为AOT，即 “提前编译”。解释执行则是一句句地边翻译边运行，通常将这种类型称为JIT，即“即时编译”。

AOT程序的典型代表是用C/C++开发的应用，它们必须在执行前编译成机器码。而JIT的代表则非常多，如JavaScript、python等。事实上，所有脚本语言都支持JIT模式。但需要注意的是，JIT和AOT指的是程序运行方式，和编程语言并非是强关联的，有些语言既可以以JIT方式运行，也可以以AOT方式运行，如Java、Python，它们可以在第一次执行时编译成中间字节码，然后在之后的执行中，直接执行字节码。

Flutter的高性能主要靠两点来保证，首先，Flutter APP采用Dart语言进行开发。当Dart在 JIT模式下时，其运行速度与 JavaScript基本持平。此外Dart支持 还AOT，当Dart在 AOT模式下事，其运行速度远超JavaScript。速度的提升对高帧率下的视图数据计算很有帮助。

其次，Flutter使用自己的渲染引擎来绘制UI，布局数据等由Dart语言直接控制，所以在布局过程中不需要像RN那样要在JavaScript和Native之间通信，在一些滑动和拖动的场景下具有明显优势。由于滑动和拖动往往会引起布局的变化，所以JavaScript需要不停地与Native之间同步布局信息，这和在浏览器中要JavaScript频繁操作DOM所带来的问题是相同的，都会带来比较可观的性能开销。

------

## **为何Flutter选择Dart**

**1.开发效率高。**Dart运行时和编译器支持Flutter的两个关键特性的组合，分别是基于JIT的快速开发周期和基于AOT的发布包。基于JIT的快速开发周期：Flutter在开发阶段，采用JIT模式，这样就避免了每次改动都需要进行编译，极大地节省了开发时间。基于AOT的发布包，Flutter在发布时可以通过AOT生成高效的ARM代码，以保证应用性能。而JavaScript则不具备这个能力。

**2.高性能。**为了实现流畅、高保真的的UI体验，Flutter必须在每个动画帧中都运行大量的代码。这意味着需要一种既能支持高性能，又能保证不丢帧的周期性暂停的语言，而Dart支持AOT，在这一点上比JavaScript更有优势。

**3.快速分配内存。**Flutter框架使用函数式流，这使得它在很大程度上依赖于底层的内存分配器。

**4.类型安全。**由于Dart是类型安全的语言，支持静态类型检测，所以可以在编译前就发现一些类型的错误，并排除潜在问题。这对于前端开发者来说更具有吸引力。而JavaScript是一个弱类型语言，这也是为什么在诸多前端社区中，会有众多为JavaScript代码添加静态类型检测的扩展语言和工具。

------

## **Flutter框架结构**

![img](https://gitee.com/lastlight/MyPictrue/raw/master/img/v2-41.jpg)

Flutter Framework是一个完全由Dart语言构建的SDK，它实现了一整套自底而上的基础库。

1.底部两层(Foundation和Animation、Painting、Gestures)是Flutter引擎暴露的底层UI库，提供动画、手势及绘制能力。

2.Rendering层是一个抽象的布局层，它依赖于dart UI层。Rendering层会构建一个UI树，当UI树有变化时，它会随即计算出有变化的部分，然后更新UI树，最终将UI树绘制到屏幕上。这个过程类似于React中的虚拟DOM。Rendering层可以说是Flutter UI框架最核心的部分，它除了确定每个UI元素的位置、大小之外，还要进行坐标变换和绘制(调用底层dart:ui)。

3.Widgets层是Flutter提供的一套基础组件库，在基础组件库之上，Flutter还提供了 Material 和Cupertino两种视觉风格的组件库。

Flutter Engine：这是一个完全由 C++实现的 SDK，其中包括了 Skia引擎、Dart运行时和文字排版引擎等。在代码调用 dart:ui库时，调用最终会走到Engine层，然后实现真正的绘制逻辑。

React Native、Weex和Flutter进行对比结果如下所示：

![img](https://gitee.com/lastlight/MyPictrue/raw/master/img/v2-b6.jpg)

------


# Android开发

**简介:**
<img src="https://gitee.com/lastlight/MyPictrue/raw/master/img/image-20200608164002594.png" alt="image-20200608164002594" style="zoom:67%;" />

## 1.HelloWorld

- 项目创建

<img src="https://gitee.com/lastlight/MyPictrue/raw/master/img/image-20200414112829983.png" alt="image-20200414091418749" style="zoom:80%;" />

<img src="https://gitee.com/lastlight/MyPictrue/raw/master/img/image-20200414091418749.png" alt="image-20200414091756399" style="zoom:80%;" />

​											==Android版本一般4.4,确保兼容==

- 项目目录

![image-20200414112902917](https://gitee.com/lastlight/MyPictrue/raw/master/img/image-20200414112902917.png)

![image-20200414112829983](https://gitee.com/lastlight/MyPictrue/raw/master/img/image-20200414091756399.png)





![image-20200414121811933](https://gitee.com/lastlight/MyPictrue/raw/master/img/image-20200414121811933.png)

![image-20200414122141355](https://gitee.com/lastlight/MyPictrue/raw/master/img/image-20200414122141355.png)

## Android四大组件

<img src="https://gitee.com/lastlight/MyPictrue/raw/master/img/image-20200602164227656.png" alt="image-20200602164227656" style="zoom:67%;" />

<img src="https://gitee.com/lastlight/MyPictrue/raw/master/img/image-20200602174434020.png" alt="image-20200602174434020" style="zoom: 90%;" />

## 本地化



## JetPack

JetPack简介

### ViewModel及其使用

![image-20200602175502099](https://gitee.com/lastlight/MyPictrue/raw/master/img/image-20200602175502099.png)

### LiveData及其使用

当底层数据变化时，自动通知界面。



<img src="https://gitee.com/lastlight/MyPictrue/raw/master/img/image-20200602180902942.png" alt="image-20200602180902942" style="zoom:67%;" />

## 【开发经验】flutter的优点与缺点

> 本文默认你已经是开发者，并对`Flutter`有基本的了解，但是还未深入使用，希望了解`Flutter`在商业级（而非demo）的项目中的优势与劣势。

很多前端开发者应该都寻找过跨平台的App解决方案，包括没有同时独立开发`iOS`和`Android`双端原生app的开发者，应该都接触过或者看到过Google的`Flutter`框架。我对于iOS原生开发与基于Vue.js的web开发比较熟悉，并在一个正在进行的蓝牙硬件项目中应用了`Flutter`框架，经历的漫长的适应，在本文中我将以iOS原生开发者与web开发者的视角看待`Flutter`框架，简单罗列`Flutter`的优势与缺点。

### Flutter优点

`Flutter`的优点非常明显，如果你选择一个跨平台框架，与众多基于`html`的跨平台框架相比，`Flutter`绝对是体验最好，性能与构建思路几乎最接近原生开发的框架。

- **性能强大，流畅**  
  `Flutter`对比`weex`和`react native`相比，性能的强大是有目共睹的。基于`dom`树渲染原生组件，很难与直接在原生视图上绘图比肩性能，Google作为一个轮子大厂，直接在两个平台上重写了各自的UIKit，对接到平台底层，减少UI层的多层转换，UI性能可以比肩原生，这个优势在**滑动**和**播放动画**时尤为明显。
- **路由设计优秀**  
  `Flutter`的路由传值非常方便，`push`一个路由，会返回一个`Future`对象（也就是`Promise`对象），使用`await`或者`.then`就可以在目标路由`pop`，回到当前页面时收到返回值。这个反向传值的设计基本是甩了微信小程序一条街了。弹出`dialog`等一些操作也是使用的路由方法，几乎不用担心出现传值困难
- **单例模式**  
  `Flutter`支持单例模式，单例模式的实现也非常简单。单例模式很好的解决了一些问题。相比之下，js的单例则并不是一个真正的单例，或者说不是一个简单的单例，这也是受限于js所运行的环境。单例模式并不总是合理的，容易被滥用。但是在App的初期开发中，往往一个容易实现的单例可以帮助我们快速完成一些逻辑的搭建。
- **优秀的动画设计**  
  `Flutter`的动画简单到不可思议，动画对象会根据屏幕刷新率每秒产生很多个（一般是60个）浮点数，只需要将一个组件属性通过补间（Tween）关联到动画对象上，`Flutter`会确保在每一帧渲染正确的组件，从而形成连贯的动画。这种十分暴力的操作在`Flutter`上却看不到明显的卡顿，这也是`Flutter`的一个魔力所在。相比之下其他跨平台框架几乎不能设计动画……往往会遭遇非常严重的性能问题。
- **UI跨平台稳定**  
  Google直接在两个平台上在底层重写了UIKit，不依赖于`Css`等外部解释器，几乎不存在UI表达不理想，渲染不正常的情况，可以获得非常稳定的UI表达效果。`Css`换个浏览器就有不同的表现，基于`Css`的跨平台框架很难获得稳定的UI表现。
- **可选静态的语言，语言特性优秀**
  `Dart`是一个静态语言，这也是相对于js的一个优势。`Dart`可以被编译成js，但是看起来更像`java`。静态语言可以避免错误，获得更多的编辑器提示词，极大的增加可维护性。很多js库也已经用ts重写了，`Vue3.0`的底层也将全部使用ts编写，静态语言的优势不言而喻。

### Flutter缺点

- **假装跨平台，躲不开原生代码**  
  这是最大的问题，跨平台框架说白了就是UI跨平台，最后还是在原生平台运行，本来两个平台就有天壤之别，一套代码就想吃掉iOS和Android在实际应用之中其实根本就不现实。`Flutter`具有与原生代码互相调用的能力固然非常科学，但是问题反而显得更加明显——我一个前端工程师上哪里去知道什么是`UIViewController`，什么是`Activity`呢？我要是双端都熟悉，学习`Flutter`就显得很没有必要。这是一个很矛盾的点，特别是在团队里，只有几个前端突然想学`Flutter`，是绝对做不来大项目的，如果有原生开发者，那就没必要搞`Flutter`了。
- **组合而不是继承的思路**  
  `Flutter`提倡“组合”，而不是“继承”。在iOS开发中，我们经常会继承UIView，重写UIView的某个生命周期函数，再添加一些方法和属性，来完成一个自定义的View。但是在`Flutter`中这些都是不可能的——属性都是`final`的，例如你继承了了一个`Container`，你是不能在它的生命周期中修改他的属性的。你始终需要嵌套组合几种`Widget`，例如`Row`，`Container`，`ListView`等`Widget`。这种方法非常不符合直觉，初学时很难想明白如何构建一个完整的组件。
- **Widget的类型难以选择**  
  `Flutter`的`Widget`分为`StatefulWidget`和`StatelessWidget`两种，一种是带状态的一种是不带状态的，刚开发的时候很难想明白用哪个，因为`StatelessWidget`也能存值，其实区别就在于框架重构UI的时候会使用`State`来重构，如果是`StatelessWidget`，暂时存进去的值就没了。但是问题远不止这么简单，好在只是有点麻烦，并不影响产品性能。
- **糟糕的UI控件API**  
  虽然google尽可能的让我们通过构造函数定制化`Widget`，但是也难免有遗漏的。例如，又一次我想修改一个`Appbar`的高度，居然没有找到关于高度的属性，通过阅读源码发现，高度是写死（`const`）的。上文已经说过，无法通过生命周期来改变组件属性，自己写Appbar显得非常没必要，毕竟我还是想使用`Appbar`的各种方便的功能。最后我只能把他的源码全部复制出来，直接修改高度来使用。初学框架，和一些初级开发者是不可能有迅速阅读源码的能力的（作为框架也不应该产生如此问题）。一些定制化的UI的Api设计经常有缺失，好在我已经基本习惯了。除了`Appbar`这种复杂的组件，自己写一个小组件也并不费事。
- **糟糕的资源管理设计**  
  这里是最蠢的，`Flutter`支持动态加载不同分辨率的图片，但是目录设计太鬼畜了。简单的说，Sketch导出的多分辨率资源，**几乎不可能**直接拖到`Flutter`里用，极其，极其，麻烦。
- **墙**  
  毕竟国情在此，要用`Flutter`，先买梯子。虽然有“在中国使用Flutter”指南，但是太麻烦，没梯子开发`Flutter`，难度系数太高了，总不能碰到每个问题都花一整天寻找替代方案吧，先买好梯子图个安心……

### 总结

`Flutter`主要的坑就在于需要**非常了解原生的环境**，其实跨平台的框架都是如此，想要通过跨平台的API就拿下双端的开发任务，对认真学习的原生开发者来说也是不公平的。
 主要的优势则在于动画流畅，很多开发者反应比原生安卓还流畅（存疑），至少在iOS上是看不到卡顿的，安卓上动画也很稳定，性能上展示了`Google`的硬实力