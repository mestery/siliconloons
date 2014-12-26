---
title: Unit Test Frameworks for “C”
author: mestery
date: 2011-11-08
url: /unit-test-frameworks-for-c/
socialsharing: true
tmac_last_id:
  - 544156019165655040
categories:
  - Programming
tags:
  - C Language
  - Development
  - Programming
---
A recent project had me looking into useable Unit Test Frameworks for the &#8220;C&#8221; programming language. After doing some initial research, wikipedia ended up showing me a <a title="Unit Test Frameworks in C" href="http://en.wikipedia.org/wiki/List_of_unit_testing_frameworks#C" target="_blank">large list of frameworks</a>, of which the majority appear to be dead or not used anymore. After doing some initial scanning, I decided to look into a handful:

  * I initially looked into <a title="check" href="http://check.sourceforge.net/" target="_blank">check</a>. This one is mostly current, still appears to be maintained, and looks like a large list of open source projects use this for their own unit test needs.
  * I also look at <a title="cmockery" href="http://code.google.com/p/cmockery/" target="_blank">cmockery</a>. This is a Google project to provide a fast, easy unit test framework for &#8220;C&#8221;. However, this one looks older than check, and doesn&#8217;t appear to be actively maintained.
  * The last one I looked at was <a title="FCTX" href="http://fctx.wildbearsoftware.com/" target="_blank">FCTX</a>. Ultimately, this is the one I chose.

<div>
  FCTX has the following advantages:
</div>

<div>
  <ul>
    <li>
      It provides a robust unit test framework, all while being written and existing in a single header file.
    </li>
    <li>
      It is licensed under the BSD license, which makes it friendly for commercial projects.
    </li>
    <li>
      It is actively maintained, with the latest release coming out in April, 2011.
    </li>
  </ul>
  
  <div>
    I&#8217;m in the process of trying to write unit tests with this now. Once I&#8217;ve played with it a bit, I&#8217;ll either update this post or write a new one detailing the actual experience of using FCTX for unit test creation.
  </div>
</div>
