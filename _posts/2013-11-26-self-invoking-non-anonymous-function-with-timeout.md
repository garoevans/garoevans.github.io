---
layout: post
title: Self Invoking Non-Anonymous Function with Timeout
---

Useful anonymous function. Named for calling, but self invoking. Timeout added for example purposes.

{% highlight javascript %}
(function theFunction(aParam) {
  this._aParam = aParam || ++this._aParam;
  document.write(this._aParam + '<br />');
  setTimeout(theFunction, 1000);
})(10);
{% endhighlight %}
