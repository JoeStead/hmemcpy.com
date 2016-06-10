﻿---
title: '[FW]orking in Github - a slightly better workflow?'
date: 2014-01-06T11:53:06+00:00
---
_If you don't understand the title, I tried to be clever and used_ [_regular ex_p_ressions_](http://www.regular-expressions.info/charclass.html)_. I now have 2 problems._

I've been using git and github for a while now, but only recently found out it's possible to define 2 separate URLs for fetching and pushing. Often times, when I wanted to contribute to an open source project, I had to go through the ceremony of a) forking the repository b) cloning the fork to my machine and c) define an [upstream remote](https://help.github.com/articles/syncing-a-fork) to keep the fork in sync with the changes from the original repository.

Defining the upstream repository is my least favorite part of working with git/github &ndash; I always have to look up the steps how to do it. Instead of keeping the fork in sync, I just want to be able to **fetch** the changes from the original (upstream) repository, but **push** the changes into my own fork.

Turns out, git supports this scenario! Normally, when you type **git remote &ndash;v**, you get the following output:

<pre>&gt; git remote -v

origin git@github.com:username/MyForkedRepository.git (fetch) 
origin git@github.com:username/MyForkedRepository.git (push)
</pre>

As you can see, the remote *˜origin' defines 2 URLs, one with label _fetch_ and one with _push_. Let's set a different URL for the original, upstream repository (the one to _**fetch**_ from):

<pre>git remote set-url origin git@github.com:NancyFx/Nancy.git
</pre>

And another URL to my own fork (the one to **_push_** to):

<pre>git remote set-url --push origin git@github.com:hmemcpy/Nancy.git</pre>

And that's it, I can now fetch and push normally, without having to worry about which remote I'm using!

N.B.

You can also do this by directly modifying the `.git/config` file, and adding a separate `pushurl` value under `[remote "origin"]:`

<pre>...
[remote "origin"]
 fetch = +refs/heads/*:refs/remotes/origin/*
 url = git@github.com:NancyFx/Nancy.git
 pushurl = git@github.com:hmemcpy/Nancy.git
...
</pre>

Alternatively, if you're using [GitExtensions](https://code.google.com/p/gitextensions/) on Windows, you can go to **Repository** &ndash; **Remote repositories** in the menu, and check the _Separate Push URL_ checkbox:

<img title="" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="" src="http://i1.wp.com/hmemcpy.com/wp-content/uploads/2014/01/image.png?resize=670%2C332" data-recalc-dims="1" />
