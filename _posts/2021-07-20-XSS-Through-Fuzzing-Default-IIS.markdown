---
layout: post
title: XSS-Through-Fuzzing-Default-IIS
date: 2021-07-20 12:13 +0600
image: "/images/IIS-RXSS.jpg"
permalink: /XSS-Through-Fuzzing-Default-IIS/
tags: IIS Fuzzing Reflected-XSS
featured: false
---

<p>Hello World, Another Blog related to IIS. In this blog i am going to write about how i found a reflected cross site scripting on one of the popular bug bounty program </p>

* We know Rxss is an easy bug to find in most cases, but the reason for writing this blog post is I submitted nearly 20 XSS bugs to the same program but 19 of them are duplicate and only this one is accepted. The bug is present there for a long time. In this blog post i am going to share my approach in finding this one

* If you havent read the recent blog, check it out here -->  <a href="https://0xdln1.github.io/IIS-Default-Page-to-Information-Disclosure/">IIS-Default-Page-to-Information-Disclosure</a>

### Default IIS Page

* Whenever i see a default iis page i get  excited because there a lot of chances for finding Bugs there

* As mentioned in the previous blogpost i ran IIS Shortname scanners but this webserver is not vulnerable

* I decided to do general content discovery with ffuf
    
* So i ran ffuf with jhaddix content_discovery_all.txt
    
<div class="language-bash"><div class="highlight"><pre class="highlight"><code> ffuf -u https://sub.redacted.com/FUZZ -w content_discovery_all.txt -fc 404
</code></pre></div></div>

<div class="language-bash"><div class="highlight"><pre class="highlight"><code> /manager - 403
</code></pre></div></div>

* The path /manager gave a 403 Forbidden 

* Fuzzing again gave access to a Login Panel

<div class="language-bash"><div class="highlight"><pre class="highlight"><code> ffuf -u https://sub.redacted.com/manager/FUZZ -w content_discovery_all.txt -fc 404
</code></pre></div></div>

<div class="language-bash"><div class="highlight"><pre class="highlight"><code>/default.aspx - 200
</code></pre></div></div>

* I tried default credentials manually but none of them Worked

* After spending sometime i obeserver the path is being reflected in the source code without sanitisation 
<div class="language-bash"><div class="highlight"><pre class="highlight"><code>http://sub.redacted.com/beta/default.aspx/%27%3E%3C/script%3E%3Cscript%3Ealert(document.cookie)%3C/script%3E </code></pre></div></div>

The above payload executed successfully 


* Fuzzing often gives access to juicy endpoints.

<p> That's it for now. Cheers !!  Happy Hacking :)