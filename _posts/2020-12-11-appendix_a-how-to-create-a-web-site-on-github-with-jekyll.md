---
layout: front
title:  "Appendix A. Fixing the errors in Install the jekyll and bundler."
date:   2020-12-11 01:01:01 +0900
categories: jekyll tutorial
---

## Overview

This is an appendix for `How to create a web site on Github with Jekyll (1)`.

## Problem

Running the original command in the instructions results in an error. 

```bash
$ jekyll new myblog
bash: /usr/bin/jekyll: No such file or directory
$
```

Without configuring `GEM_HOME`, the following error occurs. 

```bash
$ gem install jekyll bundler
ERROR:  While executing gem ... (Gem::FilePermissionError)
    You don't have write permissions for the /var/lib/gems/2.5.0 directory.
$
```

## Hint

Google search: "ERROR: While executing gem ... (Gem::FilePermissionError) You don't have write permissions for the /var/lib/gems/2.5.0 directory."

## Solution

*  [You don't have write permissions for the /var/lib/gems/2.3.0 directory](https://stackoverflow.com/questions/37720892/you-dont-have-write-permissions-for-the-var-lib-gems-2-3-0-directory)

> If you want to use the distribution Ruby instead of rb-env/rvm, you can set up a `GEM_HOME` for your current user. Start by creating a directory to store the Ruby gems for *your* user:
>
> ```
> $ mkdir ~/.ruby
> ```
>
> Then update your shell to use that directory for `GEM_HOME` and to update your `PATH` variable to include the Ruby gem bin directory.
>
> ```
> $ echo 'export GEM_HOME=~/.ruby/' >> ~/.bashrc
> $ echo 'export PATH="$PATH:~/.ruby/bin"' >> ~/.bashrc
> $ source ~/.bashrc
> ```
>
> (That last line will reload the environment variables in your current shell.)
>
> Now you should be able to install Ruby gems under your user using the `gem` command. I was able to get this working with Ruby 2.5.1 under Ubuntu 18.04. If you are using a shell that is not Bash, then you will need to edit the startup script for that shell instead of `bashrc`.

