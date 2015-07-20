---
layout: post
type: post
title: Crosswalk Weekly 9
---

# Crosswalk master has been rebased to M41

Crosswalk's master branch is now based on Chromium 41.0.2272.16, the first M41 release promoted to the Linux beta channel at [pull request #2838](https://github.com/crosswalk-project/crosswalk/pull/2838).

Web QA has checked below features enabled by default M41. Crosswalk 12.41.296.0 on Android gets the same results as Chrome 41.

* [any-pointer' and 'any-hover' Media Queries](https://github.com/GoogleChrome/samples/tree/gh-pages/media-hover-pointer)
* [Lexical Declarations (ES6)](https://github.com/GoogleChrome/samples/tree/gh-pages/lexical-declarations-es6)
* [Template Strings (ES6)](https://github.com/GoogleChrome/samples/tree/gh-pages/template-literals-es6)
* [WebAudio suspend/resume](https://github.com/GoogleChrome/samples/tree/gh-pages/webaudio-suspend-resume)
* [image-rendering: pixelated](https://github.com/GoogleChrome/samples/tree/gh-pages/image-rendering-pixelated)

Therefore, [XWALK-3364](https://crosswalk-project.org/jira/browse/XWALK-3364) is closed as resolved-fixed.

# Crosswalk for iOS is open source

[Crosswalk for iOS](https://github.com/crosswalk-project/crosswalk-ios/) is announced as open source on February 2nd. It is an extensible WebView which is built on top of WKWebView, the modern WebKit framework debuted in iOS 8.0. It provides fast Web runtime with carefully designed extension API for developing sophisticated iOS native or hybrid applications.

# Crosswalk Project Lite branch is available

[Crosswalk Project Lite](https://github.com/crosswalk-project/crosswalk/tree/crosswalk-lite) is the branch to focus on size reduction of the Crosswalk binary, by trying out different techniques and removing certain not-so-commonly-used features. Read more about it in [this blog post](https://crosswalk-project.org/blog/crosswalk-lite-10.html).

# Interest in commercial support for Crosswalk

Sandy Pérez, a project manager at a middle-sized company in Spain, [is interested in](https://lists.crosswalk-project.org/pipermail/crosswalk-help/2015-January/000750.html) commercial support for Crosswalk. They are developing hybrid HTML5 applications for the industrial market making intensive use of the CANbus. At the moment, They are exploring Crosswalk+Blink as an alternative of current being WebKit.

# Testing efforts required from community

* [XWALK-3555](https://crosswalk-project.org/jira/browse/XWALK-3555): [community][embedding] Need tests for transparent backgrounds
* [XWALK-3556](https://crosswalk-project.org/jira/browse/XWALK-3556): [community][embedding] Need tests for capturing Crosswalk Cordova webview touch events
