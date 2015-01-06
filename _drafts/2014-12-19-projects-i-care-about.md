---
layout: post
type: post
title: The Projects I Care About
---

# Crosswalk Tests

在过去的一年里，我大半的时间和精力都放在了 Crosswalk 项目的测试上，主要是测试套件和测试案例方面。

## [crosswalk-project/crosswalk-test-suite](https://github.com/crosswalk-project/crosswalk-test-suite)

2014年3月19日，经过一系列内部代码调整和定制以及版权信息检查，我们开源了该项目。此后，所有有关 Crosswalk 项目的测试套件和测试案例都在这里进行维护和开发，全部开源。

Crosswalk 项目本身是要构建一款跨平台（操作系统）的 Web 运行时环境，帮助应用程序开发者快速开发和部署应用程序；其目标之一是成为 Tizen 3.0 标配的运行时环境，基于此，Crosswalk Test Suite 采用 [Tizen Compliance Tests](https://source.tizen.org/compliance/compliance-tests) Web TCT 结构，并将 Web TCT 作为蓝本。这样，Crosswalk Test Suite 自产生就有了三个部分：[Behavior Test Tool](https://github.com/crosswalk-project/crosswalk-test-suite/tree/master/behavior), [Web APIs](https://github.com/crosswalk-project/crosswalk-test-suite/tree/master/webapi), [Web Runtime Core](https://github.com/crosswalk-project/crosswalk-test-suite/tree/master/wrt)。

Crosswalk 项目目前被广泛使用主要是因为它能够提供更好的性能和功能而取代 Android 默认的 WebView，同时兼容 Apache Cordova。所以，我们增加了两个部分的测试：[XwalkView Embedding APIs](https://github.com/crosswalk-project/crosswalk-test-suite/tree/master/embeddingapi) 和 [Crosswalk Cordova](https://github.com/crosswalk-project/crosswalk-test-suite/tree/master/cordova)。

Crosswalk 项目本身提出很多新的特性，针对这些新特性，我们站在应用程序开发者（最终用户）的角度开发了 [Use Case Tests](https://github.com/crosswalk-project/crosswalk-test-suite/tree/master/usecase)，用来验证这些特性的实现是否符合需求。这些测试案例基于 Behavior Test Tool 测试架构；后来成为示例代码库 demo-express 的基础。

一个运行时环境项目的成功，离不开长时间的稳定运行，[Stability Tests](https://github.com/crosswalk-project/crosswalk-test-suite/tree/master/stability) 即为此目的。此外，我们还开发了一些测试案例，用来验证 Crosswalk Documentation, Web Driver, Chromium 引入的新特性，等等；因为不好归类，放在 [misc](https://github.com/crosswalk-project/crosswalk-test-suite/tree/master/misc)。

Crosswalk Test Suite 本身也是一个独立的项目，离不开[文档](https://github.com/crosswalk-project/crosswalk-test-suite/tree/master/doc)和[工具](https://github.com/crosswalk-project/crosswalk-test-suite/tree/master/tools)的支持。

基于 Crosswalk Test Suite，我们创建了 [Tizen IVI 3.0 Compliance Tests](https://github.com/crosswalk-project/crosswalk-test-suite/tree/ivi-tct)，在不久的将来，会随着 Tizen IVI 3.0 M4 一起发布到 tizen.org 。

2015年，我想我还会投入很多时间和精力在这个项目上：

* 继续维护和开发 WebAPI 相关的测试案例和使用案例；确保 Crosswalk 所支持的特性有很好的质量；优先提交给 W3C, Khronos 等。
* 自动化集成和更新来自 W3C, Khronos等的测试案例；这一块之前做得不够好，手工耗时耗力。
* 优化整个项目代码结构，使整体代码尽可能无冗余，参见这些[问题报告](https://github.com/crosswalk-project/crosswalk-test-suite/issues)。
* 自动化代码格式检查和更新，简化测试案例开发人员的工作。
* 使用 [Travis CI](https://travis-ci.org/) 来检查每一个提交 (Pull Request)，保持项目的一致性。

## [crosswalk-project/demo-express](https://github.com/crosswalk-project/demo-express)

顾名思义，该项目主要是快速演示 Crosswalk 所支持的新特性。设计之初，就将该项目做成一个应用程序，使基于 Crosswalk 做产品开发的应用程序开发者以及潜在的 Crosswalk 使用者能够快速了解 Crosswalk 新特性的使用以及如何使用 Crosswalk 运行时环境。

该项目基于 [Use Case Tests](https://github.com/crosswalk-project/crosswalk-test-suite/tree/master/usecase) 来实现：将其中所涉及到的测试步骤和测试结果检查做成应用程序的使用步骤；进而实现两者代码级别差异，使之尽可能共用一套代码。

该项目荣获 Intel OTC System Enginieering Orientation (SEO) 部门奖认可 （DRA, Department Recogniation Award）。

后续将使用 [Bootstrap 框架](https://github.com/twbs/bootstrap) 来取代目前的 [jQuery Mobile 框架](https://github.com/jquery/jquery-mobile)；并开发更多的示例。

## [crosswalk-project/web-testing-service](https://github.com/crosswalk-project/web-testing-service)

Web Testing Service (WTS) 意在搭建一套 Web 测试服务，使得测试和开发人员能够很容易通过浏览器或者运行时环境快速执行测试案例，发现或者重现代码缺陷。目前因为种种原因，只在内部搭建这样一套服务器，公共服务还在争取之中。

## [crosswalk-project/crosswalk-web-driver](https://github.com/crosswalk-project/crosswalk-web-driver)

该项目基于 ChromeDriver 来实现 Crosswalk 的标准 WebDriver。我因为要使用 W3C 的测试案例来验证该实现是否符合标准，所以关注了它，并提交2个 PR 来修订它的 README 和 LICENSE。如有可能，花些精力帮助其实现，以期将现有的测试案例自动化。

## [testkit/testkit-lite](https://github.com/testkit/testkit-lite)

## [testkit/testkit-stub](https://github.com/testkit/testkit-stub)

## [testkit/tinyweb](https://github.com/testkit/tinyweb)

## [testkit/webrunner](https://github.com/testkit/webrunner)

## [GoogleChrome/samples](https://github.com/GoogleChrome/samples)


# Web Platform Tests

## [w3c/web-platform-tests](https://github.com/w3c/web-platform-tests)

## [w3c/csswg-test](w3c/csswg-test)

## [w3c/testharness.js](https://github.com/w3c/testharness.js)

## [w3c/wptserve](https://github.com/w3c/wptserve)

## [w3c/pywebsocket](https://github.com/w3c/pywebsocket)

## [w3c/test-results](https://github.com/w3c/test-results)

## [darobin/wptreport](https://github.com/darobin/wptreport)

## [darobin/webidl2.js](https://github.com/darobin/webidl2.js)

## [KhronosGroup/WebGL](https://github.com/KhronosGroup/WebGL)

## [KhronosGroup/WebCL-conformance](https://github.com/KhronosGroup/WebCL-conformance)


# HTML5 Chinese IG

## [w3c-html-ig-zh/w3c-glossary](https://github.com/w3c-html-ig-zh/w3c-glossary)

## [w3c-html-ig-zh/about](https://github.com/w3c-html-ig-zh/about)

## [w3c-html-ig-zh/ES5](https://github.com/w3c-html-ig-zh/ES5)


# Popular Frameworks

## [jquery/jquery](https://github.com/jquery/jquery)

In IVI TCT, there are 4 versions of jQuery used, [jQuery v1.7](https://code.jquery.com/jquery-1.7.js), [v1.7.1](https://code.jquery.com/jquery-1.7.1.js), [v1.8.2](https://code.jquery.com/jquery-1.8.2.js) and [v1.10.2](https://code.jquery.com/jquery-1.10.2.js). Considering the [v1.11.1](https://code.jquery.com/jquery-1.11.2.js) to be used by bootstrap demo, and the latest [v1.x](https://code.jquery.com/jquery-1.11.2.js), we may have 6 versions of jQuery! This is a nightmare and disaster for the whole test suites and tools development and maintaining. We need to unify them using one of the versions, preferring the latest one. See more discussion at [issue #875](https://github.com/crosswalk-project/crosswalk-test-suite/issues/875#issuecomment-68036384).

Moreover, I shall take a deep look at the source of of jQuery, even if for a better understanding and maintaining of our tests and tools.

## [jquery/jquery-mobile](https://github.com/jquery/jquery-mobile)

Tizen TCT Behavior Test tool leverages the [jquery.mobile.js](https://github.com/crosswalk-project/crosswalk-test-suite/blob/master/behavior/js/thirdparty/jquery.mobile.js) as its UI Framework. So I need to go through the source code and to check what we have used. And then compare it with the bootstrap framework to see why some guys want to replace it with bootstrap.

## [twbs/bootstrap](https://github.com/twbs/bootstrap)

I used this framework for this home page and my blog posts, with reference to the http://testthewebforward.org/; therefore, I need to learn more about it to make full use of it.

Moreover, one of my colleagues is working on the Behavior tool using this framework to get a better UI.

## [hakimel/reveal.js](https://github.com/hakimel/reveal.js)

I have used this HTML Presentation Framework for several talks and like it. However, I haven't dived into the source code to customize my own theme and template. It is time to do it for my talks posted here.

## [w3c/respec](https://github.com/w3c/respec)

Most W3C technical reports (aka spec) are created based on this JS library, specification edition support tool. If you want to be a spec editor, it is worthy of reading through the source code.

