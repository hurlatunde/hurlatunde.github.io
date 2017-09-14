---
layout: post
title: Jekyll template guide
date:   2016-07-22 10:18:00
subclass: 'post tag-test tag-content'
navigation: True
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover7.jpg'
comments: true
excerpt: "A step-by-step guide for Jekyll template"
categories: [Jekyll, Windows, Git, template , step-by-step ,guide]
comments: true
tags: HTML CSS Jekyll
---

## Get up and running in seconds.

Markdown (or Textile), Liquid, HTML & CSS go in. Static sites come out ready for deployment.

{% highlight html %}
gem install jekyll
jekyll new my-awesome-site
cd my-awesome-site
/my-awesome-site $ jekyll serve
# => Now browse to http://localhost:4000
{% endhighlight %}

### Configuration

Jekyll allows you to concoct your sites in any way you can dream up, and it’s thanks to the powerful and flexible configuration options that this is possible. These options can either be specified in a `_config.yml` file placed in your site’s root directory, or can be specified as flags for the `jekyll` executable in the terminal.

### Setting

The table below lists the available settings for Jekyll, and the various `options` (specified in the configuration file) and `flags` (specified on the command-line) that control them.

{: .table .table-striped .table-bordered}
| SETTING | OPTIONS AND FLAGS |
|:--------|:-------:|--------:|
| <strong> Site Source </strong> <br> Change the directory where Jekyll will read files |  `source: DIR` <br> `-s, --source DIR` |
| <strong> Site Destination </strong> <br> Change the directory where Jekyll will write files |  `destination: DIR` <br> `-d, --destination DIR` |
| <strong> Safe </strong> <br> Disable custom plugins, and ignore symbolic links. |  `safe: BOOL` <br> `--safe` |
| <strong> Exclude </strong> <br> Exclude directories and/or files from the conversion. These exclusions are relative to the site's source directory and cannot be outside the source directory. |  `exclude: [DIR, FILE, ...]` |
| <strong> Include </strong> <br> Force inclusion of directories and/or files in the conversion.  `.htaccess` is a good example since dotfiles are excluded by default. |  `include: [DIR, FILE, ...]` |
| <strong> Time Zone </strong> <br>Set the time zone for site generation. This sets the `TZ` environment variable, which Ruby uses to handle time and date creation and manipulation. Any entry from the IANA Time Zone Database is valid, e.g. `America/New_York`. A list of all available values can be found here. The default is the local time zone, as set by your operating system. |  `timezone: TIMEZONE` |
| <strong> Encoding </strong> <br> Set the encoding of files by name (only available for Ruby 1.9 or later). The default value is `utf-8` |  `encoding: ENCODING` |

read more about settings - [jekyllrb configuration](https://jekyllrb.com/docs/configuration/)

## jekyll Templates

Jekyll uses the Liquid templating language to process templates. All of the standard Liquid tags and filters are supported. Jekyll even adds a few handy filters and tags of its own to make common tasks easier.

[http://jekyllrb.com/docs/templates/](http://jekyllrb.com/docs/templates/)

<div class="embed-responsive embed-responsive-16by9">
<iframe class="embed-responsive-item" src="https://www.youtube.com/embed/7-7W2sKhnyc" frameborder="0" allowfullscreen></iframe>
</div>

#### Read more:
* [Jekyll cheat](http://jekyll.tips/jekyll-cheat-sheet/)
* [Jekyll theme by leonids](https://github.com/renyuanz/leonids)
* [Jekyll Windows by juthilo](http://jekyll-windows.juthilo.com/1-ruby-and-devkit/)
* [Jekyll on Windows](https://jekyllrb.com/docs/windows/)
* [Jekyll on Windows by davidburela](https://davidburela.wordpress.com/2015/11/28/easily-install-jekyll-on-windows-with-3-command-prompt-entries-and-chocolatey/)
