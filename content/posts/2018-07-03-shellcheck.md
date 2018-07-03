---
author: mestery
Description: "ShellCheck: Static analysis for shell scripts"
socialsharing: true
url: ""
categories:
  - open source
  - developer
  - CI/CD
tags:
  - open source
  - developer
  - CI/CD
title: "ShellCheck: Static analysis for shell scripts"
date: 2018-07-03T10:48:51-05:00
---

I recently stumbled upon [ShellCheck][1]. ShellCheck is a tool to provide static
analysis support for your shell scripts. From their website:

> ShellCheck is:
>
> * GPLv3: free as in freedom
> * available on GitHub
> * already packaged for your distro or package manager
> * supported as an integrated linter in major editors
> * available in CodeClimate and Codacy to auto-check your GitHub repo
> *written in Haskell, if you're into that sort of thing.

Go and check it out on [github][2] and ensure you have static analysis for your
shell scripts covered in your CI system of choice.

I'm [adding this][3] into NetworkServiceMesh at the moment, as I spent a few hours
debugging something which ShellCheck would have caught quickly for me. As a good
friend used to say: "If it's not tested in CI, it's not working," Good advice.

[1]: https://www.shellcheck.net
[2]: https://github.com/koalaman/shellcheck
[3]: https://github.com/ligato/networkservicemesh/pull/141
