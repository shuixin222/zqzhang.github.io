---
layout: post
type: post
title: Crosswalk 9 TODO List
---

Here only list what to be done by Zhiqiang during Crosswalk milestone 9 development.

## Crosswalk 9 Features

See the [current milestone features](https://crosswalk-project.org/jira/issues/?filter=11019) filter and watch the features so that you can receive update notification via emails.

| JIRA Ticket | Feature Description | More Info | Action |
| :---------- | :------------------ | :-------- | :----- |
| [XWALK-443](https://crosswalk-project.org/jira/browse/XWALK-443) | [Tizen] Package API | [tizen-extensions-crosswalk/pull/352](https://github.com/crosswalk-project/tizen-extensions-crosswalk/pull/352) | Liu Xin to review/create use-case tests |
| [XWALK-826](https://crosswalk-project.org/jira/browse/XWALK-826) | [Tizen] W3C Speech API | [speech-api spec](https://dvcs.w3.org/hg/speech-api/raw-file/tip/speechapi.html) | Xie Yunxiao to review/create use-case tests |
| [XWALK-865](https://crosswalk-project.org/jira/browse/XWALK-865) | [Tizen] Vehicle Signals API | [vehicle info spec](https://rawgit.com/w3c/automotive-bg/master/vehicle_spec.html) | Liu Xin to review/create use-case tests |
| [XWALK-1070](https://crosswalk-project.org/jira/browse/XWALK-1070) | [Tizen][IVI] Download API | [tizen-extensions-crosswalk/pull/352](https://github.com/crosswalk-project/tizen-extensions-crosswalk/pull/352) | Liu Xin to review/create use-case tests |
| [XWALK-1106](https://crosswalk-project.org/jira/browse/XWALK-1106) | [Tizen][IVI] SpeechSynthesis API | [speech-api spec](https://dvcs.w3.org/hg/speech-api/raw-file/tip/speechapi.html) | Xie Yunxiao to eview/create use-case tests |
| [XWALK-2310](https://crosswalk-project.org/jira/browse/XWALK-2310) | Support H.264 in WebRTC | [Patch for Google Chrome](https://groups.google.com/ forum/#!topic/discuss-webrtc/U-y3or-dBOU) | Liu Xin to review/create use-case tests at [XWALK-2326](https://crosswalk-project.org/jira/browse/XWALK-2326) |

Zhiqiang is also watching below features for HW video decoding and audio policy integration.

| JIRA Ticket | Feature Description | More Info | Action |
| :---------- | :------------------ | :-------- | :----- |
| [XWALK-1436](https://crosswalk-project.org/jira/browse/XWALK-1436) | Enable hardware acceleration video decoding for WebRTC in Tizen IVI | This feature depends on (1) upstream VP9 HW decoding work and (2) IVI HW driver | Make sure WebRTC is working
| [XWALK-1668](https://crosswalk-project.org/jira/browse/XWALK-1668) | Policy integration for web applications (audio tag) | Will be tested with the Tizen IVI Media Player app |
| [XWALK-1669](https://crosswalk-project.org/jira/browse/XWALK-1669) | Policy integration for WebAudio API | |
| [XWALK-1670](https://crosswalk-project.org/jira/browse/XWALK-1670) | Policy integration for WebRTC API | |

## Chromium 38 Features

See [Chromium Web Platform Features](http://www.chromestatus.com/features) for details.

| Feature | Description | Implementation Status | Specification | Upstream Test |
| :------ | :---------- | :-------------------- | :------------ | :------------ |
| `any-pointer` and `any-hover` Media Queries | Media queries for determining capabilities of a UA's pointer devices | Enabled by default | [http://www.w3.org/TR/2014/WD-mediaqueries-4-20140605/#any-input](http://www.w3.org/TR/2014/WD-mediaqueries-4-20140605/#any-input) | |
| File constructor | A programmatic method of constructing File objects, very similar to how Blob objects are built. | Enabled by default | [http://dev.w3.org/2006/webapi/FileAPI/#file](http://dev.w3.org/2006/webapi/FileAPI/#file) | |
| JS iterators (i.e. the for-of feature) (ES6)| Iterates over iterable objects (including arrays, array-like objects, iterators and generators), invoking a custom iteration hook with statements to be executed for the value of each distinct property. | Enabled by default | [https://people.mozilla.org/~jorendorff/es6-draft.html#sec-iteration-statements](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-iteration-statements) | |
| Map (ES6) | Map objects are simple key/value maps. | Enabled by default | [https://people.mozilla.org/~jorendorff/es6-draft.html#sec-map-objects](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-map-objects) | |
| Math functions (ES6) | Math related functions - `sign`, `trunc`, `sinh`, `cosh`, `tanh`, `asinh`, `acosh`, `atanh`, `log10`, `log2`, `hypot`, `fround`, `clz32`, `cbrt`, `log1p`, `expm1` (as `Math.sign(...)`, `Math.trunc(...)` and so on). | Enabled by default | [https://people.mozilla.org/~jorendorff/es6-draft.html#sec-math-object](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-math-object) | |
| Navigation Transitions | Allows web authors to both improve the perceived loading speed as well as provide visual polish by allowing two pages to coordinate on a transition animation (regardless of their origin). | Behind a flag | [Editor's draft](https://docs.google.com/document/d/17jg1RRL3RI969cLwbKBIcoGDsPwqaEdBxafGNYGwiY4/edit?pli=1#heading=h.pcll678prpwu) | |
| Screen Orientation API | Gives ability to read the screen orientation and lock it. | Enabled by default | [https://w3c.github.io/screen-orientation/](https://w3c.github.io/screen-orientation/) | [Blink Layout Tests](https://chromium.googlesource.com/chromium/blink/+/master/LayoutTests/screen_orientation/) |
| Set (ES6) | Set objects let you store unique values of any type, whether primitive values or object references. | Enabled by default | [http://wiki.ecmascript.org/doku.php?id=harmony:specification_drafts](http://wiki.ecmascript.org/doku.php?id=harmony:specification_drafts) | |
| Symbols (ES6) | Allows properties to be added to existing objects without the possibility of interference with the existing properties, unintended visibility, or with other uncoordinated additions by any other code. | Enabled by default | [https://people.mozilla.org/~jorendorff/es6-draft.html#sec-symbol-objects](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-symbol-objects) | |
| Unscopables (ES6) | Unscopables allows properties to be hidden to with statement lookup rules. This is important for adding new properties to existing objects both in JavaScript and in DOM. | Enabled by default | [https://people.mozilla.org/~jorendorff/es6-draft.html#sec-symbol.unscopables](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-symbol.unscopables) | |
| `image-rendering: pixelated` | `image-rendering: pixelated` indicates that image should be scaled "so that the image appears to be simply composed of very large pixels", e.g. using nearest-neighbour. | Enabled by default | [http://www.w3.org/TR/css4-images/#image-rendering](http://www.w3.org/TR/css4-images/#image-rendering) | Samples [jsfiddle.net/zda24/147/](jsfiddle.net/zda24/147/) |

## Test Case Tasks

| JIRA Ticket | Task Description | More Info | Action |
| :---------- | :--------------- | :-------- | :----- |
| [XWALK-2322](https://crosswalk-project.org/jira/browse/XWALK-2322) | [community][webapi] Create use-case test checking hide/recover several time | [XWALK-2199](https://crosswalk-project.org/jira/browse/XWALK-2199) `tizen.application.getCurrentApplication().hide()` works once | Create use-case tests |
| [XWALK-2326](https://crosswalk-project.org/jira/browse/XWALK-2326) | [community][webapi] Add test case for H.264 support of WebRTC | Depends on [XWALK-2310](https://crosswalk-project.org/jira/browse/XWALK-2310) | Liu Xin to create use-case or system tests |
| [XWALK-2331](https://crosswalk-project.org/jira/browse/XWALK-2331) | [community][webapi] Add test case for media source API test pause | Based on [XWALK-2231](https://crosswalk-project.org/jira/browse/XWALK-2231) | Create use-case or system tests |
| [XWALK-2367](https://crosswalk-project.org/jira/browse/XWALK-2367) | `height=device-height` viewport is overllaped by device buttons on tabblet | `<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,minimum-scale=1,user-scalable=no,height=device-height,minimal-ui">` | Create a test case |
| [XWALK-2368](https://crosswalk-project.org/jira/browse/XWALK-2368) | [webapi] BlobBuilder is deprecated | [BlobBuilder should not be supported](https://github.com/w3c/web-platform-tests/blob/master/FileAPI/historical.html); [Don't Build Blobs, Construct Them](http://updates.html5rocks.com/2012/06/Don-t-Build-Blobs-Construct-Them) | Xie Yunxiao to revise related test cases |
| [XWALK-2372](https://crosswalk-project.org/jira/browse/XWALK-2372) | [webapi] Update sreen orientation tests to reflect Chromium 38 implementation | [spec difference](http://services.w3.org/htmldiff?doc1=http%3A%2F%2Fwww.w3.org%2FTR%2F2012%2FWD-screen-orientation-20120522%2F&doc2=https%3A%2F%2Fw3c.github.io%2Fscreen-orientation%2F); [implementation status](http://www.chromestatus.com/features/6191285283061760); and [layout tests](https://chromium.googlesource.com/chromium/blink/+/master/LayoutTests/screen_orientation) | Liu Xin to revise related test cases |

## Test Upstream to W3C

1. [Create test cases for Vibration to cover the TODO list](http://lists.w3.org/Archives/Public/public-device-apis/2014Aug/0019.html)
2. [Review reference files submitted to csswg-test repo](https://github.com/w3c/csswg-test/pulls/chenxix)
3. [Review test cases for IndexedDB](https://github.com/w3c/web-platform-tests/labels/IndexedDB)
4. [Review test cases for Server Sent Event](https://github.com/w3c/web-platform-tests/labels/eventsource)
5. Regenerate test results after the above and report to working groups

