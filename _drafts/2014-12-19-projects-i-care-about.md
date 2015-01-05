---
layout: post
type: post
title: Thinking of 2014 and 2015
---

# Crosswalk Tests

## [crosswalk-project/crosswalk-test-suite](https://github.com/crosswalk-project/crosswalk-test-suite)

## [crosswalk-project/demo-express](https://github.com/crosswalk-project/demo-express)

## [crosswalk-project/web-testing-service](https://github.com/crosswalk-project/web-testing-service)

## [crosswalk-project/crosswalk-web-driver](https://github.com/crosswalk-project/crosswalk-web-driver)

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

