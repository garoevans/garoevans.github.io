---
layout: post
title: Damn You, DateTime
---

So, yesterday (Sunday) I had a phone call, it was from the on call dev. There was a problem with some code I’ve written. Since midnight on the 31st August these crons that run every hour were erroring. Something about September reporting as October… weird.

Now, I’ve run into date problems in PHP before. Have you ever tried iterating over a long period of time one [strtotime(‘+1 month’, $someTime);](http://php.net/manual/en/function.strtotime.php) at a time? Get it wrong and you’ll end up a month ahead, or even the same month and this is kind of what happened this weekend, even though I thought I was being good and using the [DateTime](http://php.net/manual/en/class.datetime.php) object:

{% highlight php %}
<?php
$dateTime = DateTime::createFromFormat('Ym', '201409');
{% endhighlight %}

Harmless right? Unfortunately not, on the 31st August running the above code is equivalent to doing the following:

{% highlight php %}
<?php
$dateTime = new DateTime('2014-09-01 00:00:00');
$dateTime->setDate($dateTime->format('Y'), $dateTime->format('m'), 31);
var_dump($dateTime);
//class DateTime#1 (3) {
//  public $date =>
//  string(26) "2014-10-01 00:00:00.000000"
//  public $timezone_type =>
//  int(3)
//  public $timezone =>
//  string(13) "Europe/London"
//}
{% endhighlight %}

By not explicitly setting a day in my first example PHP was defaulting to the current day (the 31st). So when working on a month of less than 31 days guess what? We end up on a different month. The fix was easy, but the code had been live for two months so had an affect everywhere!

**Damn You, DateTime!**
