---
layout: post
title: Running with Jekyll on Windows - Part two
date:   2016-07-21 10:18:00
subclass: 'post tag-test tag-content'
navigation: True
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover7.jpg'
comments: true
excerpt: "A step-by-step guide to setting up Jekyll on Windows by @hurlatunde."
categories: [Jekyll, Windows, Git]
comments: true
tags: HTML CSS Jekyll Git Windows
---


## Install the Jekyll Gem

Jekyll itself comes in the form of a Ruby Gem, which is an easy-to-install software package. To install Jekyll and all its default dependencies, launch your favorite command line tool and enter the following command.

{% highlight html %}
gem install jekyll
{% endhighlight %}

Hit enter, watch, enjoy. This might take a while due to the number of dependencies. [ i know i had to wait, it may be nothing or just the internet ]

### Summary
Tada! You have successfully installed Jekyll. In fact, you can already build and serve sites without errors, unless there are blocks of code in there and you want to use syntax highlighting.

### Use subfolders

Jekyll cannot build or serve sites from certain system-reserved folders on Windows, like your user folder. Instead, it will output an error looking like this:

{% highlight html %}
C:\Users\You>jekyll serve
Configuration file: C:\Users\You\_config.yml
            Source: C:\Users\You
       Destination: C:\Users\You\_site
      Generating...
jekyll 2.4.0 | Error: Permission denied - .
{% endhighlight %}

If you encounter such an error, move your site to a subdirectory (e.g., `C:\Users\You\awesome-jekyll-site`) and try again.

{% highlight html %}
jekyll build
jekyll build --watch
jekyll build -w
jekyll serve
jekyll serve --watch
jekyll serve -w
{% endhighlight %}

You can now run all of the above commands on your Windows machine. Congratulations! You have successfully set up Jekyll on Windows.

Found something that wasn’t quite clear? Is something in this guide outdated? Did I forget something? Please [look if somebody else noticed it already](https://github.com/juthilo/run-jekyll-on-windows/issues?state=open) or file a new issue on GitHub if that’s not the case. Thanks!

If you need help with using Jekyll in general, please visit the [official Jekyll website](http://jekyllrb.com/).

#### Read more:
* [Jekyll Windows by juthilo](http://jekyll-windows.juthilo.com/1-ruby-and-devkit/)
* [Jekyll on Windows](https://jekyllrb.com/docs/windows/)
* [Jekyll on Windows by davidburela](https://davidburela.wordpress.com/2015/11/28/easily-install-jekyll-on-windows-with-3-command-prompt-entries-and-chocolatey/)
