---
layout: post
type: post
title: Web Assembly
---

> Web 应用程序较于原生应用之短在于性能。当然性能的问题不在于比较跑分高下，而在于用户体验。试想象一下，浏览器直接执行的游戏引擎代码是优化过的二进制中间表达形式（IR），甚至可能是缓存下来的后端转换过的机器码。[WebApp与Native App再战一轮？](http://tech.163.com/15/0709/09/AU2R65MF000948V8.html)

> [谷歌等巨头拟推全新网络应用标准WebAssembly](http://tech.163.com/15/0621/15/ASL5P1JJ000915BF.html)，旨在提高编译后Web应用程序的性能。

> [Google/微软/苹果联手：浏览器提速20倍！](http://news.mydrivers.com/1/435/435294.htm) WebAssembly是一种可用于未来浏览器中的字节码(bytecode)，可使浏览器性能提升20倍。字节码是一种机器可读的指令集，与高级语言相比，字节码的加载速度更快。WebAssembly项目旨在开发全新的字节码，从而让桌面和移动端浏览器变得更高效。


# W3C WebAssembly Community Group

* [https://www.w3.org/community/webassembly/](https://www.w3.org/community/webassembly/)
* The mission of this group is to promote early-stage cross-browser collaboration on a new, portable, size- and load-time-efficient format suitable for compilation to the web.
* Chairs: Luke Wagner (Mozilla), Jean-Francois Bastien (Google), BRHAM GIRI ABHIJITH CHATRA (Microsoft).
* Non-Chair participants: 317 as of 20150701; 357 as of 20150713.
* Mailing lists: [public-webassembly](https://lists.w3.org/Archives/Public/public-webassembly/), [public-webassembly-contrib](https://lists.w3.org/Archives/Public/public-webassembly-contrib/), [internal-webassembly](https://lists.w3.org/Archives/Member/internal-webassembly/).
* IRC: `irc://irc.w3.org:6667/#webassembly`.


# GitHub WebAssembly Organization

* [https://github.com/WebAssembly](https://github.com/WebAssembly): Development of WebAssembly and associated infrastructure.
* [design](https://github.com/WebAssembly/design): WebAssembly Design Documents.
* [experimental](https://github.com/WebAssembly/experimental): Loosely-coupled collection of quick-and-dirty experiments.
* [interpreter-prototype](https://github.com/WebAssembly/interpreter-prototype): A very early experimental prototype WebAssembly interpreter.
* [js-astcompressor-prototype](https://github.com/WebAssembly/js-astcompressor-prototype): Research prototype for investigating binary AST representation approaches.
* [polyfill-prototype-1](https://github.com/WebAssembly/polyfill-prototype-1): Experimental WebAssembly polyfill library and tools.
* [v8-native-prototype](https://github.com/WebAssembly/v8-native-prototype): Prototype native decoder that targets TurboFan.

Note:

* AST is an abbreviation of [abstract syntax tree](https://en.wikipedia.org/wiki/Abstract_syntax_tree). This research prototype is experimenting to find the best balance of post-compression size, pre-compression size, complexity, and decode speed.
* [TurboFan](http://ariya.ofilabs.com/2014/08/javascript-and-v8-turbofan.html) is a codename of a new, experimental optimizing compiler for Google’s V8 JavaScript engine.


# WebAssembly Design Documents

## [High Level Goals](https://github.com/WebAssembly/design/blob/master/HighLevelGoals.md)

1. Define a [portable](https://github.com/WebAssembly/design/blob/master/Portability.md), size- and load-time-efficient binary format.
2. Specify and implement incrementally: [Minimum Viable Product (MVP)](https://github.com/WebAssembly/design/blob/master/MVP.md) primarily aimed at [C/C++](https://github.com/WebAssembly/design/blob/master/CAndC%2B%2B.md), [polyfill](https://github.com/WebAssembly/design/blob/master/Polyfill.md), essential [post-MVP](https://github.com/WebAssembly/design/blob/master/PostMVP.md) features, [future features](https://github.com/WebAssembly/design/blob/master/FutureFeatures.md).
3. Design to execute within and integrate well with the existing [Web platform](https://github.com/WebAssembly/design/blob/master/Web.md).
4. Design to support [non-browser embeddings](https://github.com/WebAssembly/design/blob/master/NonWeb.md) as well.
5. Make a great platform: build a new LLVM backend for WebAssembly and an accompanying clang port; promote other compilers and tools targeting WebAssembly; and enable other useful [tooling](https://github.com/WebAssembly/design/blob/master/Tooling.md).

## [FAQ](https://github.com/WebAssembly/design/blob/master/FAQ.md)

1. Why create a new standard when there is already asm.js?
2. What are WebAssembly's use cases?
3. Can the polyfill really be efficient?
4. Is WebAssembly only for C/C++ programmers?
5. What compilers can I use to build WebAssembly programs?
6. Will WebAssembly support View Source on the Web?
7. What's the story for Emscripten users?
8. Is WebAssembly trying to replace JavaScript?
9. Why not just use LLVM bitcode as a binary format?

## [Use Cases](https://github.com/WebAssembly/design/blob/master/UseCases.md)

How WebAssembly can be used?

1. Entire code base in Web Assembly.
2. Main frame in Web Assembly, but the UI is in JavaScript / HTML.
3. Re-use existing code by targeting Web Assembly, embedded in a larger JavaScript / HTML application. This could be anything from simple helper libraries, to compute-oriented task offload.

## Other Documents

1. [AstSemantics](https://github.com/WebAssembly/design/blob/master/AstSemantics.md): Abstract Syntax Tree Semantics: types, linear memory, local/global variables, control flow structures, calls, literals, expressions with control flow, 32/64-bit integer operations, floating point operations; datatype conversions, truncations, reinterpretations, promotions, and demotions.
2. [BinaryEncoding](https://github.com/WebAssembly/design/blob/master/BinaryEncoding.md): portable binary encoding of the Abstract Syntax Tree nodes, designed to allow fast startup, which includes reducing download size and allow for quick decoding.


# Conclusion

WebAssembly is two things (at least):

1. Standardized way across all the browser houses to enable hybrid applications – on many dimensions.
2. Key component in Google OS convergence; kills NaCL and PNaCL.
