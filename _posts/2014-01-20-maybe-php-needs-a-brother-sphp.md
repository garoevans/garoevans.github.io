---
layout: post
title: Maybe PHP Needs a Brother, SPHP
category: code
---

So, I’ve been trying my best recently to keep up to date with “the community” and it’s often… how do I put this; NUTS! I’m subscribe to the [PHP](http://php.net/) internals mailing list, and though it is very interesting and I love knowing what’s going on, these guys can get rude. To me, it seems that PHP is at a cross roads and some REALLY big decisions are needing to be made. <!--more-->Take a look at some of these RFCs:

- [https://wiki.php.net/rfc/arrayof](https://wiki.php.net/rfc/arrayof)
- [https://wiki.php.net/rfc/typechecking](https://wiki.php.net/rfc/typechecking) – not an RFC, but relevant
- [https://wiki.php.net/rfc/fcallfcall](https://wiki.php.net/rfc/fcallfcall)
- [https://wiki.php.net/rfc/enum](https://wiki.php.net/rfc/enum)
- [https://wiki.php.net/rfc/propertygetsetsyntax-as-implemented](https://wiki.php.net/rfc/propertygetsetsyntax-as-implemented)
- [https://wiki.php.net/rfc/object_cast_to_types](https://wiki.php.net/rfc/object_cast_to_types)

That tells me that some people want PHP to get stricter, me included (but that’s not relevant). But there are always a mass of counter arguments. Some other people don’t want it to get stricter, they like PHP the way it is. I can imagine a lot of people would be happy if PHP was just faster, just concentrate on making it faster.

There was also a mention of replacing the [Zend Engine](http://www.zend.com/en/company/community/php/) with [HHVM](http://www.hhvm.com/blog/) for PHP6 in a [podcast](http://www.phpclasses.org/blog/post/225-Is-Facebook-HHVM-going-to-Replace-Zend-Engine-in-PHP-6--Lately-in-PHP-podcast-episode-43.html) earlier today:

> Cesar Rodas: If that ever happens to be true, if that is doable, that would take a very long time. Like I remember that when PHP 5, when it was released and when it was planned, plans for development and things like that, it took so long time that before that, I wasn’t even developing.

> So, if that ever happens to be true, that would take, I would guess what, five years or so. Which isn’t that bad, like having two implementations is not something bad at all.

> Manuel Lemos: Yeah.

Now that is an interesting thought.

## Welcome In The New

So; I’ve come up with a solution (idea)… SPHP, the ‘S’ stands for Strict. Why can’t this branch? There are enough developers in the world interested in both avenues that PHP seems to be trying to cater for. Internals is insanely busy, and there is no lack of RFCs to keep everything moving. This could be a great opportunity to take something like HHVM and start fresh. Not completely fresh of course, but just fresh enough to have some nice things:

{% highlight php %}
// I borrowed this form the Array of RFC
function heyLook(Foo[] $foos) {
{% endhighlight %}

or

{% highlight php %}
// I borrowed this from the same RFC
function heyLook(Dict<int, string>[] foo) {
{% endhighlight %}

It doesn’t matter, just bring the nice stuff, however it comes (sort of). Just look at some of these comments;

> Generics are more like “I would like a 100lb to 120lb bag of hammers
with handles made of wood grown in equatorial Africa between 1980 and
1985, not cut down during national holidays in Brazil and provided all
workers were paid the fair wage, while the heads must be made of steel
approved by German Council of Steel Manufacturers, and the assembly must
have been performed in a country that signed the convention about the
ethical treatment of animals”. You’d want arrays of arrays of foo, and
arrays that have keys of foo and values be arrays of tuples of bar and
baz, etc. etc.

> [http://news.php.net/php.internals/71349](http://news.php.net/php.internals/71349)

> Well, arrayof using generics-like syntax doesn’t give you entrance
type checking, but actual generics would. Or, to map it into current
PHP terms:

> private $spanners = [];
> public function __offsetset($key, $value) { if (!($value instanceof
> Spanner)) throw new Exception(“F-off”); $this->spanners[] = $value; }

> But this RFC isn’t about generics, it’s about arrayof typehinting and
ways to make that work for PHP. Your point about perf is absolutely
valid and one which I’d still like to hear addressed.

> [http://news.php.net/php.internals/71357](http://news.php.net/php.internals/71357)

> And I do not accept the argument of “if you don’t like it, you don’t
have to use it”. It is true, but only to a point. You can, in theory,
use C++ without templates. In practice, if you want to call yourself a
C++ programmer, you can not ignore them, not now. Language is also an
ecosystem, and I think Java-ifying PHP would take the ecosystem not in
the right direction. You, of course, may disagree and thing it is
exactly the right direction – there is always a moment where preferences
which are subjective come to play and in such a moment there’s nothing
to do but agree to disagree.

> [http://news.php.net/php.internals/71361](http://news.php.net/php.internals/71361)

That is a barrage of discussion that is still ongoing. There are now so many people concentrating on their wants and needs of this open and loosely typed language. One of the biggest asks is for it not to be a loosely typed language, I don’t want it to be a loosely typed language anymore, but is that fair? Maybe it is, maybe it isn’t but SPHP would solve that problem.

Would love to hear some opinions on this, hopefully thought provoking idea.
