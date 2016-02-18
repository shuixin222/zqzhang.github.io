---
layout: post
type: post
title: Exploring Battery Status API
---

# Introduction

As of 20 August 2015, W3C Battery Status API improved its `security and privacy
considerations` section since its W3C Candidate Recommendation 09 December 2014.

As CR exit criterion said, it needs two interoperable deployed implementations
of each feature. Among the only three browsers that supported the Battery Status
API, we chose Chrome and Firefox to explore the API since Opera is based on the
same browser engine (Blink) as Chrome.

The Battery Status API extends `window.navigator` with a `navigator.getBattery()`
method returning a battery promise, which is resolved in a `BatteryManager`
object providing also some new events (`chargingchange`, `levelchange`,
`chargingtimechange`, `dischargingtimechange`) you can handle to monitor the
battery status (`charging`, `chargingTime`, `dischargingTime`, `level`).



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
