---
layout: post
type: post
title: Testing Effort for Crosswalk on Android 4.0
---

## Background

Because Google is [freezing Chrome for Ice Cream Sandwich](http://blog.chromium.org/2015/03/freezing-chrome-for-ice-cream-sandwich_3.html), [Chrome 42 will be the last supported release of Chrome for Android on all Ice Cream Sandwich (Android 4.0) devices](http://www.chromium.org/Home/ice-cream-sandwich-support-deprecation-faq). The Crosswalk Project comes to a real crosswalk: maintain Crosswalk on Android 4.0 or not?

Copy the reason of this change from Chromium blog post here:

> In the last year, we've seen the number of Chrome users running ICS drop by thirty percent. Developing new features on older phones has become increasingly challenging, and supporting ICS takes time away from building new experiences on the devices owned by the vast majority of our users. So, with Chrome's 42nd release, we'll stop updating Chrome on ICS devices. After Chrome 42, users on ICS devices can continue to use Chrome but won't get further updates.

## Questions

As Crosswalk Web QA, I was asked a question as:

> If Google doesn't run upstream tests on 4.0 we should do it ourselves, and we should make sure 4.0 is part of the weekly test. Is that feasible and at what cost?

Some intuitive testing efforts might be:

* upstream Chromium tests: execute them on Crosswalk weekly (How many tests? What is the automation rate of Chromium tests? How much time required for test execution, both auto testing time and manual testing time?)
* upstream Chromium tests: report out all failures as bugs but not like current test plan that we only report the regression of Crosswalk comparing with Chromium test results (Need to check latest results of Chromium project to see how many test failures on Chromium.)
* upstream Chromium tests: review and understand the tests code logic.
* Crosswalk W3C webapi tests: report out all failures as bugs but not like current test plan that we only report the regression of Crosswalk comparing with Chromium test results (Need check latest results to see how many test failures on Chromium?)
* How to access the Chromium tests in PRC?

## Testing for Chromium for Android

From the [Android Test Instructions](https://code.google.com/p/chromium/wiki/AndroidTestInstructions) wiki page, we can see that there are 4 types of tests running on Chromium for Android.

* Gtests: googletest-based C++ tests.
* Instrumentation Tests: InstrumentationTestCase-based Java tests.
* Blink Layout Tests: to verify the correctness of Chrome's graphically accelerated rendering pipeline.
* GPU Tests: to check the correctness of the renderer.

Per the [overview dashboard in the test result server](http://test-results.appspot.com/dashboards/overview.html#showNoFlakes=true), we can get the flaky and total count of the tests.

| Test Type | Flaky Count | Total Count | Applicable to Crosswalk |
| :-------- | :---------- | :---------- | :---------------------- |
| Gtests (content_unittests) | 3 | 3263 | Yes |
| Instrumentation Tests (ContentShellTest) | 1 | 403 | Yes |
| Instrumentation Tests (ChromeShellTest) | 31 | 357 | No |
| Instrumentation Tests (AndroidWebViewTest) | 3 | 428 | No |
| Blink Layout Tests (layout-tests) | 3774 | 42485 | Yes |
| GPU Tests (context_lost) | 5 | 6 | Yes |
| GPU Tests (memory_test) | 1 | 1 | Yes |
| GPU Tests (webgl_conformance) | 7 | 679 | Yes |
| GPU Tests (maps) | 1 | 1 | Yes |
| GPU Tests (angle_unittests) | 0 | 4832 | Yes |
| GPU Tests (content_gl_tests) | 0 | 19 | Yes |
| GPU Tests (gl_tests) | 0 | 94 | Yes |
| GPU Tests (gles2_conform_test) | 0 | 143 | Yes |

**Note**:

* All these tests are automated since they are running on Chromium Try Build server.
* Tests that fail due to a bad patch being committed are counted as **flaky**.
* The 'Applicable to Crosswalk' info above has been confirmed with Ningxin Hu and Lin Sun.
* Crosswalk Try Build server has enabled some Intel created Instrumentation tests.


