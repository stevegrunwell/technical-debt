<!-- .slide: class="title-slide" data-hide-footer -->
# Up to my Eyeballs in Technical Debt!

Steve Grunwell <!-- .element: class="byline" -->
[@stevegrunwell@phpc.social](https://phpc.social/@stevegrunwell)
[stevegrunwell.com/slides/technical-debt](https://stevegrunwell.com/slides/technical-debt)

---

## Understanding<br>Technical Debt

Note:

Before we can address technical debt, we should understand what we're talking about

----

### What is Technical Debt?

Challenges resulting from past decisions to favor <u>speed, simplicity, or cost</u> over<br><u>quality, maintainability, or robustness</u>

Note:

If you ask 10 different engineers to define technical debt, somehow you'll get 15 different answers.

For the sake of the talk today, we're going to define technical debt thusly.

Keep in mind, technical debt doesn't just mean "bad" or "legacy" code, either...

----

#### So you've settled on React&hellip;

<dl class="centered">
    <dt class="fragment" data-fragment-index="0">Pros</dt>
    <dd class="fragment" data-fragment-index="0">Tons of docs, libraries, etc.</dd>
    <dd class="fragment" data-fragment-index="1">Popular framework == large hiring pool</dd>
    <dt class="fragment" data-fragment-index="2">Cons</dt>
    <dd class="fragment" data-fragment-index="2">Need to keep up with the React ecosystem</dd>
    <dd class="fragment" data-fragment-index="3">Beholden to decisions of Meta</dd>
</dl>

Note:

Right now your front-end team might be deciding to move to React, and that comes with pros and cons

----

#### Technical Debt is a Part of Life

* <!-- .element: class="fragment" --> Mo' features, mo' problems
* <!-- .element: class="fragment" --> No code is 100% maintenance-free<br>(so pick your battles)

Note:

* In the grand scheme of things, you can't have software without incuring some debt
* The real challenge is getting the maximum benefit with minimal downside

----

#### Software is all about trade-offs

![Meme from Spaceballs (1987) where Dark Helmet is talking to Colonel Sanders in the desert, with the caption "He got the upside, I got the downside. See, there's two sides to every Schwartz"](resources/schwartz.png) <!-- .element: style="max-height: 60vh;" -->

Note:

Ultimately, software is all about trade-offs:

- do we do it fast, or do we do it right?
- is it worth the time/effort to replace this?
- is fixing this worth the potential risks?

----

### ECON Sidequest: Opportunity Cost

_What am I missing out on by doing this instead of something else?_ <!-- .element: class="fragment" -->

Note:

A short econ lesson: business types love talking about opportunity cost.

* New Oxford American Dictionary: the loss of potential gain from other alternatives when one alternative is chosen
* Is it worth more to address the technical debt or focus on (for example) new features that could drive revenue?
* Imagine you're a freelancer, making $100/hr. It takes you one hour to mow your lawn. Neighbor kid offers to mow it for $50.
    * On paper, if you do client work in that hour, you come out $50 ahead (assuming you have client work lined up)
    * In reality, maybe you enjoy mowing the lawn (or at least the fresh air) or you've already done as much freelance work as you can bear
* Keep this in mind as you pitch projects for cleaning up technical debt to your managers!

----

### Technical Debt in the Real World

_Success + Tech Debt are not mutually exclusive!_

* <!-- .element: class="fragment" --> Banking systems still running COBOL
* <!-- .element: class="fragment" --> WordPress: ~43% of web, "compatible with exceptions" for PHP 8.x
* <!-- .element: class="fragment" --> Services on outdated servers/dependencies
* <!-- .element: class="fragment" --> "Legacy" applications

Note:

Technical debt is everywhere:

* Many financial institutions still run on software written decades ago in COBOL, because the cost + risk of replacing these systems is so high
    - Cheaper to pay handsome saleries to mainframe devs
* WordPress, by far the most popular PHP-based CMS, powers roughly 43% of the web (according to W3Techs)
    - Only "beta" support for PHP 8.2 + 8.3, is "compatible with exceptions" for PHP 8.0 + 8.1
    - Part of the market strategy is making it easy to run WordPress _anywhere_, and cheap hosts aren't usually current on PHP
* Services you use every day, perhaps even to power your business, are often running outdated server software, dependencies, etc.
    - Opportunity cost: what value could those engineers be driving instead of constantly updating?
* So-called "legacy" applications that still bring in millions in revenue
    - Craigslist made $660M in revenue in 2021!

----

<!-- .slide: data-background-image="resources/lobster-hot-tub.png" data-background-size="cover" data-background-opacity="0.7" -->

### Technical Debt is a Slow Boil
<!-- .element: style="padding-bottom: 4em;"-->

Note:

If technical debt is a part of life and isn't inherently bad, why are we talking about it?

The problem is when the tech debt piles up and inhibits your team.

----

### Signs You May Be In Debt

1. <!-- .element: class="fragment" --> Even small changes are highly-involved
2. <!-- .element: class="fragment" --> Frequent incidents & outages
3. <!-- .element: class="fragment" --> Increased attrition
4. <!-- .element: class="fragment" --> Maintainers stop providing patches
5. <!-- .element: class="fragment" --> Archive.org becomes your doc site

Note:

1. Even small changes like adding a button or updating copy takes hours (or more)
    * New features are nearly-impossible (or end up being written as entirely-separate services)
2. You're constantly fighting fires due to things breaking
3. Your top engineers are looking for new jobs
    * Even your IDE wants to quit
4. You have more EOL dependencies than supported ones
5. The docs for your library versions are so old you have to visit the Internet Archive to reach them

---

## Refactoring 101

Note:

* Will talk about specific manifestations of technical debt in a moment
* First, there are a few principles you should know and apply liberally as you refactor:

----

### Start with Tests

* <!-- .element: class="fragment" --> Safety net for today and tomorrow
* <!-- .element: class="fragment" --> Focus on the big picture
* <!-- .element: class="fragment" --> Continuous Integration FTW!

Note:

* Before you change anything, you should make sure that you have good integration and/or e2e tests around your application
    * Critical flows (signup, login, checkout, etc.) and the areas you're working on
    * These act as guardrails or a safety net, ensuring that you don't accidentally break anything as you refactor
    * Tests will then live on, aiding in future refactors
* Focus more on integration + e2e tests; individual functions/methods may change considerably, so unit tests are less helpful here
    * Write tests as you write new code during the refactor (including unit tests!)
* These tests should be run as part of your CI pipeline on every push
    * Don't have a CI pipeline? No time like the present!

----

### Static Code Analysis

* <!-- .element: class="fragment" --> Inspect your code without running it
    * [PHPStan](https://phpstan.org), [Phan](https://github.com/phan/phan), [Psalm](https://psalm.dev/)
* <!-- .element: class="fragment" --> Find type + logical errors
* <!-- .element: class="fragment" --> Tune it to avoid a firehose!

Note:

* Static code analysis is a method of analyzing your code without having to run it
* Great at catching logical errors, type issues, etc.
    * Many can also help you identify dead code paths
* Turning it on without tuning will hurt your feelings

----

#### Tuning Static Code Analysis

1. <!-- .element: class="fragment" --> Unknown classes/functions/methods, wrong number of args, etc.
2. <!-- .element: class="fragment" --> Potentially undefined vars, invalid PHPDocs
3. <!-- .element: class="fragment" --> Unreachable code, conditionals that will always pass/fail
4. <!-- .element: class="fragment" --> Strict types, etc.

Note:

* Most static code analysis tools let you dial in the things you care about
* If you're just introducing static code analysis, start with the lowest level and, as you address (or suppress) issues, you can turn this up

----

### Backfill Documentation

![George McFly, writing in his notepad while talking to Marty, saying "I'm writing this down, this is good stuff."](resources/writing-this-down.gif)

Note:

* As you begin digging into the old, crusty code don't be afraid to take notes on your findings!
    * Writing inline docs can help you keep track of your findings both today and tomorrow
    * Remember to capture not only the how, but the _why_!
* Documentation-only PRs are not only very low-risk, but also help you and other members of your team follow along.
* Adding docblocks also helps static code analysis tools better analyze your code

----

### The Power of Package Managers

* <!-- .element: class="fragment" --> Manage direct + intermediary dependencies
* <!-- .element: class="fragment" --> Negotiates version constraints, conflicts
* <!-- .element: class="fragment" --> Easily see what's out of date

Note:

Whenever possible, leverage the appropriate package manager for your language's ecosystem. In PHP that's Composer, and we're so lucky to have it!

* Allow you to install and update dependencies, including any intermediary dependencies
* Negotiates version constraints and conflicts with other packages
* Easily see what packages have updates available

----

#### Composer in Action

```sh [1|2]
$ composer why-not php 8.3
some-vendor/some-old package 1.2.3 requires php (^7.0)
```
<!-- .element: class="hide-line-numbers" -->

```sh
$ composer require "php:8.3" --dry-run
```
<!-- .element: class="fragment" -->

Note:

* Composer can tell us which of our dependencies don't claim to support PHP 8.3
* For even further details, you can run `composer require php:8.3` with the `--dry-run` flag and see what conflicts Composer has flagged

----

### Step Debugging

* <!-- .element: class="fragment" --> Pause your code at certain points
* <!-- .element: class="fragment" --> Inspect values, dig into function calls
* <!-- .element: class="fragment" --> Worth the effort to configure!

Note:

If you really want to level up your refactoring game, learn to use a step debugger like Xdebug

* Allows you to set breakpoints and freeze the execution when you reach it
* From there, you can inspect the values of different variables, see the current stacktrace, and then progress through your code, one step at a time
* Can be challenging to get set up, but way more powerful than die debugging

---

## Common Manifestations<br>of Technical Debt<br><small>(and how to fix them)</small>

Note:

With those fundamentals out of the way, let's look at some common manifestations of technical debt and how we might go about addressing them:

----

### Committed libraries

* <!-- .element: class="fragment" --> Replace with copy managed by Composer
* <!-- .element: class="fragment" --> Consider modern replacements

Note:

Not uncommon to come across apps with `lib` directories or similar, full of third-party code **not** managed by a tool like Composer
    * Congratulations, you've effectively adopted that dependency!
    * Updates, conflicts, patches, and bugs are now your responsibility

* When possible, you want to use an appropriate package manager (e.g. Composer)
* If the library predates Composer, you may want to start looking for more modern solutions
    * You can ease this transition with the Adapter Pattern

----

#### Adapter Pattern

* <!-- .element: class="fragment" --> Define an interface, then write library-specific implementations
* <!-- .element: class="fragment" --> Makes it easier to swap out underlying libraries with minimal interruption
* <!-- .element: class="fragment" --> Easier to test individual implementations

Note:

* Design pattern where you define a common interface, then write lightweight wrappers that implement those interfaces using different underlying libraries
    * Decouples your app code from the underlying library: application code only uses the methods on the interface (often injected through a DI container or factory method)
    * Your adapters are responsible for implementing the interface and interacting with the underlying libraries
    * For the Laravel devs, this is like binding implementations to interfaces in the service container
* Once the app is only focused on the interface, which adapter gets used is a matter of configuration
    * Example: maybe you were sending email with Postmark, and you switch it to Mandrill. As long as they're both configured, nothing about the implementation should need to change (the app just knows it's sending through a `MailerInterface`)
* Makes it easier to test individual implementations

----

<!-- .slide: class="has-background-image" data-background="resources/spaghetti.jpg" data-background-size="cover" data-background-opacity="0.3" -->

### Spaghetti Code

* <!-- .element: class="fragment" --> Don't forget to bring a test!
* <!-- .element: class="fragment" --> Step debuggers will be a huge help!
* <!-- .element: class="fragment" --> Extract what you can

Note:

Code that's difficult to navigate through, like a big plate of spaghetti
    * Often the result of poorly thought-out or ever-changing business requirements
    * Causes developers to waste a lot of time sorting things out
    * Difficult to onboard into
    * Breeding ground for tough-to-track-down bugs

* As usual, start with tests
    * The harder the code is to follow, the more important it is that you have broad, e2e tests
* A step debugger is worth its weight in gold when navigating a noodly codebase
* As you can, find ways to extract pieces into standalone classes or methods that you can more-easily test

----

<!-- .slide: data-background-image="resources/trogdor.png" data-background-repeat="no-repeat" data-background-size="contain" data-background-position="10% center" data-background-opacity="0.3" -->

### Black Boxes

* <!-- .element: class="fragment" --> Box of spaghetti?
* <!-- .element: class="fragment" --> Start broad, then go narrow

Note:

If you find comments like "here be dragons", "I don't know why this works, it just does", and/or "Dear, sweet Jeebus, be careful!", you may have a black box
    * where data goes in and comes out, but nobody's sure _how_ it works

* In many ways, approach black boxes as you would spaghetti code: tests, step debugging, and writing docs as you go
* Try to focus first on the big picture (what it's trying to do), then narrow in on the "how"
* Try not to get burninated

----

### @todo comments

```php
/**
 * @todo WTF is going on here?! 😱
 */
```

Note:

* `@todo` comments aren't inheriently-evil, but can be good indicator of incomplete/buggy code
* Try to be as descriptive as possible; can this be linked to a Jira ticket or something?
* Be sure to read existing comments: sometimes you'll find the "todo" is already "todone"

----

### Useless Tests

* <!-- .element: class="fragment" --> Describe the behavior, not the implementation
* <!-- .element: class="fragment" --> Too many mocks (including the <abbr title="System Under Test">SUT</abbr>!)
* <!-- .element: class="fragment" --> Asserting that <u>any</u> exception is thrown
* <!-- .element: class="fragment" --> Loose comparisons (e.g. false == null)

Note:

Brittle, tightly-coupled tests can sometimes be worse than no tests at all!

* When people are just learning how to test (or worse, are told "you must have tests for everything" without guidance), they often fall into the trap of testing the implementation, not the intended behavior
    * Basically just writing the code twice, which defeats the purpose
* Tests that mostly serve as tests for the mocking library
* Overly-broad expectations and assertions
    * I expect a 500 error when my app can't talk to that API, so lemme just pass the test if I get _any_ exception (even a type error due to my own bug)
    * `assertEquals()` instead of `assertSame()` where `0` and `false` are two possible returns with *very* different meanings

----

### Branching for special cases
<!-- .element: class="screen-reader-text" -->

![Four panel comic from Commit Strip. In the first panel, the developer tells the Product Manager "No. Just No." as the PM pleads "Come on...only one small exception". Panel two continues, with the developer stating "It's a self-service SaaS, we can't handle individual requests" while the PM reasons "Come on...just a tiny IF. A ridiculously tiny IF...". In panel three, the PM continues "It's one of our biggest customers...I'll owe you one!". The developer hesitates, saying "I shouldn't...". In panel four, set later, the Database Engineer asks the dev "Where you do you manage clients' special requests", to which the dev responds defeatedly "model/clients.php. There's a switch with 145 cases, just add yours".](resources/commitstrip-exceptions.jpg) <!-- .element: style="max-height: 80vh;"-->

Note:

* Codebase is full of one-off "well, this particular customer requires this extra thing be enabled" conditionals
    * Far more difficult to keep everything straight
    * These "quick if statements" are rarely given appropriate tests, meaning when something breaks it's often for the high-value customers
    * If customers churn, these may never get cleaned up
* Ideally, these should be seen as attributes or flags you can enable on a per-user basis
    * Ensure that you treat it as you would any other feature (including tests!)

----

### Dead Code

!["Bring out yer dead" bit from Monty Python and the Holy Grail](resources/bring-out-yer-dead.gif)

Note:

* Sometimes it can be really hard to say goodbye to code that we wrote, even if it's no longer necessary
    * Version 2 is live, but nobody removed v1 after launch
    * Code that's outlived its usefulness: One-time migration scripts, COVID-19 promos, etc.
* Thanks to version control, dead code's never truly gone (but it doesn't need to be cluttering up your repo)
* Leverage static code analysis, IDE capabilities, logging, and/or observability tools to see if a block of code is truly dead

---

## Technical Debt<br>Repayment Plan

Note:

* You just joined a new team with a large, legacy codebase serving millions of users
* Can't just throw everything away and start over, so where do you start?

----

### Define scope

1. <!-- .element: class="fragment" -->What are we hoping to solve?
2. <!-- .element: class="fragment" -->Why do we want to do this?
3. <!-- .element: class="fragment" -->What's our ideal state?
4. <!-- .element: class="fragment" -->How will we address this?
5. <!-- .element: class="fragment" -->How do we measure success?

Note:

Jumping right in without a strategy is likely how the app ended up with all this debt, so let's be smarter as we fix things

1. What is it that we're trying to solve? Replace an old library? Untangle a complex web?
2. Why are you tackling this? Performance? Is it a security risk? A pain point for users or your team?
3. What's the ideal state? Where do you hope to be after this?
4. How do you get from A to B? What needs to happen?
5. How will you measure success?
    * Very important when trying to sell management on the project

----

### Example: Upgrade to PHP 8

Note:

Here's an example that will probably resonate: upgrading your app so it runs on PHP 8.

----

#### Why do we want to do this?

* <!-- .element: class="fragment" --> PHP 8 is more powerful and faster
* <!-- .element: class="fragment" --> PHP 7.x is EOL (security risk)
* <!-- .element: class="fragment" --> Packages dropping 7.x support

Note:

So we want to upgrade, but why?

* PHP 8 has a lot of powerful new features and can be more performant
* PHP 7.x is EOL, so we won't get new security patches
* Packages we rely on are dropping PHP 7.x support, so we won't get new features or patches

----

#### What's our ideal state?

* <!-- .element: class="fragment" --> All app servers are running PHP 8.3
* <!-- .element: class="fragment" --> Composer dependencies are updated<br>to their latest versions
* <!-- .element: class="fragment" --> No impact to application behavior

Note:

Just because we're going to PHP 8 doesn't mean we have to use all of its features on day one.

Notice we didn't mention anything about, for example, ripping out that old enum library and using PHP's native enums. One thing at a time!

----

#### How will we address this?

1. <!-- .element: class="fragment" --> Install/upgrade static code analysis tools
2. <!-- .element: class="fragment" --> Resolve issues caught by static code analysis, test suite(s)
3. <!-- .element: class="fragment" --> Pre-prod testing w/ PHP 8.3
4. <!-- .element: class="fragment" --> Slow-roll 8.3 image across hosts
5. <!-- .element: class="fragment" --> Clean up PHP 7.x leftovers

Note:

Now we know what we're hoping to accomplish, so now we need to determine how we get there

1. If we already have a static code analysis tool, make sure it's current.
    * If not, now would be a good time to install one
2. Tell the tool that we're targeting PHP 8 and let it tell us where we might have issues. Then get the tests running on PHP 8
    * Good test suites will cover large portions of the app
    * No tests? This would be a very good time to start!
3. Next, we want to manually test things
    * If you have a QA team, they'll be vital here
    * Involve SMEs to ensure things continue to work as expected
4. Finally, start rolling out PHP 8 on production
    * If possible, don't upgrade all servers at once
5. Once you're on PHP 8, clean up any PHP 7-specific paths you may have added

----

#### How do we measure success?

1. <!-- .element: class="fragment" --> All app servers are running PHP 8.3
2. <!-- .element: class="fragment" --> All Composer dependencies are up-to-date
3. <!-- .element: class="fragment" --> No unscheduled downtime or production errors related to upgrade

Note:

* You may notice, a lot of these metrics match our described, ideal state
* Gives your managers clear numbers, e.g.:
    * All 50 servers are now running the latest version of PHP
    * All 20 direct and 80 intermediate Composer dependencies are up to date
    * 0 minutes of unscheduled maintenance
    * 0 incidents
* Having these numbers makes it very easy for them to say "yes" the next time you propose a refactor!

---

## Preventing Technical Debt

Note:

Now that we've covered common forms of technical debt and how we might address them, let's talk about how we can catch ourselves from getting back there again

----

### Recognize Trade-offs

How likely is it that taking<br>the easy way now will bite us later?

Note:

* As mentioned earlier, software is all about trade-offs
* Remember: not all code is meant to last forever; be intentional about new debt, and know when you can and cannot compromise

----

### Code review

![Lisa Simpson, desperate for attention from Marge (or anyone, really), hopping up and down pleading "Grade me! Look at me! Evaluate and rank me!"](resources/lisa-grade-me.gif)

Note:

* If it isn't already, make code review a required part of your team's development.
* Not only does it help catch bugs before they reach production, but it ensures you're not the only one who understands how the app works.
* Code reviews should include documentation: if a PR changes the way something works it must also include the relevant documentation updates!

----

### Embrace Coding Standards

A good codebase reads like it was written by a team that was on the same page.

Note:

* Coding standards help keep the codebase organized and readable
* Not just spaces v. tabs, but procedural v. OOP, namespaces, organization, etc.
* Enforce standards with tools like PHP_CodeSniffer and PHP Coding Standards Fixer

----

#### Write code that's easy to follow

`1337 C0D3 15 4 1053R5`

Note:

* One of the really fun things about programming is challenging ourselves to come up with clever new ways to do things
    * Keeps the 9-5 from totally crushing our souls, but boring can be good!
* Part of being an effective engineer on a team is not being flashy, but being consistent
    * Clean, well-documented, and easy to follow code are the mark of a truly-talented developer
* Strict types, composition over inheritance, and avoiding magic

----

### Write tests as you go

* <!-- .element: class="fragment" --> Test-Driven Development
* <!-- .element: class="fragment" --> Regression tests to fix bugs

Note:

Touched on this earlier, but it's not one of my talks without me harping on testing!

* If you're able, embrace TDD
    * Write tests first to describe the feature, then write the code necessary to make the tests pass
    * Encourages more thoughtful design patterns
    * Built-in defense against unintended changes
* When fixing bugs, start the same way:
    * Write tests to reproduce the bugs (tests should fail)
    * Fix the bug (tests should pass)
    * The test then protects against future regressions

----

### Plan for updates

![Geordi La Forge meme where he rejects "wait too long, apply tons of updates at once" in favor of "update incrementally on a regular cadence"](resources/geordi.jpg)

Note:

Remember that technical debt is a slow boil, so make sure you're giving yourself time for updates.

Maybe it's a day at the end of your sprint or some time at the end of the month, but set an upgrade cadence and stick to it

----

### Removing the Clutter

* <!-- .element: class="fragment" --> Throw away what's not needed
* <!-- .element: class="fragment" --> Write new code so it can be removed easily

Note:

* Some of the best commits you can make are those that simply remove unneeded code.
* If something's no longer needed, get rid of it!
    * Thanks to source control, you can always reference it later if needed
* Write new code in ways that it can be removed when no longer needed
    * Namespaces, separate Composer packages, etc.

----

<!-- .slide: data-background-image="resources/spiderman-pointing.jpg" data-background-size="cover" data-background-opacity="0.4" -->

### No Two Ways About It!

Note:

* On a larger codebase, it's not uncommon to have multiple libraries that do the same thing.
    * Maybe two teams installed Libraries A and B independently, but now there are two ways to do the same thing
    * Worse yet, another engineer comes in and implements Library C, making the count three!
* Have some sort of central location (wiki, spreadsheet, etc.) that outlines which libraries are available, where they're being used, and where to go to get further details.
* Another place where the adapter pattern can help: if people aren't interacting with the libraries directly (just your interface), it matters a lot less

----

### Resist Not Invented Here (NIH)

![Homer Simpson, lounging on the couch with a cigar, laughing that "everyone is stupid but me", then drifiting off and starting a fire as the cigar falls out of his mouth](resources/homer-stupid.gif)

Note:

* At one point or another, many organizations may feel they have to write every part of their stack
* Do you really want to maintain your own authentication library? Or logging system?
* Where possible, leverage the tools provided by your framework or other third-party libraries
    - Dramatically reduces maintenance burden, benefit from existing art
    - Adapter pattern (discussed earlier) enables you to more-easily change implementations later, if needed

----

<!-- .slide: data-background-image="resources/waterfall.jpg" data-background-size="cover" data-background-opacity="0.3" -->

### Don't Go Chasing Waterfalls

_Please stick to the languages <br>& practices you're used to_

Note:

* It can be a lot of fun to work with new technologies, but having a dozen apps in as many languages will make maintenance a huge PITA
    * Most teams are good with a small set of technologies
* Remember: every time someone "disrupts the status quo" you're stuck maintaining it!
* If you want to explore new technologies, see if there's a way you can pilot the tech in a small project that could be rewritten or thrown away if necessary

----

### Web standards are always in style

![Brent Rambo, a kid on a very 1990s-era PC, clicking around before giving a thumbs up and nodding at the camera](resources/brent-rambo.gif)

Note:

* If in doubt, lean on functionality within the programming language. This is generally less prone to major breaking changes than the flavor of the week library or framework
* If nothing else, plenty of great, well-tested libraries out there that are designed to do one thing exceedingly well.

---

## So, what have we learned?

* <!-- .element: class="fragment" --> Technical debt is a part of life
* <!-- .element: class="fragment" --> Watch for red flags
* <!-- .element: class="fragment" --> Identify, plan, execute
* <!-- .element: class="fragment" --> Test early, test often
* <!-- .element: class="fragment" --> Be empowered—not hindered—by open-source

Note:

* Technical debt is a part of life, but by making good decisions we can minimize its impact.
    * It's only a problem if it's costing you time, money, and/or sanity
* Ever vigilent, always watching for red flags we discussed: spaghetti code, committed libraries, todo comments, dragon lairs, bad+brittle tests, branching for special cases, dead code
* Identify *what* you want to solve, then make a plan
* A solid test suite is worth its weight in gold
    * E2E and integration tests at the start help ensure your app doesn't break as you refactor
    * Write regression tests as you fix things
* Take advantage of well-tested, documented, and maintained open source projects, but do so in a way that you're not tightly coupled to them
    * Manage them using dependency managers
    * Have a reason for everything you install

----

### What's the best way to eat an ElePHPant?

![The PHP Elephant logo, a profile of a purple, cartoon elephant with the letters "php" along its body](resources/php-elephant.png)<!-- .element: style="max-height: 6em;" -->

You don't, you monster! <!-- .element: class="fragment" -->

Note:

A little riddle for you

---

## Thank You!

Steve Grunwell<br>
<span style="font-size: .75em;">Staff Software Engineer, Mailchimp</span>

[stevegrunwell.com/slides/technical-debt](https://stevegrunwell.com/slides/technical-debt)<!-- .element: class="slides-link" -->
