---
layout: post
type: post
title: Testing Effort for ICU
---

## Backgroud

To save binary size, Crosswalk Project Lite replaced ICU dependence with java utils at [blink-crosswalk PR#30](https://github.com/crosswalk-project/blink-crosswalk/pull/30/files) and [chromium-crosswalk PR#202](https://github.com/crosswalk-project/chromium-crosswalk/pull/202/files). Since the change made a great gain, Crosswalk Project is considering to pick it up back to master. It is said that, however, the change may result in some performace loss and strange behavior in line breaking and selection behavior. So we definitely to test it carefully.

And I am assigned to investigate the testing effort for the ICU (International Components for Unicode).

## What is ICU?

