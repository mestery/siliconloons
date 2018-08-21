siliconloons
============

Silicon Loons Blog Site

Howto
=====

To generate this site, follow the instructions below:

1. Clone this repository, including submodules:

   `git clone --recurse-submodules git@github.com:mestery/siliconloons.git`

2. Build the site using hugo

   `hugo --theme=redlounge`

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
