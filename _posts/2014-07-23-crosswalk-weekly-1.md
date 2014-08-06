# Crosswalk Weekly 1

Crosswalk Weekly is a summary of activity on the Crosswalk Community from QA's perspective, to get inputs to improve [crosswalk-test-suite](https://github.com/crosswalk-project/crosswalk-test-suite) test coverage and approach.

## App crashes after some time because of Audio Decoder

Florian Landerl and Christoph Atteneder are using Crosswalk for their Apache Cordova application and everything works great, except of application crashes after some time on different devices.

In the [root cause discussion on the crosswalk-help mailing list](https://lists.crosswalk-project.org/pipermail/crosswalk-help/2014-July/000307.html), this issue is recognized as a bug of WebAudio. Thus Florian creates [a sample reproducing the issue](http://cl.ly/3F101r183I1a) and adds it to the comments of a relevant bug report: https://crosswalk-project.org/jira/browse/XWALK-1993

Because the sample has used at least below features in webapi testing scope:
* WebAudio
* Audio element
* XMLHttpRequst
* Session history

... QA will create a test suite **misc/xwalk-system-tests** for this case.

Everyone can create test cases in this test suite if (s)he feels they are difficult to be in existing test suites, especially from samples, bugs and mailing lists from the community. This test suite will leverage behavior/usecase testing framework if no better option.

Florian Landerl has submitted the sample with some modification at https://github.com/crosswalk-project/crosswalk-test-suite/pull/515; and Jianfeng Xu wrapps it as a test case at [xwalk-system-tests](https://github.com/crosswalk-project/crosswalk-test-suite/tree/master/misc/xwalk-system-tests/tests/WebAudio).

## Calling JS function from Java

Gokhan Gokce is trying to use Crosswalk Runtime in his Android app, but finds that it is not working like Android WebView where he can call JS functions from Java code. Though he eventually finds this issue is not about Crosswalk, the `XWalkView.load` supporting JS schema is worthy a test case for Embedding API testing, comparing to `loadUrl("javascript:xxx")` with Android WebView. See [the thread at crosswalk-help](https://lists.crosswalk-project.org/pipermail/crosswalk-help/2014-July/000290.html) for details.

On [Stack Overflow](http://stackoverflow.com/questions/24601087/crosswalk-call-js-function-from-java-on-android), Gokhan Gokce insists on [`public void evaluateJavascript (String script, callback)`](https://crosswalk-project.org/apis/embeddingapidocs/reference/org/xwalk/core/XWalkView.html#evaluateJavascript(java.lang.String, <any>)) is better.

Zhiqiang has file a JIRA task, https://crosswalk-project.org/jira/browse/XWALK-2238, to create test cases for this.

## XHR Requests in XWalkView

Leonardo Tegon wants to make AJAX requests from index.html to local files (images, sounds in same directory in phone sdcard) in XWalkView; and he gets [a positive answer](https://lists.crosswalk-project.org/pipermail/crosswalk-help/2014-July/000304.html) from Xingnan Wang that he can use either relative or absolute path to get resources via XHR in XWalkView, `XWalkView.load("file://" + folderPath, null);`

Zhiqiang has file a JIRA task, https://crosswalk-project.org/jira/browse/XWALK-2238, to create test cases to verify [Crosswalk Embedding API XWALKView](https://crosswalk-project.org/apis/embeddingapidocs/reference/org/xwalk/core/XWalkView.html).

## Documentation about animatible XWalkView

Hongbo Min documents [Android SurfaceView v.s. TextureView](https://crosswalk-project.org/#wiki/Android-SurfaceView-vs-TextureView) to address potential questions like when to use animitable XWalkView and what is the difference, because the embedding API for Android supports the animatible XWalkView by use of TextureView as the target compositing surface.

Zhiqiang has file a JIRA task, https://crosswalk-project.org/jira/browse/XWALK-2239, to create some tests for the animatible XWalkView accordingly.

## Intent to Implement

1. **Remove application un/installation functionality from xwalk binary**
   [The install/uninstall/list-apps functionality will go to 'xwalkctl' binary](https://lists.crosswalk-project.org/pipermail/crosswalk-dev/2014-July/001638.html).    This change needs WRT tests if it becomes true.
2. **Tizen Web Application Protection**
   with reference to the [Tizen 2.x WRT Core Specification](https://source.tizen.org/sites/default/files/page/tizen-2.2-wrt-core-spec.pdf) and related features in JIRA [XWALK-1491](https://crosswalk-project.org/jira/browse/XWALK-1491), [XWALK-1172](https://crosswalk-project.org/jira/browse/XWALK-1172).
3. **W3C NFC API for Tizen**
   with [specification](http://www.w3.org/TR/nfc/), [feature XWALK-432](https://crosswalk-project.org/jira/browse/XWALK-432) and [implementation](https://github.com/crosswalk-project/tizen-extensions-crosswalk/pull/346).
4. **Pluggable extensions for	embedding API**
   with feature [XWALK-1052](https://crosswalk-project.org/jira/browse/XWALK-1152).
5. **Multiarch packages via	expansion files**
   with [Android Expansion File Info Spec](https://developer.android.com/google/play/expansion-files.html) and feature [XWALK-1626](https://crosswalk-project.org/jira/browse/XWALK-1626).
6. **Suspend and resume web	application for Tizen**
   with reference to the [Tizen 2.x WRT Core Specification](https://source.tizen.org/sites/default/files/page/tizen-2.2-wrt-core-spec.pdf) and related features in JIRA [XWALK-1497](https://crosswalk-project.org/jira/browse/XWALK-1497), [XWALK-1498](https://crosswalk-project.org/jira/browse/XWALK-1498).
7. **Extension Manager Tool for	Crosswalk Projects**
   with feature [XWALK-1947](https://crosswalk-project.org/jira/browse/XWALK-1947).
8. **Tizen Widget Signature**
   targets Crosswalk 9.

## Adding WebUI to Crosswalk (for Tizen)

Joone Hur is working on File-picker for Crosswalk and Chromium(Ozone-wayland) using WebUI.
* https://crosswalk-project.org/jira/browse/XWALK-950
* https://github.com/01org/ozone-wayland/issues/147

If that comes true, one can try to open `chrome://file-picker` and `chrome://gpu`. Thus Crosswalk provides system dialog boxes (file-picker or printing) and system menu (settings or help) like Chromium.

Shouqun Liu [added WebUI support for Crosswalk on Tizen](https://github.com/crosswalk-project/crosswalk/pull/2163) because Android port does not require WebUI.

However, Web QA needs a JIRA feature report to track such kind of feature/requirement to create some test cases checking it. Thus Zhiqiang adds a comment to the pull request to ask for a feature report.

## HTML5 Audio not working on Crosswalk Cordova or standard Cordova based WebView on Android 4.4

@patrickjquinn is trying to use the HTML Audio API to play a mp3 file from a remote HTTP source. Its flat out not working on either Android's default WebView based Cordova instance or using a Crosswalk Cordova blink based instance. The device is registering it as playing but no actual sound is emitted.

This question is still open at [Stack Overflow](http://stackoverflow.com/questions/24543387/html5-audio-not-working-on-crosswalk-cordova-or-standard-cordova-based-webview-o). But Zhiqiang thinks that the question is not clear to reproduce. Once the question is clear, QA may need to improve existing test case to cover it.

## Problem with accelerometer on Moto G

Robert Cohn runs this APK, https://drive.google.com/file/d/0B4MlW1-_vxuaNk1KUnFHQ1RGb1E/edit?usp=sharing, when playing the game, tilt the phone left & right to move the player; the player does not move on Moto G, but works on Nexus 4 and other phones. This issue is tracked at https://crosswalk-project.org/jira/browse/XWALK-2159; but sounds this is an issue of Chromium https://code.google.com/p/chromium/issues/detail?id=347507

QA will watch the [XWALK-2159](https://crosswalk-project.org/jira/browse/XWALK-2159) and verify it after Chromium fixes it together with Crosswalk rebase.

## Return the proper Error code when open the proper URL

Hengzi Wu reports [a bug that open a non-existed URL](https://crosswalk-project.org/jira/browse/XWALK-2158), e.g. "file:///android_asset/does_not_exist.html", the Error code should be `ERROR_FILE_NOT_FOUND` rather than `ERROR_UNKNOWN`.

However, QA does not know whether this error code is thrown by a Web API. If yes, QA needs to create test case. So a comment has been added to the JIRA bug to confirm with developer.

## `<a target="_blank">` does not work in Crosswalk Cordova

Gao Chun reports [a bug regards to `<a target="_blank">`](https://crosswalk-project.org/jira/browse/XWALK-2157): after click the hyper-link 'GO", the app should navigate to http://www.intel.com but the navigation failed. He also file bug https://crosswalk-project.org/jira/browse/XWALK-1037 to implement that hyperlink `<a target="_blank">` and method `window.open()` will be bridged to default browser.

There is an use-case test, `misc/cordova-usecase-android-tests/tests/TargetBlank/index.html`, for this feature. Zhiqiang has linked the 2 bugs and suggest improve the test if it doesn't cover the checkpoints. Belem Zhang thinks that he will add it to Cordova test case, and suggest to add a test case in Crosswalk WRT as well in different behaviors.

## XWalk Cordova doesn't seem to set `window.navigator.language` - always en-US

Lucas Gunn reports this issue at https://crosswalk-project.org/jira/browse/XWALK-2132.

QA is able to create a test case based on the steps to reproduce:
* Set Android phone language to Espanol (Estados Unidos)
* Create cordova app, log window.navigator.language, logs es-US
* Convert app to xwalk app
* Re-run, now it will log en-US

Belem thinks that this is not only a Cordova specific bug, and QA should have webapi test cases to cover this upstream Chromium issue. Zhiqiang file a JIRA task, https://crosswalk-project.org/jira/browse/XWALK-2242, to integrate test cases for `navigator.language`:
* https://github.com/crosswalk-project/blink-crosswalk/blob/master/LayoutTests/navigator_language/navigator_language.html
* https://github.com/w3c/web-platform-tests/blob/master/workers/interfaces/WorkerUtils/navigator/language.html

If possible, QA can help submit the Blink test to https://github.com/w3c/web-platform-tests/ at proper location.

## Rebase to Chromium 37

Francesco says in https://crosswalk-project.org/jira/browse/XWALK-1969 that for verification, ensure that Chromium 37 features are added to the test plan. For reference see http://www.chromestatus.com/features

At Chromium 37, there are 7 new features out of 11 in enabled by default implementation status without prefix. These features are:
* `<dialog>` Element
* CSS Shapes Module Level 1
* DirectWrite on Windows
* Navigator.hardwareConcurrency
* NavigatorLanguage: `navigator.languages` and `languagechange` event
* Subpixel font scaling
* Web Crypto API.

Because such kind of features are not tracked as Crosswalk Features, it is out of Crosswalk testing scope. QA is talking to developer managers and project manager about which features have been enabled by default on Crosswalk.

For the testable features, QA will run same tests on Chromium 37 and Crosswalk to compare the test; only difference will be reported as bug.

