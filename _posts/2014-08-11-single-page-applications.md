---
layout: post
title:  "Single page applications"
date:   2014-08-11 09:00:01
categories: js
---

Single page applications (SPA) are *supposed* to 'provide a more fluid user experience' [[0](#ref0)] but beware of the following fatal pitfalls:

## Navigation and fast back

Browsers store history, meaning, these pages can load very quickly when the user presses the back button. SPAs need to recreate this functionality. As Daniel Puplus says in his article [[1](#ref1)]:

> "Back should be quick; users don’t expect data to have changed much.

> "When a user presses the browser’s back button they expect the change to happen quickly and for the page to be in a similar state to how it was last time they saw it.

> "In the traditional web model the browser will typically be able use a cached version of the page and linked resources.

> "In a naive implementation of a SPA hitting back will do the same thing as clicking a link, resulting in a server request, additional latency, and possibly visual data changes."

Upon 'navigating', the application will need to a way of storing and retrieving 'pages' from a cache. Unless of course we want to slow down the speed of loading 'pages', which is *meant* to be a significant benefit of SPAs. Storage could be memory, local (or session) storage, client-side database or cookies.

**Note: The words 'navigating' and 'pages' are in quotes because SPAs, by definition don't have the concept of navigation and pages in the traditional sense. Quotes will be discarded for brevity going forward.**

The application will also need to determine when to store and retrieve pages from it. Navigation typically utilises `pushState` or `hashchange` and the application will need to differentiate between the user changing the URL (via clicking a link or typing a URL in the location bar) or manually hitting back/forward, which is not trivial [[2](#ref2)].

## Navigation and remembering scroll history position

Browsers remember the scroll position of the pages you have visited which is very convenient. As Daniel Puplus says in his article:

> "Lots of sites get this wrong and it’s really annoying. When the user navigates using the browser’s forward or back button the scroll position should be the same as it was last time they were on the page. This sometimes works correctly on Facebook but sometimes doesn’t. Google+ always seems to lose your scroll position."

Clicking forward or back should remember the scroll position, but unfortunately, as SPAs rely on faux navigation this functionality is absent.

Upon navigation, the application will need to remember the scroll position so that it can be retrieved later. This is a topic heavily related to "Navigation and fast back" discussed previously.

## Cancelling navigation

Browsers provide a cancel button, which when pressed, cancels the loading of the requested page. Also, if a user clicks another link, the browser will cancel the previous request. This is useful for performance and also ensures the user's internet data allowance isn't eaten up unnecessarily.

Pages in SPAs are likely to be retrieved via XHR, meaning several requests could be in progress at the same time; the first page request might be loaded last, even though it should have been cancelled out by the second page request.

Also, the *same* link could be clicked twice, meaning the page will be requested (and loaded) twice, which is not efficient and could also cause visual glitches.

The application needs to reproduce the aforementioned browser functionality. This means exposing a custom cancel button, which is obviously not desirable, and the application needs to handle duplicate requests as well as cancelling out all previous requests that are still in progress.

## Navigation and data loss

Browsers normally provide the `beforeunload` event which allows the application to warn against losing unsaved changes.

The application would need to provide this functionality, before any routing takes place.

## Search engine optimisation

Some SPAs don't require SEO. For those that do, whilst there are solutions, they aren't easy or effortless [[3](#ref3)].

## Navigation and loading CSS &amp; JS

If an SPA grows to a significant size, loading the entire application on page load may be detrimental to the experience because it's akin to loading all pages of a website when only the home page was requested.

Unfortunately, this leads to the requirement to load CSS and JS for certain pages. Script loading is notoriously difficult and contains unreliable hacks [[4](#ref4)]. This can be fatal to the reliability of the application. Reliability should obviously be valued highly.

## Summary

SPAs are meant to provide a better experience. It is therefore ironic that SPAs require significantly more development effort with a result that is detrimental to the user experience.

Remember that websites can still have rich-user interfaces without cramming the entire site into one document. All of the issues described in this article arise due to the choice of architecting a website as as an SPA.

Furthermore, it is interesting to note that sites, such as Twitter [[5](#ref5)] and Lifehacker [[6](#ref6)], realised the SPA architecture was a mistake and have since reverted their architectures. **Avoiding the SPA architecture avoids the pitfalls**.

<dl>
	<dt><a name="ref0"></a>[0]</dt>
	<dd><a href="http://en.wikipedia.org/wiki/Single-page_application">Wikipedia: SPAs</a></dd>
	<dt><a name="ref1"></a>[1]</dt>
    <dd><a href="https://medium.com/joys-of-javascript/4353246f4480">Beyond pushState - building single page applications</a></dd>
	<dt><a name="ref2"></a>[2]</dt>
	<dd><a href="http://stackoverflow.com/questions/2008806/how-to-detect-if-the-user-clicked-the-back-button">Stackoverflow: Detecting back button click</a></dd>
	<dt><a name="ref3"></a>[3]</dt>
	<dd><a href="http://stackoverflow.com/questions/7549306/single-page-js-websites-and-seo">Stackoverflow: SPAs and SEO</a></dd>
	<dt><a name="ref4"></a>[4]</dt>
	<dd><a href="http://blog.getify.com/labjs-script-loading-the-way-it-should-be/">Script loading hacks</a></dd>
    <dt><a name="ref5"></a>[5]</dt>
    <dd><a href="https://blog.twitter.com/2012/improving-performance-on-twittercom">Improving performance on twitter</a></dd>
    <dt><a name="ref6"></a>[6]</dt>
    <dd><a href="http://isolani.co.uk/blog/javascript/BreakingTheWebWithHashBangs">Lifehacker and the hash bang debarkle</a></dd>
</dl>