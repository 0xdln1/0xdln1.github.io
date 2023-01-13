---
layout: post
title: Application-Level-DoS-mastodon
date: 2023-01-13 12:13 +0600
image: "/images/mdos/dos.png"
permalink: /Application-Level-DoS-mastodon/
tags: DOS bugbounty
featured: true
---

Hey everyone!  It's 0xdln here! So, me and my friend @0xrj were poking around the Mastodon public program on intigriti and we stumbled upon some pretty interesting vulnerabilities that we thought you might find interesting. From bypassing link length restrictions to causing server crashes, it was a wild ride. 

### Description

This bug could allow a malicious attacker to make a mastodon server down i.e Denial of service, after posting a toot ( similar to tweet in twitter ) 

### Details

Mastodon allows a toot feature where users can share information just like twitter.
While testing this feature, we observed that there is a restriction on the length of toot, This feature looks buggy and we started to try attempts of bypassing it.

After reviewing the documentation for the toot feature, we understood that links can be longer than 250 characters but still there is a restriction on link length. 

* Performing DoS by tooting with payload

Through trial and error, we found a way to bypass this restriction by using a payload that exceeds the limit, causing the toot to behave as normal text instead of a link.

![payload1](/images/mdos/payload-mdos-1.png)

This toot caused the backend to crash and resulted in a 504 Gateway Timeout error. We promptly reported this as a high-severity vulnerability and were informed that it was a valid issue, but with a reduced severity rating of medium. We understand that the team may have determined this severity based on the limited impact.

* Increasing Severity

To further explore the potential impact of this vulnerability, we attempted to include hashtags in our payload and found that it caused the entire server to become inaccessible. The hashtag reflected on multiple locations, affecting every endpoint and every user connected to the server.

![payload2](/images/mdos/payload-mdos-2.png)

We discussed this with the team and upgraded the severity rating to high

![severity-discussion](/images/mdos/mdos-seeverity-discussion.png)

### Exploitation

* Step 1 : Post a toot1 with contents of payload1 and the server will respond with Gateway Timeout error.  
* Step 2 : Now Post a toot2 in new tab with contents of payload2.
* Step 3 : Now nothing will be accessible like profiles , hashtag etc 

### Timeline

![timeline](/images/mdos/mdos-timeline.png)

Keep an eye out for more updates on our discoveries and let us know if you have any thoughts or questions.

Follow us on twitter

[@0xdln](https://twitter.com/0xdln) , [@0xrj][https://twitter.com/JagadeshRonanki]