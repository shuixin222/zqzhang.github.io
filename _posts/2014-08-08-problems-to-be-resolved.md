> 总得时时寻一两个值得研究的问题！

[胡适这个方子](http://www.douban.com/note/289778846/)今儿在脑中盘旋甚久，挥之不去，这是好事儿；因为有几个问题困扰着。先写在这儿，待后续有解决方案时，再补充完整。

# 如何集成Blink Layout Tests到Crosswalk Test Suite？

评审[同事集成Blink NavigatorLanguage测试用例的代码提交](https://github.com/crosswalk-project/crosswalk-test-suite/pull/635)时，发现其在集成过程中，直接拷贝源代码文件部分内容（而不是整个文件），这给代码库的维护（尤其是版权声明）带来很大困难。所以就[试图改进之](https://github.com/crosswalk-project/crosswalk-test-suite/pull/658)。然而，这个所谓的改进，并没有解决同事所遇到的错误信息：

> Cannot read property 'setAcceptLanguages' of undefined

其原因是Blink测试框架定义了`window.testRunner.setAcceptLanguages`接口，而这个接口在Crosswalk的测试框架中并没有实现。好了，现在的问题是，如何把Blink的测试框架整合到Crosswalk的测试框架中？进而快速的整合Blink测试用例。

# 如何快速更新集成自W3C WPT和CSSWG的测试用例？

上次大规模的更新是几个月之前的事情了，费了好大劲，原因有三：

1. 代码组织结构完全不同，W3C主要考虑浏览器的测试，而Crosswalk和Tizen是运行时环境（Web Runtime）测试，前者可在线运行，而后者需要做成应用程序安装、执行、卸载；
2. 测试用例不完全集成，考虑运行时环境实现状况，没有完全集成W3C的测试用例，而是部分集成，甚至取部分测试文件中的部分测试用例，这就给筛选带来很大困难；
3. 执行工具差异甚大，运行时环境测试采用[testkit-lite](https://github.com/testkit/testkit-lite)自动化测试工具，需要将测试用例组织成具有一定格式的`tests.xml`，这个文件的生成，目前还不能完全自动化，详见下个问题。

目前，Blink和Gecko均实现了自动化或者半自动化集成和更新W3C测试用例，包括其测试框架。

# 如何准确高效地自动化生成`tests.xml`？

目前，已经有同学实现了单个文件仅有一个测试用例的情况，而对单个文件多个测试用例的情景，没有实现，只有一些想法。想将之攻克。

另，好几次都想，为何不能废弃[这个XML方案](https://github.com/testkit/testkit-lite/tree/master/xsd)，转投[W3C Manifest的方案](https://github.com/w3c/web-platform-tests/blob/master/tools/scripts/manifest.py)呢？

# [寒冬winter的9个题目](http://weibo.com/p/1001603741249222874725)

> 感兴趣的同学可以试试。

> 谈谈你对CSS布局的理解

> 讲讲输入完网址按下回车，到看到网页这个过程中发生了什么。

> 谈谈你对Web前端组件化的理解，Web Component会带来怎样的影响

> 谈谈你对前端资源下载性能优化的经验和思考

> 现在有很多的MV*框架，你对它们有什么看法

> iOS体验好在哪里，Web能赶上么？

> 网页游戏怎么做？

> Hybrid技术应当如何应用？

> 你最爱的前端框架是什么，为什么？
