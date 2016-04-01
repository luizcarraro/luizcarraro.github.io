---
layout: post
title: Ember-cli first install troubleshooting
tags: [ember]
excerpt_separator: <!--more-->
---

So today I've just installed Ember-cli and was trying to create my initial project using the following command:
<!--more-->

~~~
$ ember new ProjectName
~~~

After the initial folders configuration managed by ember-cli, the bower fase ended the process with the following:

Failed to execute "git ls-remote --tags --heads git://github.com/components/handlebars.js.git", exit code of #128
The Solution

Run the following command:

~~~
git config --global url."https://".insteadOf git://
~~~

This will make git use https instead of git when downloading packages.

Note: this must be the first thing to appear in your config file in ~/.gitconfig