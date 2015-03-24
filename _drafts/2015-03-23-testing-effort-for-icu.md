---
layout: post
type: post
title: Testing Effort for ICU
---

## Backgroud

To save binary size, Crosswalk Project Lite replaced ICU dependence with java utils at [blink-crosswalk PR#30](https://github.com/crosswalk-project/blink-crosswalk/pull/30/files) and [chromium-crosswalk PR#202](https://github.com/crosswalk-project/chromium-crosswalk/pull/202/files). Since the change made a great gain, Crosswalk Project is considering to pick it up back to master. It is said, however, that the change may result in some performace loss and strange behavior in line breaking and selection behavior. So we definitely need to test it carefully.

Therefore I am assigned to investigate the testing effort for the ICU (International Components for Unicode) replacement.

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

The [blink-crosswalk PR#30 patch](https://github.com/crosswalk-project/blink-crosswalk/pull/30.patch) has the following files changed:

~~~
Source/core/core.gyp
Source/core/editing/ReplaceSelectionCommand.cpp
Source/core/editing/TextIterator.cpp
Source/core/html/forms/EmailInputType.cpp
Source/core/rendering/RenderText.cpp
Source/platform/blink_platform.gyp
Source/platform/fonts/Character.cpp
Source/platform/fonts/Font.cpp
Source/platform/fonts/FontCache.h
Source/platform/fonts/FontDescription.h
Source/platform/fonts/GenericFontFamilySettings.h
Source/platform/fonts/harfbuzz/FontHarfBuzz.cpp
Source/platform/fonts/skia/FontCacheSkia.cpp
Source/platform/fonts/skia/SimpleFontDataSkia.cpp
Source/platform/text/LocaleICU.cpp
Source/platform/text/LocaleICU.h
Source/platform/text/SurrogatePairAwareTextIterator.cpp
Source/platform/text/TextBreakIterator.h
Source/platform/text/TextBreakIteratorICU.cpp
Source/platform/text/TextEncodingDetector.cpp
Source/platform/text/UnicodeUtilities.cpp
Source/web/SpellCheckerClientImpl.cpp
Source/web/web.gyp
Source/wtf/text/StringImpl.cpp
Source/wtf/text/TextCodecICU.h
Source/wtf/text/TextEncoding.cpp
Source/wtf/text/TextEncodingRegistry.cpp
Source/wtf/unicode/Collator.h
Source/wtf/unicode/icu/CollatorICU.cpp
Source/wtf/unicode/icu/UnicodeIcu.h
Source/wtf/wtf.gyp
~~~

The [chromium-crosswalk PR#202 patch](https://github.com/crosswalk-project/chromium-crosswalk/pull/202.patch) has the following files changed:

~~~
base/android/base_jni_registrar.cc
base/base.gyp
base/base.gypi
base/i18n/break_iterator.h
base/i18n/break_iterator_icu_alternatives.cc
base/i18n/build_utf8_validator_tables.cc
base/i18n/case_conversion.cc
base/i18n/file_util_icu.cc
base/i18n/icu_encoding_detection.cc
base/i18n/icu_string_conversions.cc
base/i18n/icu_string_conversions.h
base/i18n/icu_util.cc
base/i18n/number_formatting.cc
base/i18n/rtl.cc
base/i18n/string_compare.cc
base/i18n/string_compare.h
base/i18n/string_search.cc
base/i18n/time_formatting_icu_alternatives.cc
base/i18n/timezone.cc
base/icu_alternatives_on_android/break_iterator_bridge.cc
base/icu_alternatives_on_android/break_iterator_bridge.h
base/icu_alternatives_on_android/icu_utils.cc
base/icu_alternatives_on_android/icu_utils.h
base/icu_alternatives_on_android/java/src/org/chromium/base/icu/BreakIteratorBridge.java
base/icu_alternatives_on_android/java/src/org/chromium/base/icu/IcuUtils.java
build/common.gypi
content/browser/android/date_time_chooser_android.cc
content/child/web_url_loader_impl.cc
content/content_child.gypi
content/content_common.gypi
content/content_renderer.gypi
content/renderer/android/email_detector.cc
content/renderer/android/phone_number_detector.cc
content/renderer/render_view_impl.cc
net/base/net_util_icu_alternatives.cc
net/base/net_util_icu.cc
net/net.gyp
net/net.gypi
third_party/libxml/src/encoding.c
third_party/libxml/src/include/libxml/encoding.h
third_party/libxml/src/include/libxml/parser.h
third_party/libxml/src/include/libxml/xmlversion.h.in
third_party/libxml/src/parser.c
third_party/sqlite/sqlite.gyp
ui/android/java/src/org/chromium/ui/base/LocalizationUtils.java
ui/base/l10n/l10n_util_android.cc
ui/base/l10n/l10n_util.cc
ui/base/l10n/l10n_util_collator.h
ui/base/models/table_model.cc
ui/base/models/table_model.h
ui/base/ui_base.gyp
ui/gfx/gfx.gyp
ui/gfx/render_text.cc
ui/gfx/text_elider.cc
~~~

## Blink Layout Tests

~~~
LayoutTests/editing/*
LayoutTests/fonts/*
LayoutTests/fast/text/*
LayoutTests/fast/forms/*
LayoutTests/compositing/rendering-contexts.html
~~~

## Chromium Unit Tests

~~~
chromium-crosswalk/base/base_unittests.isolate
chromium-crosswalk/content/content_unittests.isolate
chromium-crosswalk/net/net_unittests.isolate
chromium-crosswalk/ui/base/ui_base_unittests.isolate
chromium-crosswalk/ui/gfx/gfx_unittests.isolate
~~~

