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
| [XWALK-443](https://crosswalk-project.org/jira/browse/XWALK-443) | [Tizen] Package API | [tizen-extensions-crosswalk/pull/352](https://github.com/crosswalk-project/tizen-extensions-crosswalk/pull/352) | Review/create use-case tests |
| [XWALK-826](https://crosswalk-project.org/jira/browse/XWALK-826) | [Tizen] W3C Speech API | [speech-api spec](https://dvcs.w3.org/hg/speech-api/raw-file/tip/speechapi.html) | Review/create use-case tests |
| [XWALK-865](https://crosswalk-project.org/jira/browse/XWALK-865) | [Tizen] Vehicle Signals API | [vehicle info spec](https://rawgit.com/w3c/automotive-bg/master/vehicle_spec.html) | Review/create use-case tests |
| [XWALK-1070](https://crosswalk-project.org/jira/browse/XWALK-1070) | [Tizen][IVI] Download API | [tizen-extensions-crosswalk/pull/352](https://github.com/crosswalk-project/tizen-extensions-crosswalk/pull/352) | Review/create use-case tests |
| [XWALK-1106](https://crosswalk-project.org/jira/browse/XWALK-1106) | [Tizen][IVI] SpeechSynthesis API | [speech-api spec](https://dvcs.w3.org/hg/speech-api/raw-file/tip/speechapi.html) | Review/create use-case tests |
| [XWALK-2310](https://crosswalk-project.org/jira/browse/XWALK-2310) | Support H.264 in WebRTC | [Patch for Google Chrome](https://groups.google.com/ forum/#!topic/discuss-webrtc/U-y3or-dBOU) | Review/create use-case tests at [XWALK-2326](https://crosswalk-project.org/jira/browse/XWALK-2326) |

Zhiqiang is also watching below features for HW video decoding and audio policy integration.

| JIRA Ticket | Feature Description | More Info | Action |
| :---------- | :------------------ | :-------- | :----- |
| [XWALK-1436](https://crosswalk-project.org/jira/browse/XWALK-1436) | Enable hardware acceleration video decoding for WebRTC in Tizen IVI | This feature depends on (1) upstream VP9 HW decoding work and (2) IVI HW driver | Make sure WebRTC is working
| [XWALK-1668](https://crosswalk-project.org/jira/browse/XWALK-1668) | Policy integration for web applications (audio tag) | Will be tested with the Tizen IVI Media Player app |
| [XWALK-1669](https://crosswalk-project.org/jira/browse/XWALK-1669) | Policy integration for WebAudio API | |
| [XWALK-1670](https://crosswalk-project.org/jira/browse/XWALK-1670) | Policy integration for WebRTC API | |

## Chromium 38 Features


## Test Case Tasks

| JIRA Ticket | Task Description | More Info | Action |
| :---------- | :--------------- | :-------- | :----- |
| [XWALK-2322](https://crosswalk-project.org/jira/browse/XWALK-2322) | [community][webapi] Create use-case test checking hide/recover several time | [XWALK-2199](https://crosswalk-project.org/jira/browse/XWALK-2199) `tizen.application.getCurrentApplication().hide()` works once | Create use-case tests |
| [XWALK-2326](https://crosswalk-project.org/jira/browse/XWALK-2326) | [community][webapi] Add test case for H.264 support of WebRTC | Depends on [XWALK-2310](https://crosswalk-project.org/jira/browse/XWALK-2310) | Create use-case or system tests |
| [XWALK-2331](https://crosswalk-project.org/jira/browse/XWALK-2331) | [community][webapi] Add test case for media source API test pause | Based on [XWALK-2231](https://crosswalk-project.org/jira/browse/XWALK-2231) | Create use-case or system tests |
| [XWALK-2367](https://crosswalk-project.org/jira/browse/XWALK-2367) | height=device-height viewport is overllaped by device buttons on tabblet | `<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,minimum-scale=1,user-scalable=no,height=device-height,minimal-ui">` | Create a test case |
| [XWALK-2368](https://crosswalk-project.org/jira/browse/XWALK-2368) | [webapi] BlobBuilder is deprecated | [BlobBuilder should not be supported](https://github.com/w3c/web-platform-tests/blob/master/FileAPI/historical.html); [Don't Build Blobs, Construct Them](http://updates.html5rocks.com/2012/06/Don-t-Build-Blobs-Construct-Them) | Revise related test cases |

## Test Upstream to W3C

1. [Create test cases for Vibration to cover the TODO list](http://lists.w3.org/Archives/Public/public-device-apis/2014Aug/0019.html)
2. [Review reference files submitted to csswg-test repo](https://github.com/w3c/csswg-test/pulls/chenxix)
3. [Review test cases for IndexedDB](https://github.com/w3c/web-platform-tests/labels/IndexedDB)
4. [Review test cases for Server Sent Event](https://github.com/w3c/web-platform-tests/labels/eventsource)
5. Regenerate test results after the above and report to working groups
