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

这是 Crosswalk Test Suite 和 Tizen Web TCT 推荐测试执行工具，一轻量级命令行工具。

## [testkit/testkit-stub](https://github.com/testkit/testkit-stub)

该工具是配合宿主机端 testkit-lite 的部署在测试机端的桩。

## [testkit/tinyweb](https://github.com/testkit/tinyweb)

顾名思义，是微小的 Web 服务器工具，部署在测试机端（被测设备）。

## [testkit/webrunner](https://github.com/testkit/webrunner)

顾名思义，测试执行器。

## [GoogleChrome/samples](https://github.com/GoogleChrome/samples)

Google Chrome 各发布版本所引入的新特性的示例代码；用于测试 Crosswalk 每6周一次的与 Chromium 代码同步后，这些新特性是否能在 Crosswalk 运行时环境使用。

# Web Platform Tests

## [w3c/web-platform-tests](https://github.com/w3c/web-platform-tests)

W3C Web 平台规范的测试套件集群，涵盖几乎除 CSS 工作组所发布规范以外的所有规范的测试。其主要目的是用测试驱动 Web 规范的成熟并保证各实现方式方法符合规范要求。因为做 Tizen Web TCT 和 Crosswalk Test Suite 采用相同测试的方法，所以也给这个项目提交很多测试案例。并作为测试协调人，帮助诸如 Indexed DB, Server Sent Event, Vibration 等规范进入推荐候选标准。同时，因为主要检阅其他人提交的测试代码，所以现在有权限直接接受代码提交。

后续仍将花费小半时间来维护测试案例和添加新的测试案例。

## [w3c/csswg-test](w3c/csswg-test)

W3C CSS 工作组发布的规范所需测试套件集群；因为历史原因，它背后有一个测试套件编译系统，一个代码审查系统，所以还没有集成到 [w3c/web-platform-tests](https://github.com/w3c/web-platform-tests)。


后续仍将花费小半时间来维护测试案例和添加新的测试案例。

## [w3c/testharness.js](https://github.com/w3c/testharness.js)

这是 W3C JS 测试案例所依赖的测试框架，它提供了大量的断言接口，同时支持同步和异步测试。

2014年度，还支持了 Service Worker Promise 测试，详见[这里](https://github.com/w3c/testharness.js/pull/82)。

## [w3c/wptserve](https://github.com/w3c/wptserve)

专为使用 [w3c/web-platform-tests](https://github.com/w3c/web-platform-tests) 而设计的 Web 服务端。

## [w3c/pywebsocket](https://github.com/w3c/pywebsocket)

Google 的 WebSocket 服务端，它同时扩展了 Apache HTTP 服务端，意在支持 [w3c/web-platform-tests](https://github.com/w3c/web-platform-tests) 测试执行。

## [w3c/test-results](https://github.com/w3c/test-results)

基于 [darobin/wptreport](https://github.com/darobin/wptreport) 的 [w3c/web-platform-tests](https://github.com/w3c/web-platform-tests) 测试执行结果报告。

## [w3c/testtwf-website](https://github.com/w3c/testtwf-website)

http://testthewebforward.org/ 网站的源代码。该网站提供了一站式开放网络平台测试领域资源，包括文档、博客和历次 TestTWF 活动介绍和安排，是 W3C Web 测试领域不可多得的资料库。推荐每一位进入该领域的同学先通读一边，进而有选择的实践之。

## [darobin/wptreport](https://github.com/darobin/wptreport)

专为 [w3c/web-platform-tests](https://github.com/w3c/web-platform-tests) 测试执行结果而开发的报告生成器。

## [darobin/webidl2.js](https://github.com/darobin/webidl2.js)

[Web IDL](http://heycam.github.io/webidl/) 解析器，可供 [idlharness.js](https://github.com/w3c/testharness.js/blob/master/idlharness.js) 使用。

## [KhronosGroup/WebGL](https://github.com/KhronosGroup/WebGL)

WebGL 官方代码库，包括 [WebGL conformance suites](https://github.com/KhronosGroup/WebGL/tree/master/conformance-suites)。期待2015年在打扫 WebGL 测试案例时，能对此有所贡献。

## [KhronosGroup/WebCL-conformance](https://github.com/KhronosGroup/WebCL-conformance)

WebCL conformance tests，期待2015年打扫 WebCL 测试案例时，能对此有所贡献。

# HTML5 Chinese IG

## [w3c-html-ig-zh/w3c-glossary](https://github.com/w3c-html-ig-zh/w3c-glossary)

无他，W3C 翻译词汇表是每一位欲翻译 W3C 规范的童鞋都该好好掌握的东西；如果发现任何问题，都请及时反馈。

## [w3c-html-ig-zh/about](https://github.com/w3c-html-ig-zh/about)

这里字面意思是介绍 W3C HTML 中文兴趣小组整个代码库；但目前只有几个翻译须知和小技巧。

## [w3c-html-ig-zh/ES5](https://github.com/w3c-html-ig-zh/ES5)

这是应 Kenny 大大的呼吁，我从 http://www.w3.org/html/ig/zh/wiki/ES5 搬过来的翻译稿，将之整理和校对。本来计划 2014 年做完的，但因种种原因，没有完成，真是很抱歉。希望今年上半年完成它，并着手 ES6 的翻译工作。

# Popular Frameworks

## [jquery/jquery](https://github.com/jquery/jquery)

在 IVI TCT 的代码库中, 我们使用了4个版本的 jQuery： [jQuery v1.7](https://code.jquery.com/jquery-1.7.js), [v1.7.1](https://code.jquery.com/jquery-1.7.1.js), [v1.8.2](https://code.jquery.com/jquery-1.8.2.js) and [v1.10.2](https://code.jquery.com/jquery-1.10.2.js)。 考虑到将要基于 Bootstrap 来开发示例代码，会引入 [v1.11.1](https://code.jquery.com/jquery-1.11.2.js)，以及最新发布的 [v1.x](https://code.jquery.com/jquery-1.11.2.js)，我们很有可能引入6个版本的 jQuery！这实在是不能接受！不仅开发人员会迷惑，代码管理维护人员更是头大。我个人倾向于统一到最新版本，但需要证明它确实可行。更多的讨论见 [issue #875](https://github.com/crosswalk-project/crosswalk-test-suite/issues/875#issuecomment-68036384)。

## [jquery/jquery-mobile](https://github.com/jquery/jquery-mobile)

Tizen TCT Behavior Test tool 将 [jquery.mobile.js](https://github.com/crosswalk-project/crosswalk-test-suite/blob/master/behavior/js/thirdparty/jquery.mobile.js) 作为其用户界面框架。目前有同事欲将其替换为 [Bootstrap](https://github.com/twbs/bootstrap)。还未深入了解就要被废弃，但无论如何也要清楚它为什么会被替换。

## [twbs/bootstrap](https://github.com/twbs/bootstrap)

Bootstrap 近来很火，我也加了一把材。参考 http://testthewebforward.org/，我搭建了这个博客和分享系统。同时，项目将采取其可以开源的部件，重写手动测试；所以，需要更加深入了解之。

## [hakimel/reveal.js](https://github.com/hakimel/reveal.js)

自从进入 Web 领域，我就被教导要热情洋溢地使用 Web 技术，包括演讲稿。几经调研和对比，选择使用这个 reveal.js；用过好多次，感觉很不错。后续需要定制自己的模板。

## [w3c/respec](https://github.com/w3c/respec)

搞 W3C 技术规范，离不开这个工具；如果想编辑规范，更是要使用好这个工具才行；否则会给大家带来不便。
