---
layout: post
title: XSS-Special-Cases
date: 2021-07-27 12:35 +0600
image: "/images/XSS-Special.jpg"
permalink: /XSS-Special-Cases/
tags: Reflected-XSS
featured: true
---

<p>Hello World, while Doing Bug Bounty Hunting i came accross some Special XSS Cases. In this blog Post i will write about them.</p>

### 1) XSS That Works only in mobile Devices

Recently i was hunting on a program and testing parameters for XSS and that website has a strong waf since it is a banking related website

* All tags are blocked and mostly all event handlers are blocked, i tried bypassing the waf and was about to give up.

* I noticed normal strings like FUZZ are beign reflected but whenever i use it with an event handler in the payload, i am getting blocked by the waf.

* So i tried all eventhandlers from [Portswigger Cheatsheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet) and only below event handlers gave a response of 200 OK

<div class="language-text"><div class="highlight"><pre class="highlight"><code>touchstart
touchmove
touchcancel
touchend
</code></pre></div></div>

Using them in the payload like this didn't pop any alert, after googling about these eventhandlers a bit, i understood that these event handlers only work with mobile devices.

<div class="language-text"><div class="highlight"><pre class="highlight"><code>https://REDACTED.COM/SOMEPATH/Amount?UNIQUE_TICKET_ID=XXXXXXX&LANG=EN&name=0%22ontouchend%3Dalert(document.cookie)%20
</code></pre></div></div>

The developers blocked all event handlers but not mobile event handlers.
Using Toggle Device Toolbar in the chrome dev tools, we can simulate the mobile device environment, so i quickly changed that and clicking on name field popped an alert with cookies


### 2) XSS in Hidden Input

You might be already familier with this one. But i didn't knew about this, until recently one of the target i was hacking on, was vulnerable to this

Portswigger has a good blog post -> [Xss in Hidden Input Fields](https://portswigger.net/research/xss-in-hidden-input-fields)

[+] I will keep updating this blog post when i found any interesting cases of xss. If you know any ping me on [twitter](http://twitter.com/0xdln). I will add them here and give you credits
<p> That's it for now. Cheers !!!  Happy Hacking :)