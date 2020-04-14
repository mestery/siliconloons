siliconloons
============

[![Netlify Status](https://api.netlify.com/api/v1/badges/41da72e5-3f60-4712-a652-7fbf085ee740/deploy-status)](https://app.netlify.com/sites/brave-brown-9afa0a/deploys)
[![Build Status](https://travis-ci.org/mestery/siliconloons.svg?branch=master)](https://travis-ci.org/mestery/siliconloons)
[![GitHub license](https://img.shields.io/badge/license-Apache%20license%202.0-blue.svg)](https://github.com/mestery/siliconloons/blob/master/LICENSE)

Silicon Loons Blog Site

Howto
=====

To generate this site, follow the instructions below:

1. Clone this repository, including submodules:

   `git clone --recurse-submodules git@github.com:mestery/siliconloons.git`

2. Build the site using hugo

   `hugo --theme=terminal`

3. Sync the content out to your hosting provider:

   `rsync -avz -e ssh public/* mestery@sadira.dreamhost.com:siliconloons.com/`

4. You're done!

To create a new post, run a command such as the following:

   `hugo new posts/2014-12-26-welcome-to-hugo.md`

References
==========
The following are links for references for working with Hugo and Markdown:

* Markdown Cheatsheet: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
* VIM spell checking: http://robots.thoughtbot.com/vim-spell-checking
