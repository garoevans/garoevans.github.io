---
layout: post
title: Testing Legacy PHP, Characterization Tests
category: testing
---

In the perfect world questions like "how do I test this?" are easily answered with one or multiple different test types like; [Unit Tests](http://en.wikipedia.org/wiki/Unit_testing) and [Integration Tests](http://en.wikipedia.org/wiki/Integration_testing). But in the big world of legacy code often these *don't fit*.
<!--more-->

Wouldn't it be lovely if everyone's first endeavour in a new project was to write some tests using [TDD](http://en.wikipedia.org/wiki/Test-driven_development), [BDD](http://en.wikipedia.org/wiki/Behavior-driven_development) or even [DDD](http://en.wikipedia.org/wiki/Domain-driven_design) to some respects. Maybe in two or three years time all the projects that are being started today will appear to be [Legacy Code](http://en.wikipedia.org/wiki/Legacy_code). I think that is fairly likely for some pieces of code.

## So how do we go about testing legacy code?

> My function is 3000 lines long, how many unit tests do I need to full coverage?

> Every other line of code has a global, how can I mock this?

> The server setup is so specific and state-full, the outcome always changes!

## Enter the [Characterization Tests](http://en.wikipedia.org/wiki/Characterization_test)!

> a means to describe (characterize) the actual behavior of an existing piece of software, and therefore protect existing behavior of legacy code against unintended changes

Characterization tests are very similar to [Regression Tests](http://en.wikipedia.org/wiki/Regression_testing) apart from one big main difference; characterization tests do not verify the correct behaviour of code, instead they verify that the output remains the same for a specific input after changes even if the original output was found to be wrong or unexpected.

I consider characterization tests a stepping stone, a safety net if you will. Once you have these tests in place you should be in a position where you can start to refactor your code, little bits at a time. After every change you make run the characterization tests, and add new tests as mentioned above.

Nobody likes legacy code, but everyone has written it. It may not be easy to test or ready for change but with a bit of sleeves rolled up work it can get there. The challenges a re-write bring over testing and refactoring are not often justified, so consider characterization tests next time you want to improve some legacy code.
