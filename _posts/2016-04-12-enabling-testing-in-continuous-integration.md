---
layout: post
type: post
title: Enabling Testing in Continuous Integration
---


## Background

The Crosswalk Project Extensions for RealSense implement the Intel RealSense
SDK API in JavaScript on top of the [Crosswalk application
runtime](https://crosswalk-project.org/) and its extensions framework. The
source code repository,
[realsense-extensions-crosswalk](https://github.com/crosswalk-project/realsense-extensions-crosswalk)
has been using [AppVeyor](https://www.appveyor.com/) as its continuous
integration (CI) and deployment system. This CI, however, misses testing.

For web platform testing, W3C has a fantastic testing framework,
[testharness.js](https://github.com/w3c/testharness.js) for writing low-level
tests of browser functionality in JavaScript. It provides a convenient API for
making assertions and is intended to work for both simple synchronous tests
and for tests of asynchronous behavior. [Crosswalk test
suite](https://github.com/crosswalk-project/crosswalk-test-suite/) has been
creating thousands of tests using this framework. Thus it is a good choice to
create tests using this testing framework for RealSense JavaScript APIs.

Therefore the problem here is how to enable the W3C testharness.js bassed tests
in realsense-extensions-crosswalk CI.

## Dumping test results

The [testharnessreport.js](https://github.com/w3c/testharness.js/blob/master/testharnessreport.js#L385)
provides a function to dump test results as below. 

```js
function dump_test_results(tests, status) {
    var results_element = document.createElement("script");
    results_element.type = "text/json";
    results_element.id = "__testharness__results__";
    var test_results = tests.map(function(x) {
        return {name:x.name, status:x.status, message:x.message, stack:x.stack}
    });
    var data = {test:window.location.href,
                tests:test_results,
                status: status.status,
                message: status.message,
                stack: status.stack};
    results_element.textContent = JSON.stringify(data);

    // To avoid a HierarchyRequestError with XML documents, ensure that 'results_element'
    // is inserted at a location that results in a valid document.
    var parent = document.body
        ? document.body                 // <body> is required in XHTML documents
        : document.documentElement;     // fallback for optional <body> in HTML5, SVG, etc.

    parent.appendChild(results_element);
}
```

Taking [battery-promise.html](http://w3c-test.org/battery-status/battery-promise.html)
as an example. Right click and open the link, you will get an online test
running. Press F12 and click "Elements", you will get a hidden element as

```html
<script type="text/json" id="__testharness__results__">
{
  "test":"http://w3c-test.org/battery-status/battery-promise.html",
  "tests":[
    {
      "name":"navigator.getBattery() return BatteryManager",
      "status":0,
      "message":null,
      "stack":null
    },
    {
      "name":"navigator.getBattery() shall always return the same promise",
      "status":0,
      "message":null,
      "stack":null
    }
  ],
  "status":0,
  "message":null,
  "stack":null
}
</script>
```

The `test` has 3 status values to indicate the testharness's status:

```json
{
  OK:0,
  ERROR:1,
  TIMEOUT:2
}
```

... while `tests` contains 4 status values to indicate each test's status:

```json
{
  PASS:0,
  FAIL:1,
  TIMEOUT:2,
  NOTRUN:3
}
```

Therefore all testing scripts need to properly handle the test results data.


## Reference

* [python实现SimpleHTTPServer的POST方法](http://blog.csdn.net/feier7501/article/details/9026577)
* [Implementing An HTTP Server for Python 2 and 3](http://douglatornell.ca/blog/category/python3-porting/)
* [Simple Python Http Server with Upload](https://gist.github.com/UniIsland/3346170)
* [Shutting down an HTTPServer](https://blog.gocept.com/2011/08/04/shutting-down-an-httpserver/)
* [How to shut down a Python TCPServer or HTTPServer or
  SimpleHTTPServer?](http://stackoverflow.com/questions/24226210/how-to-shut-down-a-python-tcpserver-or-httpserver-or-simplehttpserver)
* [MDN XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)
* [MDN Using XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest)
