# Crosswalk Weekly 1

Crosswalk Weekly is a summary of activity on the Crosswalk Community from QA's
perspective, to get inputs to improve [crosswalk-test-suite]
(https://github.com/crosswalk-project/crosswalk-test-suite) test coverage and
approach.

## App crashes after some time because of Audio Decoder

Florian Landerl and Christoph Atteneder are using Crosswalk for their Apache
Cordova application and everything works great, except of application crashes
after some time on different devices.

In the [root cause discussion on the crosswalk-help mailing list]
(https://lists.crosswalk-project.org/pipermail/crosswalk-help/2014-July/000307.html),
this issue is recognized as a bug of WebAudio. Thus Florian creates [a sample
reproducing the issue](http://cl.ly/3F101r183I1a) and adds it to the comments of
a relevant bug report:
https://crosswalk-project.org/jira/browse/XWALK-1993

This sample can be converted to an use-case test at [webapi-usecase-w3c-tests]
(https://github.com/crosswalk-project/crosswalk-test-suite/tree/master/misc/webapi-usecase-w3c-tests).
Because the sample contains an audio clip, v-contra.mp3, and some scripts,
Zhiqiang is confirming with the author about the origin of the audio clip and
the scripts, to see if they are OK to be published under BSD 3-Claused License;
but haven't had any responses so far.

## Calling JS function from Java

Gokhan Gokce is trying to use Crosswalk Runtime in his Android app, but finds
that it is not working like Android WebView where he can call JS functions from
Java code. Though he eventually finds this issue is not about Crosswalk, the
`XWalkView.load` supporting JS schema is worthy a test case for Embedding API
testing, comparing to `loadUrl("javascript:xxx")` with Android WebView. See
[the thread at crosswalk-help]
(https://lists.crosswalk-project.org/pipermail/crosswalk-help/2014-July/000290.html)

## XHR Requests in XWalkView

Leonardo Tegon wants to make AJAX requests from index.html to local files
(images, sounds in same directory in phone sdcard) in XWalkView; and he gets
[a positive answer]
(https://lists.crosswalk-project.org/pipermail/crosswalk-help/2014-July/000304.html)
from Xingnan Wang that he can use either relative or absolute path to get
resources via XHR in XWalkView, `XWalkView.load("file://" + folderPath, null);`

So QA needs test cases to verify [Crosswalk Embedding API XWALKView]
(https://crosswalk-project.org/apis/embeddingapidocs/reference/org/xwalk/core/XWalkView.html)

