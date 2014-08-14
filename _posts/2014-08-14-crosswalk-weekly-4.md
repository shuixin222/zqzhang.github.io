---
layout: post
type: post
title: Crosswalk BuildBot中运行的测试用例
---

## 起因

Crosswalk在每6周一次的发布周期内，都会更新其代码库至最新的Chromium代码库，比如在[XWALK-1969](https://crosswalk-project.org/jira/browse/XWALK-1969)中Crosswalk 8更新至Chromium 37，这样就很自然地引入了Chromium的新特性，而验证这些特性在Crosswalk上的表现，就必需要执行一些测试。通常，Chromium/Blink在实现新特性时，都或多或少有些测试用例，关键就是何时以及如何运行这些测试用例。

去年底的时候，Raphael在[build.crosswalk-project.org](https://build.crosswalk-project.org/waterfall)上引入了runtime (instrumentation) tests
for Android，运行在搭载Android 4.0.4的X86设备上。所以就想能不能在这个系统中执行一部分来自[Blink Layout Tests](https://github.com/crosswalk-project/blink-crosswalk/tree/master/LayoutTests)的测试用例。

## 触发测试

如果有代码更新的话，`Crosswalk Release Engineering`每天下午三点左右会自动升级BUILD版本号，比如[Bump version to 9.37.192.0](https://github.com/crosswalk-project/crosswalk/commit/be731d79617136ba83bafb8ba699f0efee95c6d1)。该版本号增加后，会立即触发BuildBot产生一个Change号码，比如[Change #62601](https://build.crosswalk-project.org/changes/62601)，而后编译服务器会产生几个编译任务：[Crosswalk Android X86](https://build.crosswalk-project.org/builders/Crosswalk%20Android-X86/builds/1159)、[Crosswalk Linux](https://build.crosswalk-project.org/builders/Crosswalk%20Linux/builds/1192)、[Crosswalk Tizen 3 Mobile](https://build.crosswalk-project.org/builders/Crosswalk%20Tizen%203%20Mobile/builds/1087)、[Crosswalk Tizen Common](https://build.crosswalk-project.org/builders/Crosswalk%20Tizen%20Common/builds/546)、[Crosswalk Tizen IVI](https://build.crosswalk-project.org/builders/Crosswalk%20Tizen%20IVI/builds/705).

[Crosswalk Android X86](https://build.crosswalk-project.org/builders/Crosswalk%20Android-X86/builds/1159)编译成功之后，会触发事件[Crosswalk Tests (Android x86)](https://build.crosswalk-project.org/builders/Crosswalk%20Tests%20%28Android%20x86%29/builds/844)，来运行测试用例[XWalkCoreInternalTest, XWalkCoreTest, XWalkRuntimeClientEmbeddedTest, XWalkRuntimeClientTest](https://github.com/crosswalk-project/crosswalk/blob/master/xwalk_android_tests.gypi)和[make_apk_test](https://github.com/crosswalk-project/crosswalk/blob/master/app/tools/android/make_apk_test.py)。

## XWALK Android Tests

### XWalkCoreInternalTest

### XWalkCoreTest

### XWalkRuntimeClientEmbeddedTest

### XWalkRuntimeClientTest

## Make APK Test

## 结论

估计很难说服项目经理和配置管理工程师在BuildBot中运行验证新特性的测试用例；毕竟TryBot里面也在运行这些测试用例呢。但可以和项目经理讨论是否需要长期验证这些新特性，呵呵。