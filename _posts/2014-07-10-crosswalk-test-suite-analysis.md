---
layout: post
type: post
title: Crosswalk Test Suite代码库分析
---

顾名思义，[crosswalk-test-suite](https://github.com/crosswalk-project/crosswalk-test-suite)是Crosswalk项目的官方测试套件。（未完待续）

## crosswalk-test-suite编程语言统计与分析

[GitHub默认语言统计结果](https://github.com/crosswalk-project/crosswalk-test-suite/search?l=html)：

| 编程语言   | 文件数量 | 代码行数占比 |
| :--------- | -------: | -----------: |
| HTML       | 14891    | < 0.2%       |
| JavaScript | 1560     | 83.7%        |
| JSON       | 701      | < 0.2%       |
| Shell      | 595      | 5.7%         |
| XML        | 574      | < 0.2%       |
| CSS        | 549      | 3.4%         |
| XSLT       | 369      | 5.5%         |
| Python     | 231      | 1.5%         |
| PHP        | 53       | < 0.2%       |
| Java       | 13       | < 0.2%       |

从HTML和JavaScript的文件数量和代码行数占比来看，HTML文件数量几乎是JS文件数量的十倍，但代码行数却不足JS的千分之二；这很不合理。

找出所有的JS文件，`find . -name '*.js' -type f | sort`，发现：

- `testharness.js`: 237份，每份2222行代码
- `testharnessreport.js`: 228份，每份280行代码
- `unitcommon.js`: 51份，每份行代码
- `jquery-1.10.2.min.js`: 225份，每份4行代码；但第4行代码量很大，每份文件93107字节
- `testrunner.js`: 225份，每份851行代码

所以，完全可以把每个测试套件下的`resources\`和`webrunner\`提到最上层，只保留一份记录；同时提供一套打包使用的Python脚本，在打包之前把所有依赖的文件和结构拷贝到指定位置。

同样XSLT文件也类似，也可以将后两份从每个测试套件中剥离出来，放置顶层的`tools\`中：

- `summary.xsl`: 1份
- `testcase.xsl`: 202份
- `testresult.xsl`: 166份

`tests.xml`, `tests.full.xml`和`config.xml`虽然在每个测试套件里面都要，但因其内容互不相同，故而保留。
