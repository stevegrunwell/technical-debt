# Up to my Eyeballs in Technical Debt!

Every decision we make in our projects has the potential to increase or reduce technical debt. While the only way to completely eliminate the debt is to never write any code, there are steps that we as engineers, project managers, and project stakeholders can take to mitigate our risk.

This talk covers the concept of technical debt, its potential to devastate projects, and red flags that project teams can look for to reduce its impact before it spirals out of control.

## Outline

* What is technical debt?
    * Favoring easy/cheap over long-term maintainability
    * Not all technical debt is "bad"
        * Cost + risk analysis
        * Software is all about trade-offs
    * Everyday examples
        * Mainframes, outdated packages, etc
        * Spaghetti code
* How can we address technical debt?
    * Testing
        * Focus on E2E + integration tests ("snapshot" current behavior)
        * CI pipeline
    * Static code analysis
    * Documentation (especially as you go)
    * Dependency managers
        * Demonstrate `composer why-not php 8.3`
    * Feature flags
    * Rector
    * Componentize the application (when appropriate)
* Practical example - old app with outdated dependencies + PHP version, lots of legacy code, etc.
    * Lay out the approach
* What can we do to prevent technical debt?
    * Code review
    * Write tests as you introduce (or refactor) code
    * Require documentation
    * Embrace coding standards
    * Code organization
        * DDD?
    * Remove code when it's no longer necessary
    * Don't reinvent the wheel (NIH)
        * Loosely-coupled code, adapter pattern
    * Watch for red flags
        * @todo
        * Here be drags
        * Branching for special cases
