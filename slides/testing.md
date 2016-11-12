### Testing

* <!-- .element: class="fragment" --> Even _moderate_ testing is helpful
* Helps prevent regressions <!-- .element: class="fragment" -->
* Refactor with confidence <!-- .element: class="fragment" -->

Note:

People seem to get up in arms about testing, but the simple truth is that it can seriously help you maintain a codebase.

Even a moderate level of testing can be worth its weight in gold when you try to change something.

Imagine if every time you fixed a bug, you also wrote a test to ensure that bug is indeed fixed. If something changes later, you'll still have this test in place to ensure that bug doesn't re-surface.

Having tests also ensures that when you go to refactor your codebase you have an easy way to see if you introduced new bugs along the way.
