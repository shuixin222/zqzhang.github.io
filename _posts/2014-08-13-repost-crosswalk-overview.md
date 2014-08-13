---
layout: post
type: post
title: Crosswalk简介
---

**注**：本文摘自[Xingnan Wang](https://github.com/xingnan)在[英特尔开发人员专区发表的文章](https://software.intel.com/zh-cn/articles/crosswalk?utm_campaign=CSDN&utm_source=intel.csdn.net&utm_medium=Link&utm_content=%20others-crosswalk)，也是中文社区关于Crosswalk的首篇文章；版权归原作者所有。

![Crosswalk简介](/images/crosswalk-overview.png)

Web技术的优势早已被广大应用开发者熟知，比如可与云服务轻松集成，基于响应式UI设计的精美布局，高度的开放性，跨平台能力，高效的分发与部署等等。但是要充分利用Web技术的优势，仍然有许多障碍。Crosswalk项目正是为了跨越这些障碍而生。本文讲会简单介绍Crosswalk项目相关的概念和基本功能。

首先，Crosswalk采用Chrome浏览器的Blink渲染引擎并不断的快速演进(六周一次更新周期)，使Web应用在4.0版本之后的Android平台上充分享受Blink的性能优势。同时，我们支持最新的HTML5 API，包括WebGL，WebRTC，WebAudio，Screen Orientation，WebSocket等等。

有人可能会问，Android WebView自Android 4.4起已经采用Blink渲染引擎，这与Crosswalk有和不同？基于Chrome的WebView（Chrome WebView）和Crosswalk比起来目前存在两大缺陷：一是不被4.4之前的Android支持；二是性能以及功能与Chrome还有较大差别。主要的原因是Chrome WebView要向前兼容基于Android 4.4之前的WebView的应用。这意味着Chrome WebView要支持许多旧的功能，所以架构设计更为复杂，从而导致部分功能还没有完善，同时在某些情况下会降低性能。目前Chrome WebView的Canvas的性能所受影响最大，WebGL的性能与Crosswalk比也有所差距。由于Crosswalk不需要保持这种兼容性，它可以采用与Chrome浏览器非常相近的设计，事实上Crosswalk正是构建于Chromium的content模块之上，这使得它速度飞快并易于扩展与维护。同时还有相应的增强，比如Web应用不需要采用Chrome的多进程架构，这样运行时内存可以更加节省，等等。

## 起步

Crosswalk支持比较完善的Web技术，可以帮助Web开发者提高开发效率。例如像Polymer这样的Web组件模型框架可以在Crosswalk上顺利的工作，如同在Chrome浏览器中一样。同时对HTML5 API最大程度的支持让你的游戏与应用开发得心应手。

如果Crosswalk提供的API不能满足你的需求，我们还支持通过编写原生的Java代码来创建你自己的Web API。通过这种扩展机制用户可以轻松地获得他们所需的平台和设备能力。

如果你正在使用Cordova并且渴望更好的性能和更新的功能，如WebGL，那么Crosswalk是一个很好的选择。Crosswalk Cordova项目帮助你在Cordova中用Crosswalk替换原生的Android WebView，并将两者完美的融合，是不是两全其美？！当然，我们仍然支持Crodova的扩展机制，不过如果你的APP扩展对性能要求较高，采用Crosswalk自带的扩展机制是更好的选择。

## 打包你的应用

Crosswalk允许Web开发者将他们的应用打包成Android系统的应用安装包（APK），之后可以发布至应用商店，如Google Play。Crosswalk支持多个应用同时使用一个Crosswalk库的共享模式。但是大多数情况下开发者更倾向于将Crosswalk直接嵌入到应用本身。在这种嵌入模式下Web应用开发者可以完全控制Crosswalk的更新。例如在发布到应用商店之前在最新的Crosswalk上对应用进行测试，这是开发者这一直想要的功能。

创建一个APK的另外一种方法是使用Intel的XDK或者其它类似的工具，如Construct 2。Crosswalk也提供了自己的命令行工具，让开发者比较灵活地控制打包过程。这个命令行工具使用起来十分简单：写一个包含基本应用信息的manifest文件，然后运行一条命令就直接搞定！

## 将Web带入全新的领域

英特尔是开放Web应用开发平台的坚定支持者。我们致力于不断扩展Web平台的能力， 帮助开发者开发更加精良的应用而无需任何妥协。其中的一部分重要的工作是参与Web标准化社区，如W3C。英特尔积极参与各种规范制定工作组与其它Web领域的公司，如谷歌，Adobe，Mozilla等一同推动网络的标准化进程。

![基于Presentation API的HexGL游戏演示](/images/crosswalk-game-example.png)

标准化的制定需要大量时间，在整个过程中每一位参与者的反馈都需要被慎重考虑。Crosswalk一边不断试验各种Web前沿的功能，一边积极地反馈与影响标准的制定。更重要的是，Crosswalk确保这些被标准化的功能解决了现实的问题并帮助开发者创造更具吸引力的应用与用户体验。Presentation API就是这些实验性功能的一个典范。它由英特尔向标准化组织提出，并在Crosswalk中最早实现。使用Presentation API的Web应用可以将网页内容以无线连接的方式显示在其它的屏幕上。例如，使用一块大屏幕显示游戏的场景，用一块小触摸屏作为游戏的控制器，如上图所示。Crosswalk还在不断推出新的实验性API(比如将并行计算引入Web等 ) ，革新已有的API并积极参与长期的标准化工作， 不断推进Web技术进步！

## 后记

我们今后会带来一系列的文章来剖析Crosswalk项目的技术内幕，敬请期待！
