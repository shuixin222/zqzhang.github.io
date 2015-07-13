---
layout: post
type: post
title: Web Assembly
---

> Web 应用程序较于原生应用之短在于性能。当然性能的问题不在于比较跑分高下，而在于用户体验。试想象一下，浏览器直接执行的游戏引擎代码是优化过的二进制中间表达形式（IR），甚至可能是缓存下来的后端转换过的机器码。[WebApp与Native App再战一轮？](http://tech.163.com/15/0709/09/AU2R65MF000948V8.html)

> [谷歌等巨头拟推全新网络应用标准WebAssembly](http://tech.163.com/15/0621/15/ASL5P1JJ000915BF.html)，旨在提高编译后Web应用程序的性能。

> [Google/微软/苹果联手：浏览器提速20倍！](http://news.mydrivers.com/1/435/435294.htm) WebAssembly是一种可用于未来浏览器中的字节码(bytecode)，可使浏览器性能提升20倍。字节码是一种机器可读的指令集，与高级语言相比，字节码的加载速度更快。WebAssembly项目旨在开发全新的字节码，从而让桌面和移动端浏览器变得更高效。


# W3C WebAssembly Community Group

* https://www.w3.org/community/webassembly/
* The mission of this group is to promote early-stage cross-browser collaboration on a new, portable, size- and load-time-efficient format suitable for compilation to the web.
* Chairs: Luke Wagner (Mozilla), Jean-Francois Bastien (Google), BRHAM GIRI ABHIJITH CHATRA (Microsoft).
* Non-Chair participants: 317 as of 20150701; .
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

1. AstSemantics: Abstract Syntax Tree Semantics: types, linear memory, local/global variables, control flow structures, calls, literals, expressions with control flow, 32/64-bit integer operations, floating point operations; datatype conversions, truncations, reinterpretations, promotions, and demotions.
2. BinaryEncoding: portable binary encoding of the Abstract Syntax Tree nodes, designed to allow fast startup, which includes reducing download size and allow for quick decoding.
3. CAndC++: Guide for C/C++ developers.
4. CodeOfConduct: Code of Ethics and Professional Conduct.
5. Contributing: Contributing to WebAssembly.
6. FAQ
7. FeatureTest: Any feature not present in the MVP (Minimum Viable Product) will have a corresponding feature test.
8. FutureFeatures: Feature to add after the MVP.
9. HighLevelGoals:
  1. Define a portable, size- and load-time-efficient binary format;
  2. Specify and implement incrementally;
  3. Design to execute within and integrate well with the existing Web platform;
  4. Design to support non-browser embeddings as well;
  5. Make a great platform.
10. MVP: Minimum Viable Product. The MVP will contain features which are available today in modern web browsers and which perform well even on mobile devices, which leads to roughly the same functionality as asm.js.
11. NonWeb: Non-Browser Embeddings, mainly node.js.
12. Nondeterminism: Nondeterminism in WebAssembly.
13. Polyfill: Polyfill to JavaScript.
14. Portability: WebAssembly's binary format is designed to be executable efficiently on a variety of operating systems and instruction set architectures, on the Web and off the Web.
15. PostMVP: Essential Post-MVP features: threads, fixed-width SIMD, zero-cost exception handling.
16. TextFormat
17. Tooling: editors, compilers and language virtual machines, debuggers, sanitizers for non-memory-safe languages, opt-in security enhancements for developers' own code, profilers, process dump.
18. UseCases: inside/outside the browser, how WebAssembly can be used?
  1. Entire code base in Web Assembly.
  2. Main frame in Web Assembly, but the UI is in JavaScript / HTML.
  3. Re-use existing code by targeting Web Assembly, embedded in a larger JavaScript / HTML application. This could be anything from simple helper libraries, to compute-oriented task offload.
19. Web: Browser Embedding.
