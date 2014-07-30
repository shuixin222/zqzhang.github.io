# Crosswalk Weekly 2

Crosswalk Weekly is a summary of activity on the Crosswalk Community from QA's
perspective, to get inputs to improve [crosswalk-test-suite]
(https://github.com/crosswalk-project/crosswalk-test-suite) test coverage and
approach.

## Pull Requests from outside of Web QA Team

Gladly, there are several pull requests contributed from outside of Web QA Team,
for example, from `open.eurogiciel.org`, `platogo.com`, `samsung.com`.

Great the Crosswalk Community! Great the open source!

1. **https://github.com/crosswalk-project/crosswalk-test-suite/pull/420**
   To my observe, this is the first pull request from outside. @clecou from
   open.eurogiciel.org implements Tizen IVI Bluetooth at
   https://crosswalk-project.org/jira/browse/XWALK-1065. There is a test failure
   reported at https://crosswalk-project.org/jira/browse/XWALK-2090. This pull
   request is trying to update the test case to adapt for Crosswalk implemention.
   It is accepted after Samsung evaluates the change on Tizen 2.x targets.
2. **https://github.com/crosswalk-project/crosswalk-test-suite/pull/515**
   @sirflo from platogo.com contributes his WebAudio crashing sample to reproduce
   bug report https://crosswalk-project.org/jira/browse/XWALK-1993.
   This sample demonstrates that Chrome on Android currently has a problem with
   WebAudio. When repeatedly navigating to webpages with audio playback using
   WebAudio the browser tab crashes. In his Crosswalk application the whole app
   crashes.  This sample is wrapped as a test case at
   `misc/xwalk-system-tests/tests/WebAudio`.
3. **https://github.com/crosswalk-project/crosswalk-test-suite/pull/544**
   @yejingfu from Intel Crosswalk dev team fixes a Bookmark test case bug at
   https://crosswalk-project.org/jira/browse/XWALK-2073. The current logic of
   remove() is wrong which is trying to remove a new bookmark object. Instead,
   remove() should remove an existing bookmark which must be already added.
4. **https://github.com/crosswalk-project/crosswalk-test-suite/pull/552**
   @tiwanek from samsung.com fixes failing multicolumn TCT tests because these
   tests are incompatible with the multicolumn w3c spec:
   http://www.w3.org/TR/css3-multicol/. He also analyzes the test issue at
   https://crosswalk-project.org/jira/browse/XWALK-2202 as:
   * Tests are using invalid 'columnRuleWidth' css attrtibute instead of
   'column-rule-width'.
   * Tests make assumption about 'column-width' css attribute value.
5. **https://github.com/crosswalk-project/crosswalk-test-suite/pull/553**
   @jizydorczyk from samsung.com is trying to fix 2 ApplicationControl tests
   to reflect Blink implementation rather than WebKit implementation of the
   default onerror callback (null in WebKit but undefined in Blink) in
   `tizen.application.launchAppControl()`. I accept it with comment added into
   the changed files to show this is fixing for Crosswalk only (not TCT).
   Corresponding bug is https://crosswalk-project.org/jira/browse/XWALK-2194
6. **https://github.com/crosswalk-project/crosswalk-test-suite/pull/554**
   @jizydorczyk is trying to change Indexed DB attribute name from `multientry`
   to `multiEntry` to reflect latest W3C standard:
   http://www.w3.org/TR/IndexedDB/#index at bug report:
   https://crosswalk-project.org/jira/browse/XWALK-2203
   I would like to accept this pull request after 2 related test files update,
   because they also use this attribute:
   * `tct-indexeddb-w3c-tests/indexeddb/IDBIndex_name_exist.html`
   * `tct-indexeddb-w3c-tests/indexeddb/IDBIndex_objectStore_exists.html`
7. **https://github.com/crosswalk-project/crosswalk-test-suite/pull/555**
   @jizydorczyk wants to replace `location.hostname` with `127.0.0.1` in
   WebSocket tests. If @JianfengXu or @haoxli verifies this change as PASS,
   I will accept it.
8. **https://github.com/crosswalk-project/crosswalk-test-suite/pull/556**
   @tiwanek says in this pull request that "tests are incompatible with the
   XMLHTTPRequest spec: http://www.w3.org/TR/XMLHttpRequest/
   In current implementation send() may be called after abort(); this causes
   tests to fail". I suggest him submit the changes to W3C testing community
   directly while ask @JianfengXu or @haoxli to verify it. Yes, I will accept
   the pull request if it passes our verification.

