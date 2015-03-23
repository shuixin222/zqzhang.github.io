---
layout: post
type: post
title: Testing Effort for ICU
---

## Backgroud

To save binary size, Crosswalk Project Lite replaced ICU dependence with java utils at [blink-crosswalk PR#30](https://github.com/crosswalk-project/blink-crosswalk/pull/30/files) and [chromium-crosswalk PR#202](https://github.com/crosswalk-project/chromium-crosswalk/pull/202/files). Since the change made a great gain, Crosswalk Project is considering to pick it up back to master. It is said, however, that the change may result in some performace loss and strange behavior in line breaking and selection behavior. So we definitely to test it carefully.

And I am assigned to investigate the testing effort for the ICU (International Components for Unicode).

## What is ICU?

The [ICU Project](http://site.icu-project.org/home#TOC-What-is-ICU-) says that:

> ICU is a mature, widely used set of C/C++ and Java libraries providing Unicode and Globalization support for software applications.

> ICU is widely portable and gives applications the same results on all platforms and between C/C++ and Java software.

> ICU provides the following services:

> - **Code Page Conversion**: Convert text data to or from Unicode and nearly any other character set or encoding.
> - **Collation**: Compare strings according to the conventions and standards of a particular language, region or country.
> - **Formatting**: Format numbers, dates, times and currency amounts according the conventions of a chosen locale.
> - **Time Calculations**: Multiple types of calendars are provided beyond the traditional Gregorian calendar.
> - **Unicode Support**: ICU closely tracks the Unicode standard.
> - **Regular Expression**: ICU's regular expressions fully support Unicode while providing very competitive performance.
> - **Bidi**: support for handling text containing a mixture of left to right (English) and right to left (Arabic or Hebrew) data.
> - **Text Boundaries**: Locate the positions of words, sentences, paragraphs within a range of text, or identify locations that would be suitable for line wrapping when displaying the text.

## Replacing ICU dependence


