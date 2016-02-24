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

> The user agent must not reject the battery promise.

This statement indicates that

```js
navigator.getBattery().then(function(battery) {
  // battery checking
}, function(error) {
  // assert_unreached(error.message);
});
```

> The `charging` attribute must be set to `false` if the battery is discharging,
  and set to `true`, if the battery is charging, the implementation is unable to
  report the state, or there is no battery attached to the system, or otherwise.

> The `level` attribute must be set to 0 if the system's battery is depleted and
  the system is about to be suspended, and to 1.0 if the battery is full, the
  implementation is unable to report the battery's level, or there is no battery
  attached to the system. When the battery level is updated, the user agent must
  queue a task which sets the `level` attribute's value and fires a simple event
  named `levelchange` at the `BatteryManager` object.

Together with other statements for `chargingTime` and `dischargingTime`,
we designed these test files

http://w3c-test.org/battery-status/battery-charging-manual.html

http://w3c-test.org/battery-status/battery-discharging-manual.html

http://w3c-test.org/battery-status/battery-full-manual.html

... to check battery status (`charging`, `chargingTime`, `dischargingTime`,
`level`) and the `levelchange` event fired during charging or discharging.

However it is difficult to check the `chargingtimechange` or
`dischargingtimechange` events because the definition of how often these two
events are fired is left to the implementation. Though the specification has
these statements.

> When the battery charging time is updated, the user agent must queue a task
  which sets the `chargingTime` attribute's value and fires a simple event named
  `chargingtimechange` at the `BatteryManager` object.

> When the battery discharging time is updated, the user agent must queue a task
  which sets the `dischargingTime` attribute's value and fires a simple event
  named `dischargingtimechange` at the `BatteryManager` object.


We then designed these test files trying to get all the 4 events fired in each
condition but failed.

http://w3c-test.org/battery-status/battery-plugging-in-manual.html

http://w3c-test.org/battery-status/battery-unplugging-manual.html

# Failure analysis

To root cause failures of the tests above, we developed an example to read out
all events fired and the battery status to check what happened.

https://zqzhang.github.io/demo/battery/example.html

```js
window.onload = function () {
  var numOfEvents = 0;

  function updateBatteryStatus(battery, event) {
    var node = document.createElement('div');
    if (event) {
      numOfEvents += 1;
      node.textContent = 'Event #' + numOfEvents + ' ' + event + ': ';
    }
    node.textContent += battery.charging ? 'charging:' : 'not charging:';
    node.textContent += ' chargingTime ' + battery.chargingTime;
    node.textContent += ' dischargingTime ' + battery.dischargingTime;
    node.textContent += ' level ' + battery.level;
    document.body.appendChild(node);
  }

  navigator.getBattery().then(function(battery) {
    // Update the battery status initially when the promise resolves ...
    updateBatteryStatus(battery);

    // .. and for any subsequent updates.
    battery.onchargingchange = function () {
      updateBatteryStatus(battery, 'chargingchange');
    };

    battery.onchargingtimechange = function () {
      updateBatteryStatus(battery, 'chargingtimechange');
    };

    battery.ondischargingtimechange = function () {
      updateBatteryStatus(battery, 'dischargingtimechange');
    };

    battery.onlevelchange = function () {
      updateBatteryStatus(battery, 'levelchange');
    };
  });
};
```

## Google Chrome 49 beta on Windows 8.1

```
not charging: chargingTime Infinity dischargingTime 2580 level 0.61
[charger plugged in]
Event #1 dischargingtimechange: not charging: chargingTime Infinity dischargingTime Infinity level 0.6
Event #2 levelchange: not charging: chargingTime Infinity dischargingTime Infinity level 0.6
Event #3 chargingchange: charging: chargingTime Infinity dischargingTime Infinity level 0.6
Event #4 levelchange: charging: chargingTime Infinity dischargingTime Infinity level 0.48
Event #5 levelchange: charging: chargingTime Infinity dischargingTime Infinity level 0.61
Event #6 levelchange: charging: chargingTime Infinity dischargingTime Infinity level 0.76
Event #7 levelchange: charging: chargingTime Infinity dischargingTime Infinity level 0.82
Event #8 chargingtimechange: charging: chargingTime 0 dischargingTime Infinity level 1
Event #9 levelchange: charging: chargingTime 0 dischargingTime Infinity level 1
[full charged]
[charger unplugged in]
Event #10 chargingchange: not charging: chargingTime Infinity dischargingTime Infinity level 0.95
Event #11 chargingtimechange: not charging: chargingTime Infinity dischargingTime Infinity level 0.95
Event #12 levelchange: not charging: chargingTime Infinity dischargingTime Infinity level 0.95
Event #13 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 6010 level 0.58
Event #14 levelchange: not charging: chargingTime Infinity dischargingTime 6010 level 0.58
[charger plugged in]
Event #15 chargingchange: charging: chargingTime Infinity dischargingTime Infinity level 0.58
Event #16 dischargingtimechange: charging: chargingTime Infinity dischargingTime Infinity level 0.58
Event #17 chargingtimechange: charging: chargingTime 0 dischargingTime Infinity level 1
Event #18 levelchange: charging: chargingTime 0 dischargingTime Infinity level 1
Event #19 chargingtimechange: charging: chargingTime Infinity dischargingTime Infinity level 0.86
Event #20 levelchange: charging: chargingTime Infinity dischargingTime Infinity level 0.86
Event #21 levelchange: charging: chargingTime Infinity dischargingTime Infinity level 0.87
Event #22 levelchange: charging: chargingTime Infinity dischargingTime Infinity level 0.88
[charger unplugged in]
Event #23 chargingchange: not charging: chargingTime Infinity dischargingTime Infinity level 0.88
Event #24 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 9719 level 0.87
Event #25 levelchange: not charging: chargingTime Infinity dischargingTime 9719 level 0.87
Event #26 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 8518 level 0.86
Event #27 levelchange: not charging: chargingTime Infinity dischargingTime 8518 level 0.86
Event #28 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 3853 level 0.54
Event #29 levelchange: not charging: chargingTime Infinity dischargingTime 3853 level 0.54
```

From the log above, we can see that Chrome for desktop

* gets often level changes;
* always reports `chargingTime` as `Infinity` until the battery is full where
  it reports 0; thus
* [battery-plugging-in-manual.html](http://w3c-test.org/battery-status/battery-plugging-in-manual.html)
  has to run long time to complete the tests; and
* [battery-unplugging-manual.html](http://w3c-test.org/battery-status/battery-unplugging-manual.html)
  cannot get all 4 events fired (Event #23 to #29) given the current being
  test pre-condition that the battery must not be full or reach full capacity
  during the time the test is run.

However, if we remove the battery not full pre-condition from these two test
files, we can get all 4 events fired after charger plugged in (event #1 to #8),
or after the charger unplugged in (event #10 to #14).

## Firefox Nightly 47 on Windows 8.1

```
not charging: chargingTime Infinity dischargingTime 2580 level 0.6
[charger plugged in]
Event #1 dischargingtimechange: not charging: chargingTime Infinity dischargingTime Infinity level 0.6
Event #2 chargingchange: charging: chargingTime Infinity dischargingTime Infinity level 0.6
Event #3 levelchange: charging: chargingTime Infinity dischargingTime Infinity level 0.5
Event #4 levelchange: charging: chargingTime Infinity dischargingTime Infinity level 0.6
Event #5 levelchange: charging: chargingTime Infinity dischargingTime Infinity level 0.7
Event #6 levelchange: charging: chargingTime Infinity dischargingTime Infinity level 0.8
Event #7 levelchange: charging: chargingTime Infinity dischargingTime Infinity level 0.9
Event #8 levelchange: charging: chargingTime 0 dischargingTime Infinity level 1
Event #9 chargingtimechange: charging: chargingTime 0 dischargingTime Infinity level 1
Event #10 levelchange: charging: chargingTime Infinity dischargingTime Infinity level 0.6
Event #11 chargingtimechange: charging: chargingTime Infinity dischargingTime Infinity level 0.6
Event #12 levelchange: charging: chargingTime 0 dischargingTime Infinity level 1
Event #13 chargingtimechange: charging: chargingTime 0 dischargingTime Infinity level 1
[full charged]
[charger unplugged in]
Event #14 chargingchange: not charging: chargingTime Infinity dischargingTime Infinity level 1
Event #15 chargingtimechange: not charging: chargingTime Infinity dischargingTime Infinity level 1
Event #16 levelchange: not charging: chargingTime Infinity dischargingTime 9074 level 0.9
Event #17 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 9074 level 0.9
Event #18 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 10173 level 0.9
Event #19 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 9003 level 0.9
Event #20 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 9990 level 0.9
Event #21 levelchange: not charging: chargingTime Infinity dischargingTime 6390 level 0.6
Event #22 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 6390 level 0.6
Event #23 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 5795 level 0.6
Event #24 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 5784 level 0.6
Event #25 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 6010 level 0.6
[charger plugged in]
Event #26 chargingchange: charging: chargingTime Infinity dischargingTime Infinity level 0.6
Event #27 dischargingtimechange: charging: chargingTime Infinity dischargingTime Infinity level 0.6
Event #28 levelchange: charging: chargingTime 0 dischargingTime Infinity level 1
Event #29 chargingtimechange: charging: chargingTime 0 dischargingTime Infinity level 1
Event #30 levelchange: charging: chargingTime Infinity dischargingTime Infinity level 0.9
Event #31 chargingtimechange: charging: chargingTime Infinity dischargingTime Infinity level 0.9
[charger unplugged in]
Event #32 chargingchange: not charging: chargingTime Infinity dischargingTime Infinity level 0.9
Event #33 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 9719 level 0.9
Event #34 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 8518 level 0.9
Event #35 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 8472 level 0.9
Event #36 levelchange: not charging: chargingTime Infinity dischargingTime 8064 level 0.8
Event #37 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 8064 level 0.8
Event #38 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 7984 level 0.8
Event #39 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 6577 level 0.8
Event #40 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 7531 level 0.8
Event #41 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 8335 level 0.8
Event #42 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 6066 level 0.8
Event #43 levelchange: not charging: chargingTime Infinity dischargingTime 4243 level 0.6
Event #44 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 4243 level 0.6
Event #45 levelchange: not charging: chargingTime Infinity dischargingTime 3853 level 0.5
Event #46 dischargingtimechange: not charging: chargingTime Infinity dischargingTime 3853 level 0.5
```

From the log above, we can see that Firefox for desktop

* gets often dischargingTime changes than level;
* always reports `chargingTime` as `Infinity` until the battery is full where
  it reports 0.

However, if we remove the battery not full pre-condition from these two test
files, we can get all 4 events fired after charger plugged in (event #1 to #9),
or after the charger unplugged in (event #14 to #17).

# What to do next?

Remove the test pre-condition that "the battery must not be full or reach full
capacity during the time the test is run" from
[battery-plugging-in-manual.html](http://w3c-test.org/battery-status/battery-plugging-in-manual.html)
and
[battery-unplugging-manual.html](http://w3c-test.org/battery-status/battery-unplugging-manual.html)

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
