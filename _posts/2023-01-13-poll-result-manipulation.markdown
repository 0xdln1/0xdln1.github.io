---
layout: post
title: poll-result-manipulation-on-mastodon
date: 2023-01-13 12:13 +0600
image: "/images/mpoll/cover.png"
permalink: /poll-result-manipulation-on-mastodon/
tags: business-logic bugbounty
featured: true
---

Hey everyone!  It's [@0xdln](https://twitter.com/0xdln) here! So, me and my friend [@0xrj](https://twitter.com/JagadeshRonanki) were poking around the Mastodon public program on intigriti and we stumbled upon some pretty interesting vulnerabilities that we thought you might find interesting.

# Poll Result Manipulation

## Description

During our hunt we discovered a bug in a polling feature that allows for unrestricted and improper handling of request data. This bug could allow an attacker to flood and manipulate the poll results, making it a serious vulnerability.

## Details

As usual we tried attempting to bypass various restrictions imposed on the polls, such as time limits and duplicate options. However, we were unable to find any weaknesses in these restrictions.

Now, It’s time to inspect for the request and response and we observed that when a user votes in a poll, the request is sent in the following format:


<div class="language-json"><div class="highlight"><pre class="highlight"><code>POST /api/v1/polls/262/votes HTTP/1.1
Host: xxxxxxx.mastodon.social
Accept: application/json, text/plain, */*
.
.
.
{
    "choices":["0","6"]
}
</code></pre></div></div>

We then tried to manipulate the request by sending an empty array of choices and still successfully submit the vote. However, none of the options were actually voted for but the total vote count was incremented.

This vulnerability also allows an attacker to vote multiple times if no choice is selected, giving the attacker the ability to flood the poll with fake votes and bring the voting result to 0 for all options.

<div class="language-json"><div class="highlight"><pre class="highlight"><code>POST /api/v1/polls/262/votes HTTP/1.1
Host: xxxxxxx.mastodon.social
Accept: application/json, text/plain, */*
.
.
.
{
 "choices":[]
}
</code></pre></div></div>

![poll](/images/mpoll/poll.png)

## Exploitation

1. The attacker creates a poll from a victim's account and posts it.
2. The attacker votes from their own account, while intercepting the request.
3. The attacker removes the options from the choices array in the json body { "choices": [] } and sends the request multiple times to flood the poll with fake votes.
4. Legitimate users try to vote, but the results come to 0 for all options.

## Takeaways

This vulnerability highlights the importance of proper handling of request data, and the need for proper validation and sanitization of user input.

### Timeline

![timeline](/images/mpoll/timeline.png)


Keep an eye out for more updates on our discoveries and let us know if you have any thoughts or questions.

Follow us on twitter [@0xdln](https://twitter.com/0xdln) , [@0xrj](https://twitter.com/JagadeshRonanki)