---
author: mestery
Description: "New Blog Hosting Platform: Netlify!"
socialsharing: true
url: ""
categories:
  - Blog
  - Web
  - CDN
tags:
  - Blog
  - Web
  - CDN
title: "New Blog Hosting Platform: Netlify!"
date: 2018-03-04T14:32:16-06:00
---

After running my own Hugo install on various platforms for the past 3 years or
so, I made the move to [Netlify][1] today. Why the move? For a variety of
reasons, which include:

* Global CDN
* DNS built-in
* Free One-Click SSL!
* Integrated with github, gitlab, and bitbucket

All of these benefits alone would have made the move worth it. But the real
kicker for me was that my workflow to generate blog posts was causing friction,
which in turn meant I blogged less. As great as hugo was, running the entire
stack myself was proving problematic. Enter netlify, thanks to a recommendation
from [Jessie Frazelle][1] on twitter:

{{< tweet 969978905854664704 >}}

After spending the better part of a morning sick with the flu, I was able to
transition the site over. And I'm already thrilled and looking forward to an
easier workflow, which will allow me to blog more often.

The following articles were helpful in this transition. I'm sharing them here
as they helped me quite a bit. I had an issue with themes, similar to what
[Richard's blog post][5] details. Once I figured out how to setup git submodules
for my theme, it worked quite well.

* [Host on Netlify][3]
* [Moving your Hugo blog to Netlify by Ken Cochrane][4]
* [Getting Hugo Running on Netlify by Richard Littauer][5]

[1]: https://www.netlify.com
[2]: https://twitter.com/jessfraz
[3]: https://gohugo.io/hosting-and-deployment/hosting-on-netlify/
[4]: https://www.kencochrane.net/2016/11/20/i-rebuilt-my-blog-with-hugo-and-moved-to-netlify/
[5]: https://www.burntfen.com/2017-04-16/getting-hugo-running-on-netlify
