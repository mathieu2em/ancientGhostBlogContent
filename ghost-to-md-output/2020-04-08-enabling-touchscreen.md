---
title: Enabling Touchscreen Scrolling On Firefox With Ubuntu 14+.
slug: enabling-touchscreen
date_published: 2020-04-09T01:20:28.000Z
date_updated: 2021-01-11T01:38:49.000Z
tags: tweaks
excerpt: little tutorial about how to enable touchscreen scrolling in firefox with linux ubuntu 14+
---

Yep, looks like it still isn't handled automatically!

You have to do do some little tweaks for it to work.

First, **open Firefox** and in the navigation bar, **write about:config**
![](/content/images/2020/04/image.png)It will open this page
Then, search for **dom.w3c_touch_events.enabled** and change the value of it to **1**.

Now, close Firefox and **open /etc/security/pam_env.conf ** with your favorite code editor. You will have to use a **sudo** here as it is normally protected.

At the bottom of the file ,  paste this code: 

`MOZ_USE_XINPUT2 DEFAULT=1`

Now, reboot your computer and you should be good to go ! :)

Post picture by [Elia Pellegrini](https://unsplash.com/@eliapelle?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/touch?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText)
