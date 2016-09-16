---
layout: post
title: Testing Legacy PHP, Why?
category: testing
redirect_from:
- /2014/07/03/testing-legacy-php-why/
---

In my first post in this testing series; [Testing Legacy PHP: Characterization Tests](/2014/06/14/testing-legacy-php-characterization-tests/), I looked at how we might go about testing legacy PHP. Now I want to look at why we might go about testing legacy PHP.
<!--more-->

Strangely, the first time it occurred to me that I might need to test some legacy code I had was when I wanted to get rid of it. When I say some legacy code I mean hundreds of thousands of lines of code. This code, as [Paul Jones](https://twitter.com/pmjones) would put it in his book [Modernizing Legacy Applications In PHP](https://leanpub.com/mlaphp) is include oriented.

## An Important Note

It’s important to note that this realisation was based around my desire to refactor the legacy code base. In a perfect world I would stop all development on legacy systems and start an amazing re-write. If this was the case tests around legacy code may help describe the tasks undertaken by certain code but wouldn’t server any testing benefit  the same way as we can get when iteratively refactoring.

The rewrite vs refactor debate is not one I’m going to get into here, but you only need to take a look at the [google results](https://www.google.co.uk/search?q=rewrite%20vs%20refactor) to see how big this debate is;

- [http://www.targetprocess.com/blog/2009/11/refactoring-vs-rewrite.html](http://www.targetprocess.com/blog/2009/11/refactoring-vs-rewrite.html)
- [http://www.infoq.com/news/2009/11/refactor-rewrite](http://www.infoq.com/news/2009/11/refactor-rewrite)
- [http://www.klocwork.com/blog/code-refactoring/refactoring-vs-rewriting-why-it-matters/](http://www.klocwork.com/blog/code-refactoring/refactoring-vs-rewriting-why-it-matters/)
- [http://www.joelonsoftware.com/articles/fog0000000069.html](http://www.joelonsoftware.com/articles/fog0000000069.html)

## Why?

It became very obvious very quickly that to safely refactor large amounts of code over time I would need some way to validate that I hadn’t broken anything. Not breaking something might mean supporting that weird bug that we never wanted. If you were to fix some code that had a strange side effect, you may find that someone somewhere was relying on that side effect.

Fixing legacy code (or fixing code in general) is important. But, when refactoring it’s more important to (in my opinion), at the first step, maintain the existing functionality. What easier way to do this than to run an automated test suite each time you change some code.

1. Run tests
2. Refactor a little
3. Run tests
4. Refactor some more
5. Run tests

Each time those tests are run you can be confident that you haven’t broken (or fixed) anything.

I'm not saying that you should have 100% confidence in an automated test suite. Testers and QA are very important, but you should get the idea.

So, the short answer to the question Why should I test legacy code is; so that I can get rid of it.
