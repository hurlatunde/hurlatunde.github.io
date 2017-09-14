---
layout: post
title: Getting started with React.js and Gulp
date:   2016-11-24 10:18:00
subclass: 'post tag-test tag-content'
navigation: True
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover7.jpg'
comments: true
excerpt: "A step-by-step guide for using gulp with react.js"
categories: [react, web, gulp, npm, step-by-step ,guide, learning, understand react]
comments: true
tags: HTML JavaScript CSS Gulp React.Js
---

I’ve been learning React.js building user interfaces for the past couple of days, and belive me it as been really challenging.

Please check in mind that at the time of this post the current version of React is 0.14 and also please bear in mind that am just learning this as well but i think i have the tools and skills to share a-little that i have come to accrued in the last couple of day, After a couple of days of learning the basics (reading their Getting Started introduction to React and following their tutorial), I feel i should configured a basic gulpfile.js to include React in my local development environment.


Note: If you’re new to gulp, you may want to get familiarized with it before continuing (this post assumes you’re familiar with it). 
Here are some articles to get you started [getting started with gulp](http://alistapart.com/blog/post/getting-started-with-gulp) by alistapart and 
[getting started gulp](https://css-tricks.com/getting-started-gulp/) by css-tricks


### My gulp workflow features the following:

* Convert JSX to JavaScript
* Concatenate JavaScript files
* BrowserSync with auto-refresh of CSS changes
* ESLint to identify JSX and JavaScript errors/problems
* Sourcemaps to help debug JSX JavaScript

I’ll only be covering in detail the JavaScript and JSX parts of this guide. Here’s a look at my project file structure:

{% highlight html %}

├── builds
│   ├── development
│   │   └── src
│   │       ├── css
│   │       ├── images
│   │       ├── js
│   │       └── vendor
│   │   ├── index.html
│   └── process
│       └── jsx
│
├── .gitignore
├── node_modules
├── bower.json
├── gulpfile.js
└── package.json

{% endhighlight %}

…and the package.json file, where I define any gulp dependencies:

{% highlight javascript %}
{
  "name": "weatherApp",
  "version": "1.0.0",
  "author": "Olatunde Owokoniran",
  "description": "This is a description",
  "devDependencies": {
    "browser-sync": "^2.9.6",
    "gulp": "^3.9.0",
    "gulp-babel": "^6.1.2",
    "gulp-concat": "^2.6.0",
    "gulp-newer": "^0.5.1",
    "gulp-plumber": "^1.0.1",
    "gulp-sourcemaps": "^1.5.2",
    "gulp-eslint": "^1.0.0",
    "react": "^0.14.7",
    "react-dom": "^0.14.7"
  }
}
{% endhighlight %}

So am going to assuming that you have npm and gulp installed, run npm install and you should be set.

gulpfile.js
The meat of the setup is in my gulpfile.js file, which looks like the following:

{% highlight javascript %}
var gulp          = require('gulp');
var babel         = require('gulp-babel');
var sourcemaps    = require('gulp-sourcemaps');
var concat        = require('gulp-concat');
var newer         = require('gulp-newer');
var plumber       = require('gulp-plumber');
var browserSync   = require('browser-sync');
var uglify        = require('gulp-uglify');
var pump          = require('pump');

var appSrc = 'builds/development/',
    jsxSrc = 'process/jsx/';

gulp.task('html', function () {
    gulp.src(appSrc + '**/*.html');
});

gulp.task('css', function () {
    gulp.src(appSrc + '**/*.css');
});

gulp.task('concat', function () {
    return gulp
        .src(jsxSrc + '**/*.jsx')
        .pipe(sourcemaps.init())
        .pipe(babel({
            // npm install gulp-babel babel-plugin-transform-react-jsx
            plugins: ['transform-react-jsx']
        }))
        .pipe(concat('weather_app.js'))
        .pipe(sourcemaps.write('.'))
        .pipe(gulp.dest(appSrc + 'js/app/'));
});

gulp.task('copylibs', function () {
    return gulp
        .src([
            'node_modules/react/dist/react.js',
            'node_modules/react-dom/dist/react-dom.js'
        ])
        .pipe(gulp.dest(appSrc + 'js/lib/react'));
});

gulp.task('watch', function () {
    gulp.watch(jsxSrc + '**/*.{js,jsx}', ['concat']);
    gulp.watch(appSrc + 'css/*.css', ['css']);
    gulp.watch(appSrc + '**/*.html', ['html']);
});

gulp.task('browsersync', function () {
    browserSync({
        server: {
            baseDir: appSrc
        },
        open: false,
        online: false,
        notify: false,
    });
});

gulp.task('default', ['browsersync', 'watch', 'copylibs', 'concat']);
}
{% endhighlight %}


Converting JSX to JavaScript with Babel
When building with React, you can write plain JavaScript or in JSX (JavaScript syntax extension). JSX is a preprocessor that gives you a more concise syntax, and is arguably easier and more readable, but needs to be converted to native JavaScript. JSX is analogous to CoffeeScript, even Sass or LESS (but for CSS).

{% highlight javascript %}
// JSX
React.render(
  <h1>Hello, world!</h1>,
  document.getElementById('example')
);

// Native JavaScript
React.render(
  React.createElement('h1', null, 'Hello, world!'),
  document.getElementById('example')
);
{% endhighlight %}


With the help of Babel and its gulp plugin, gulp-babel, you can convert JSX to JavaScript by piping babel() into the concat task, like such:

### Still Learning
I’m only a few days into learning React and this workflow is a result of my early learning stages. I’m sure I have a lot to learn and have yet to find a real-world use case to React.js; feel free to reach out [@hurlatunde](https://twitter.com/hurlatunde/).

