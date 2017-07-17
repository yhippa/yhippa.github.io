---
layout: post
title:  "Weekend Coder: Angular Tour of Heroes"
date:   2017-07-16 23:35:00
categories: blog
comments: true
---

This weekend I wanted to change things up and finally dig down into the newest version of Angular for about the 4th or 5th time.  I remember having much more trouble with this the first time I did it.  Also I didn’t understand what stuff did all that much.  Similar to the phonecat tutorial for Angular 1.x there's the new [Tour of Heroes](https://angular.io/tutorial) tutorial for the new Angular.

Learned there’s a UI pattern called [master/detail](https://en.wikipedia.org/wiki/Master%E2%80%93detail_interface).  I’ve seen this before but didn’t know what it’s called.  Cool.  Now I can sound fancy when I go to Meetups.

I liked going through the tutorial and making the updates without seeing the answers to see if I had good instinct on where to put code.  This is good and bad because the documentation has to be clear.  I feel I get more out of it when I struggle through this though.

So far the new Angular reminds me of good old [Knockout.js](http://knockoutjs.com/) in terms of ease of understanding and moving around an application.

I love using [Visual Studio Code](https://code.visualstudio.com/) and the [TypeScript](https://www.typescriptlang.org/) integration.  Static validation is the best!  In fact I thought it was very necessary to add this because you knew while you were building code whether or not you were going to have errors down the road.  You don't find out object mismatches with vanilla JS until you start poking around the app.

In the services module in one part of the tutorial I noticed that import { HEROES } wasn’t working because I forgot to export it.  That makes sense.  There is intrinsic symmetry in importing and exporting things.

The unintended errors in my code and in the examples gave me a chance to do do debugging.  Neat that the exceptions in the console were fairly meaningful and were a bit more helpful in isolating issues.

The Services section was a bit scary because you had to figure out where to put a lot of the code.  But what’s nice is that I figured it out in a way due to how imports and interfaces work in Java.  When your class implements an exported class then it has to implement methods of that class.  Very familiar to me.

The part about [Promises](https://angular.io/tutorial/toh-pt4#act-on-the-promise) was new to me but how to use them smelled very much like [Java lambda expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html).  Also familiar.

When I got to the part about simulating a [slow service](https://angular.io/tutorial/toh-pt4#appendix-take-it-slow) I tried using autocomplete for the new method using control-space and it worked just like it did in my other Java IDE’s.  Cool!

One thing I couldn’t figure out was when [refactoring](https://angular.io/tutorial/toh-pt5#create-appcomponent) for routing how to get the heroes to inject into the Heroes component even though we promoted the heroes service to be at the App level.  The issue was that I mistakenly removed the HeroService import from the top of the file.  I guess through this process by having the HeroesService as a provider it’s automatically injectable by the components in this class?

I’m not an RxJs expert but I like that when you re-request a subscribe-able object and you say re-request it with a different parameter or any arbitrary call it keeps track of the subscriptions and cancels them.

The Location class is interesting.  Very interesting.  You used to have to manage state in static templates with pretty messy logic on the back-end.  Can it be this easy in Angular world?

Man, that Routing section was complicated and long.  I got through it but I lost concentration at the end.  I'm surprised I made it through that whole section after doing a lot of refactoring.

By the time I finished it was late Sunday night and I got a tiny bit through the [HTTP section](https://angular.io/tutorial/toh-pt6).  Hopefully I have some time soon to dig in to that and probably redo the Routing tutorial.  I feel like that's a huge complex part of what Angular does and I need to understand it.  Luckily I think the tutorial is well-written and after going through it and doing the refactoring a few times I'll pick it up.

Overall my impressions are positive about the new Angular.  I finally get the jokes about why it looks so much like Java.  The jokes end I'm sure when you're trying to build a single-page application and dealing with developers of different skills hacking on the codebase.  Type safety must be a huge boon in those scenarios.

