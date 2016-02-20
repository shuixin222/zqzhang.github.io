---
layout: post
type: post
title: Testing Battery Status API
---

# Introduction

The Battery Status API extends `window.navigator` with a `navigator.getBattery()`
method returning a battery promise, which is resolved in a `BatteryManager`
object providing also some new events (`chargingchange`, `levelchange`,
`chargingtimechange`, `dischargingtimechange`) you can handle to monitor the
battery status (`charging`, `chargingTime`, `dischargingTime`, `level`).

To addvance the Battery Status API specification to Proposed Recommendation and
then to Recommendation from W3C Candidate Recommendation, it needs at least two
interoperable deployed implementations of each feature. Among the only three
browsers that supported the Battery Status API, we chose Chrome and Firefox to
explore the API as Opera is based on the same browser engine (Blink) as Chrome.

To check implementations interoperability, it is good to create a conformance
test suite based on the specification. This article is to describe how to create
such test suite, how to analyze failure and improve test cases, how to use the
test suite for using the Battery Status API in your applications.

# What to be tested?

## IDL fragments

Because the Battery Status API specification has a statement in Conformance
section as

> Implementations that use ECMAScript to implement the APIs defined in this
  specification must implement them in a manner consistent with the ECMAScript
  Bindings defined in the Web IDL specification, as this specification uses
  that specification and terminology.

... we are able to create a test file based on W3C
[idlharness.js](https://github.com/w3c/testharness.js/blob/master/idlharness.js)
testing framework to check the IDL fragments in this specification. See

http://w3c-test.org/battery-status/battery-interface-idlharness.html

Note that Google Chrome Version 49.0.2623.28 beta-m (64-bit) on Windows 8.1
has 4 failures which are not specific to Battery Status API:

* the first one due to throwing instead of rejecting on promise returning
  methods (in this case, getBattery())
* the second due to a general bug of Chrome with WebIDL, see [Chrome issue
  239915](https://code.google.com/p/chromium/issues/detail?id=239915)

## MUST, MUST NOT

The [RFC2119](https://tools.ietf.org/html/rfc2119) key word `must` defines an
absolute requirement of the specification, while `must not` defines an absolute
prohibition of the specification. Test suite shall has test cases cover all
statements in normative sections of the specification with one of the two key
words.

> The `getBattery()` method, when invoked, must run the following steps:

For this statement and the 5 steps followed, we can check that

* `navigator.getBattery()` return `BatteryManager`
* `navigator.getBattery()` shall always return the same promise

Thus created this test:

http://w3c-test.org/battery-status/battery-promise.html

# Reference

* [W3C Battery Status API Specification](https://www.w3.org/TR/battery-status/)
* [W3C Battery Status API test suite](http://w3c-test.org/battery-status/)
* [MDN Battery Status
  API](https://developer.mozilla.org/en-US/docs/Web/API/Battery_Status_API)
* [MDN Retrieving Battery status
  information](https://developer.mozilla.org/en-US/Apps/Build/gather_and_modify_data/retrieving_battery_status_information)
* [Using the Battery API – Part of
  WebAPI](https://hacks.mozilla.org/2012/02/using-the-battery-api-part-of-webapi/)
* [Google Chrome Battery Status
  Sample](https://github.com/GoogleChrome/samples/tree/gh-pages/battery-status)
* [Can I Use](http://caniuse.com/#feat=battery-status)
