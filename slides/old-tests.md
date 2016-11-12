#### A word of caution:

* An outdated set of tests can be worse than having no tests at all!
* Test the functionality, not the implementation! <!-- .element: class="fragment" -->
* Red - Green - Refactor <!-- .element: class="fragment" -->

Note:

Before you start thinking that testing will solve all of your problems, remember that the tests you write should reflect your codebase: if you're updating your app but not the tests, then your tests aren't doing you any good.

One way to make sure your tests are useful now *and* in the future is to test the functionality, not the implementation; if we're using that rage() function from earlier, our tests don't care *how* it gets the result, just that we get the result that we expect.

When testing, it's recommended that you follow the pattern of Red - Green - Refactor: write your test first, before you write the function. Because the function is empty, your test should fail, which is represented by red. Then, write the contents of your function until your test passes (green). From there – whether it's right away or months down the road, you have a test that will enable you to refactor knowing that the output of the function will remain the same.
