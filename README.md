siliconloons
============

Silicon Loons Blog Site

Howto
=====

To generate this site, follow the instructions below:

1. Glone this repository

   git clone git@github.com:mestery/siliconloons.git

2. Clone the themes repository:

   git clone --recursive https://github.com/spf13/hugoThemes themes

3. Build the site using hugo

   hugo --theme=redlounge

4. Sync the content out to your hosting provider:

   rsync -avz -e ssh mestery@sadira.dreamhost.com:siliconloons.com/ public/*

5. You're done!

To create a new post, run a command such as the following:

   `hugo new posts/2014-12-26-welcome-to-hugo.md`

References
==========
The following are links for references for working with Hugo and Markdown:

* Markdown Cheatsheet
** https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
