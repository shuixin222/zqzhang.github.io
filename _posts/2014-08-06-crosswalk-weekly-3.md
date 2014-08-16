---
layout: post
type: post
title: Crosswalk Weekly 3
---

## Make Good Use of GitHub Issues

Crosswalk QA Team once decided to use [Crosswalk JIRA -> Test Suite](https://crosswalk-project.org/jira/browse/XWALK/component/10303) to track the tasks of creating test cases to cover the test gaps from the community feedback. This will sharply increase the number of JIRA tickets which makes the crosswalk test suite component of the JIRA system ugly and impenetrable. Thus the team has to seek for other means to track the TODO list.

Someone suggests leverage existing JIRA instance internally, but Zhiqiang strongly disagrees to use any kind of internals for the open sourced project. One of the shortcomings is that internal tracking system will make the task tracking and contribution from outside hard and dilemma.

Someone advices to send emails about the tasks to the component owner and related persons; but it is impossible to track the tasks status, not to say effectively handle the tasks.

Finally, the team find out the [crosswalk-test-suite issues](https://github.com/crosswalk-project/crosswalk-test-suite/issues) and file some tasks as below.

![crosswalk-test-suite open issues](/images/crosswalk-test-suite-issues.png)

When file an issue, one is able to [assign it to proper test case developer](https://help.github.com/articles/assigning-issues-and-pull-requests-to-other-github-users), to [tag it with labels](https://help.github.com/articles/applying-labels-to-issues-and-pull-requests), and to [group it together Crosswalk milestones](https://help.github.com/articles/creating-and-editing-milestones-for-issues-and-pull-requests). As shown in the above figure, there are several labels: `system test`, `task`, `tizen`, `android`, etc.

One can filter kinds of bugs by `author`, `label`, `milestone`, and/or `assignee`. One also can sort the bugs by `newest`, `oldest`, `most commented`, `least comment`, `recently updated` or `least recently updated`.

The assignee is able to close issues via commit messages, for example, when (s)he enters `Fix #45` into a commit message, **issue #45** is closed once that commit is merged into the default branch. For details about closing issues via commit messages, see github help [here](https://help.github.com/articles/closing-issues-via-commit-messages).

More info about github issues, please see the [about issues](https://help.github.com/articles/about-issues).
