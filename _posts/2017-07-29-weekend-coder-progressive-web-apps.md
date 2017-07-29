---
layout: post
title:  "Weekend Coder: Progressive Web Apps"
date:   2017-07-29 13:02:00
categories: blog
comments: true
---

This is completely random but I read a [TechCrunch article about how Windows Phone could make a comeback](https://techcrunch.com/2017/07/28/microsofts-slow-creep-back-into-mobile/) in part because of Progressive Web Apps.  I'll be honest: this has been a desire of mine since Apple released the very first iPhone "apps" which were intended to be apps that worked with the phone APIs.  Check out this video from 2007 when the iPhone was first announced that describes this: https://www.youtube.com/watch?v=v1BL8doi6wY#.

What is a Progressive Web App?

In the future if this catches on I could try out different types of phones that have different capabilities and still get access to the important apps I need as long as I have an internet connection.  The best part of these Progressive Web Apps is that you can cache the app code and still have it work offline.

I found this tutorial by Google: [Your First Progressive Web App](https://developers.google.com/web/fundamentals/getting-started/codelabs/your-first-pwapp/).  The coolest part about this tutorial is I was able to do everything on my aging Acer C720 Chromebook.  Possibly one of the cooler things is that there's now an app that lets you run a web server on your Chromebook: [web Server for Chrome](https://chrome.google.com/webstore/detail/web-server-for-chrome/ofhbbkphhbklhfoeikjpcbhemlocgigb?hl=en).  If someone can come up with a Node runtime in the Chromebook without me having to get into Developer Mode and chroot-ing I'll be a very happy man.  You do need to edit some files and for that I use [Caret](https://chrome.google.com/webstore/detail/caret/fljalecfjciodhpcledpamjachpmelml?hl=en).

How do you get the app to work offline?  By caching the app contents in the browser.  This is pretty impressive.  I'm not quite sure where the code is physically saved nor what the persistence guarantees are from session-to-session but the API is easy to grok.  There is some application code you need to write but the heavy lifting is done in a separate file with code specific to service workers.  I have rarely used this and only in learning exercises but it seems like it's one of those features that are really important that we'll see a lot of sites use several years from now.  Google Chrome has excellent support to monitor and debug servicer workers to in Dev Tools.

One part that was interesting was that instead of using a library to make a web service request the tutorial code used good old XMLHttpRequest().  I've noticed a trend of shunning libraries for lower-level function calls like this.  Honestly the code is still readable and you lose the overhead of loading something like jQuery.

Then to counter that statement I noticed a ton of edge cases and lots of gotchas that you have to look out for.  A lot of statements like "don't use this in production" were peppered throughout the tutorial.  This makes me think that some kind of framework will eventually exist that handles all of this.

Much like caching in Java Enterprise apps I think a lot of time will be spent determing what the boundaries of that are for apps used on a mobile, tablet, desktop, or any arbitrary device.  For weather stale data is mostly useless.  Same for stock quotes.  Things like user contact information could probably be stored locally and make a call home on a longer polling basis.

There's a block of code where you have two strategies of dealing with offline data: use the network first then cache or cache first then network.  Which one is use depends on if ou use a specific URL to get the data.  After doing the Angular tutorial and getting exposed to TypeScript I wonder if this type of thing could eventually be handled by their annotations?

Finally at the end there's a section about adding your platform-specrific metadata in an application manifest.  Would be nice if it was standardized across all major platforms instead of being vendor-specific (gross).

This was a well-written tutorial.  I had some issues running it offline where the code still kept trying to access the live Yahoo! Weather API instead of going to the cache directly.  I'll have to figure that out before releasing this in any shape or form.  I think a good project that could come out of this would be a to-do app.  I know it's a cliche at this point but it's a good way to exercise both my Angular and Progressive Web App skills.
