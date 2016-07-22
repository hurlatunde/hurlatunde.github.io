---
layout: post
title: Running with Jekyll on Windows - Part one
excerpt: "A step-by-step guide to setting up Jekyll on Windows by @hurlatunde."
categories: [Jekyll, Windows, Git]
tags:
    - HTML
    - CSS
    - Jekyll
    - Git
    - Windows
comments: true
---

## Introduction

[Jekyll](http://jekyllrb.com/), a simple, blog-aware, static site generator, is very easy to set up on Mac OS X or Linux. On Windows, not so much.

Please note: Using Jekyll on Windows is not officially supported by the Jekyll team. And while this guide is featured on [the Jekyll website](http://jekyllrb.com/), it remains unofficial.


### Get started: Install Ruby and the Ruby DevKit

Ruby is the programming language that Jekyll is written in. You’ll need to install Ruby and the corresponding DevKit, which is needed to build some of Jekyll’s dependencies as “native extensions”.

#### Install Ruby

First, click on the button below and download the installer for Ruby v2.0.0 that matches your system’s architecture (x86 / x64).

<a href="http://rubyinstaller.org/downloads/" target="_Blank" class="btn btn-lg btn-block btn-success"> Get Ruby for Windows </a>

Execute the installer and go through the steps of the installation. When you get to the screen below, make sure to check the “Add Ruby executables to your PATH” box.

![Smithsonian Image](http://jekyll-windows.juthilo.com/public/img/ruby-path.png)

Click Install and Ruby will be installed within seconds.

#### Install the Ruby DevKit

Jekyll has some dependencies which, out of the box, only provide raw source code. To make them into fully functional executables, you’ll probably need to install the Development Kit.

Click the button below and download the DevKit archive that corresponds to your Ruby installation and system architecture. For Ruby v2.0.0, the file name will begin with `DevKit-mingw64`. Choose the 32bits or 64bits version depending on your system.

<a href="http://rubyinstaller.org/downloads/" target="_Blank" class="btn btn-lg btn-block btn-success"> Get the Ruby DevKit </a>

The download is a self-extracting archive. When you execute the file, it’ll ask you for a destination for the files. Enter a path that has no spaces in it. We recommend something simple, like `C:\RubyDevKit\`. Click Extract and wait until the process is finished.

Next, you need to initialize the DevKit and bind it to your Ruby installation. Open your favorite command line tool and navigate to the folder you extracted the DevKit into.

{% highlight html %}
cd C:\RubyDevKit
{% endhighlight %}

Auto-detect Ruby installations and add them to a configuration file for the next step.

{% highlight html %}
ruby dk.rb init
{% endhighlight %}

Install the DevKit, binding it to your Ruby installation.

{% highlight html %}
ruby dk.rb install
{% endhighlight %}

## Summary
That’s it! If all went well, you now have a working Ruby installation on your machine and you can build fully functional executables using the Ruby Development Kit.


#### Read more:
* [Jekyll Windows by juthilo](http://jekyll-windows.juthilo.com/1-ruby-and-devkit/)
* [Jekyll on Windows](https://jekyllrb.com/docs/windows/)
* [Jekyll on Windows by davidburela](https://davidburela.wordpress.com/2015/11/28/easily-install-jekyll-on-windows-with-3-command-prompt-entries-and-chocolatey/)
