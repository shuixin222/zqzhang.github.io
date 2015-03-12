---
layout: post
type: post
title: 校订震动 API 中文译文至最新规范
---

## 背景

查阅 [HTML5 中文兴趣小组翻译列表](https://www.w3.org/html/ig/zh/wiki/%E7%BF%BB%E8%AF%91)时，赫然发现 Vibration API 后面标注 **需校订**。心想，何不趁此机会将自己主持过测试的标准规范的中文译文校订一下，然后推广给国内感兴趣的人？正好，前段时间这个规范被批准为 W3C 正式规范，也是设备 API 工作组6年来第一个正式规范；校订时，将中文翻译和最新版本的规范对应起来，会更好。所以，就动起手来，进行 **二次翻译**，或者说是 **统稿**。

## 校订

打定主意以[最新版的编辑草稿](http://dev.w3.org/2009/dap/vibration/)为基础，其实它和[最新发布的正式规范](http://www.w3.org/TR/vibration/)的内容完全一致，只是规范状态不同而已。规范是2014年11月19日版。

借用[有道翻译](http://fanyi.youdao.com/)将规范自动翻译一下，作为参考；所以 Vibration 被译为振动；然而原始译文使用 **震动**。查阅 **振动** 和 **震动** 的区别，有人给出这样的解释：

> **震动** 通常是指体积较为庞大的物体发生的短时间的偶尔一次或几次间断式的震动。比如地震、火车震动、房屋震动、坦克震动等等；也可用于抽象的东西，比如心灵和思想上的震动。

> **振动** 是指体积较小的物体，能持续一段时间的、机械式的连续的往复振动。如闹钟振铃、手机振动，等等。

通读规范，**震动** 是可行的、合适的。而后逐章节进行修订，所以统一翻译。中文译文详见：

[https://www.w3.org/html/ig/zh/wiki/Vibration_API](https://www.w3.org/html/ig/zh/wiki/Vibration_API)

## 收获

回头看，这次校订，其实是 **二次翻译**。此前的译文，规范定义接口(http://www.w3.org/TR/2012/WD-vibration-20120202/)为：

~~~
Navigator implements Vibration;

interface Vibration {
    void vibrate (unsigned long time) raises (NotSupportedError);
    void vibrate (unsigned long[] pattern) raises (NotSupportedError);
};
~~~

而今（http://www.w3.org/TR/2015/REC-vibration-20150210/）接口是：

~~~
typedef (unsigned long or sequence<unsigned long>) VibratePattern;

partial interface Navigator {
    boolean vibrate (VibratePattern pattern);
};
~~~

震动算法步骤也几易其稿，变动很大。逐段翻译之后，理解更清晰了。这更加增强继续进行校订和翻译其他规范的决心了。

## 后续

我想可以拜托 W3C 的朋友将该译文链接加到[正式规范](http://www.w3.org/TR/vibration/)提到的[非规范性翻译](http://www.w3.org/Consortium/Translation/)中去：

> The English version of this specification is the only normative version. Non-normative translations may also be available.

另一方面，也可以通过国内社区来推广之，比如[昨晚小组会议提到的SF](https://lists.w3.org/Archives/Public/public-html-ig-zh/2015Mar/0016.html)。

