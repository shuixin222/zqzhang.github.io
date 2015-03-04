---
layout: post
type: post
title: 审阅 CSS Animations 测试案例
---

## 背景

谢云霄针对 [CSS Animations](http://dev.w3.org/csswg/css-animations-1/) 属性能够应用到 [::before 和 ::after 伪元素](http://dev.w3.org/csswg/css-pseudo/#generated-content) 上 这一规范描述，提交了[几个测试案例](https://github.com/w3c/csswg-test/pulls/yunxiaoxie)给 W3C CSS 工作组。近20天过去了（期间有中国农历新年假期），这些测试案例并没有得到社区的审阅，所以我就花些时间来审阅它们，同时审阅 CSS Animations 测试套件是否完善。脑中有几个问题：

* [这些测试案例测试了哪些东西](https://github.com/w3c/csswg-test/pulls/yunxiaoxie)，有哪些问题？
* [CSS 工作组目前的动画规范测试套件都测试了哪些东西](https://github.com/w3c/csswg-test/tree/master/css-animations-1)，是否可以改进？
* [Crosswalk 测试套件里为何保有内部测试案例](https://github.com/crosswalk-project/crosswalk-test-suite/tree/master/webapi/tct-animations-css3-tests/animations)，是否可以提交给 CSS 工作组？
* [CSS Animations 规范](http://dev.w3.org/csswg/css-animations-1/)还有哪些部分没有测试到，即可测试规范空白？

## 谢云霄提交的测试案例

| Pull Request | Animation Property Name | Animation Property Value | Applies to |
| ------------ | ----------------------- | ------------------------ | ---------- |
| [#728](https://github.com/w3c/csswg-test/pull/728) | animation-timing-function | cubic-bezir, ease-in-out, ease-in, ease-out, ease | ::before, ::after |
| [#727](https://github.com/w3c/csswg-test/pull/727) | animation-play-state | paused, running | ::before, ::after |
| [#726](https://github.com/w3c/csswg-test/pull/726) | animation-name | none | ::before, ::after |
| [#725](https://github.com/w3c/csswg-test/pull/725) | animation-iteration-count | infinite, number | ::before, ::after |
| [#724](https://github.com/w3c/csswg-test/pull/724) | animation-fill-mode | backwards, both, forwards, none | ::before, ::after |
| [#720](https://github.com/w3c/csswg-test/pull/720) | animation-duration | time | ::before, ::after |
| [#717](https://github.com/w3c/csswg-test/pull/717) | animation-direction | alternate, alternate-reverse, normal, reverse | ::before, ::after |
| [#710](https://github.com/w3c/csswg-test/pull/710) | animation-delay | time | ::before, ::after |

### 测试案例分析

整体上，这些测试案例依据动画属性值枚举和两个伪元素的组合，构成 `<animation-property-name>-<animation-property-value>-pseudo-before` 和 `<animation-property-name>-<animation-property-value>-pseudo-after` 这样的测试。直观上，这些测试点无可厚非，也符合测试习惯。然而，考虑到 CSS 工作组现有的测试案例都是以 `<animation-property-name>-001` 和 `<animation-property-name>-002` 这样的方式命名，新添加的这些测试案例文件还是以序重命名为好，如 `animation-delay-004`。即 **重命名测试文件**。

这些测试案例依据最新发布版本（2013年2月19日）的规范 [http://www.w3.org/TR/css3-animations/](http://www.w3.org/TR/css3-animations/) 来编写的；然而考虑到最新编辑版本（2015年2月24日）的规范 [http://dev.w3.org/csswg/css-animations-1/](http://dev.w3.org/csswg/css-animations-1/) 已经有些许更新，还是以后者为好。即 **更新测试文件中的规范链接，甚至可能根据最新规范更新测试案例**。

纵观整个规范文档，和这两个伪元素相关的内容只有：

> Applies to: all elements, ::before and ::after pseudo-elements

我想，这也是这些测试案例的测试依据。然而，测试案例本身并不直观地反映这一点。以 [animation-play-state-paused-pseudo-after.html](https://github.com/yunxiaoxie/csswg-test/blob/animation-play-state/css-animations-1/animation-play-state-paused-pseudo-after.html) 为例，主要代码如下：

~~~
<style>
#content {
  border: 1px solid black;
  width: 150px;
}
#test::after {
  content: "::after";
}
#test {
  position: relative;
  animation-name: sample;
  animation-duration: 5s;
  animation-play-state: paused;
}
@keyframes sample {
  from {
    left: 150px;
  }
  to {
    left: 0px;
  }
}
</style>
<body>
  <p>Test passes if the '::after' doesn't move.</p>
  <div id="test"></div>
</body>
~~~

Animation 的相关属性并没有直接应用到 `::after` 伪元素上，而是应用到伪元素的原始元素即 `id` 是 `test` 的 `<div>` 元素上。从几个浏览器的测试结果上看，和直接作用在伪元素上是一致的。这有些让人费解。遇到这样费解的问题，通常会重读规范，看看浏览器的实现是否合乎规范。

[::before 和 ::after 伪元素的规范](http://dev.w3.org/csswg/css-pseudo/#generated-content)上有这么一段：

> They inherit any inheritable properties from their originating element; non-inheritable properties take their initial values as usual.

原来伪元素可以继承它原始元素里可继承的属性！ [CSS Animations 规范](http://dev.w3.org/csswg/css-animations-1/#values)上有这么一段：

> In addition to the property-specific values listed in their definitions, all properties defined in this specification also accept the `initial` and `inherit` keyword as their property value. For readability it has not been repeated explicitly.

原来如此！这样就可以解释通了，设置在 `#test` 上的动画属性，被继承到了 `#test::after`！然而，这样的写法，使得测试案例逻辑结构复杂了。即 **可以简化测试案例逻辑，将动画属性直接应用到伪元素上**。

回头再看这个测试代码，仍有如下问题：

* `<body>` 中只有 `<p>` 和 `<div>` 两个元素，完全没有必要使用 ID 选择器。即 **可以删除 ` id="test"`，使用元素选择器**。
* 填充文本使用 `content: "::after"`，看起来很糟糕。通常的做法是使用 `Filler Text`。即 **改进所有测试案例的填充文本，使用`Filler Text`**。
* 选择器 `#content` 没有对应的元素，属于未引用（unreferenced）代码，**应删除**。
* `Test passes if the '::after' doesn't move.` 这一测试结果判决条件，能让那些根本没有实现动画属性的用户代理得到 PASS 结果！是不可取的。所以要**改进测试案例，避免这样的结果**。
* `<title>CSS3 Animations Test` 中不应出现 3 这样的规范级别号；CSS 测试案例通常能被多个级别的规范使用，所以在标题中要避免使用级别号；可以使用 `<title>CSS Tests : CSS Animations :` （像目前的动画测试案例一样），或者使用 `<title>CSS Animations Test:`，个人倾向后一种。即 **删除 `<title>` 中的级别号，包括现有测试案例**。

## 工作组现有测试案例

