---
layout: post
type: post
title: 校订振动 API 中文译文至最新规范
---

## 背景

查阅 [HTML5 中文兴趣小组翻译列表](https://www.w3.org/html/ig/zh/wiki/%E7%BF%BB%E8%AF%91)时，赫然发现 Vibration API 后面标注 **需校订**。心想，何不趁此机会将自己主持过测试的标准规范的中文译文校订一下，然后推广给国内感兴趣的人？正好，前段时间这个规范被批准为 W3C 正式规范，也是设备 API 工作组6年来第一个正式规范；校订时，将中文翻译和最新版本的规范对应起来，会更好。所以，就动起手来，进行 **二次翻译**，或者说是 **统稿**。

## 校订

打定主意以[最新版的编辑草稿](http://dev.w3.org/2009/dap/vibration/)为基础，其实它和[最新发布的正式规范](http://www.w3.org/TR/vibration/)的内容完全一致，只是规范状态不同而已。规范是2014年11月19日版。

借用[有道翻译](http://fanyi.youdao.com/)将规范自动翻译一下，作为参考；所以 Vibration 被译为振动；然而原始译文使用 **震动**。查阅 **振动** 和 **震动** 的区别，《咬文嚼字》2007年第9期 [《“手机振动”，还是“手机震动”》](http://www.pep.com.cn/xiaoyu/jiaoshi/study/jszy/yy/bzxc/201012/t20101203_981554.htm)一文是这样说的：

> 问：我是安徽某报纸的一名文字编辑，在审稿中经常碰到手机的一种设置状态zhèndòng，有的写作“振动”，有的写作“震动”。请问哪一种写法是妥当的？

> 答：“手机zhèndòng”，应该写作“手机振动”。“振动”，是指物体通过一个中心位置，不断作往返运动，这种运动是有规律的，其结果没有破坏性；“震动”，意即颤动、使颤动，是无规则的，其结果往往是消极的，甚至是破坏性的。我们知道，手机的zhèndòng设置，目的是提示主人有来电或短信，对手机本身无疑是没有破坏性的结果的，故而应写作“振动”。


通读规范，**振动** 是可行的、合适的。而后逐章节进行修订，所以统一翻译。中文译文详见：

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

振动算法步骤也几易其稿，变动很大。逐段翻译之后，理解更清晰了。这更加增强继续进行校订和翻译其他规范的决心了。

## 后续

我想可以拜托 W3C 的朋友将该译文链接加到[正式规范](http://www.w3.org/TR/vibration/)提到的[非规范性翻译](http://www.w3.org/Consortium/Translation/)中去：

> The English version of this specification is the only normative version. Non-normative translations may also be available.

另一方面，也可以通过国内社区来推广之，比如[昨晚小组会议提到的SF](https://lists.w3.org/Archives/Public/public-html-ig-zh/2015Mar/0016.html)。

