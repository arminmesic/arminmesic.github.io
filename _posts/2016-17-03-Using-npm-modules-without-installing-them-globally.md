---
layout: post
title:  "Using npm modules without installing them globally"
date:   2016-03-17
categories: 
    - JavaScript
    - Node
    - Npm
---

So I've installed a new OS and I wanted to start working on a JavaScript project. I did my npm install
wanted to launch my gulp task, but I didn't had it globally installed I really didn't want to fill up my newly installed OS 
with global modules. There's a solution where you can use your global modules without installing them through `npm install -g MODULE_NAME`

### How to use 'global' modules without installing them globally

1. `npm init` your folder to get your `package.json`

2. Install your global modules without the `-g` flag, e.g. `npm install gulp ---save-dev`

3. Install your gulp modules and create your `gulpfile.js`, in this example I'll just use browser-sync

    `npm install browser-sync --save-dev`

    ```
    Gulpfile.js

        // load module
        var gulp        = require('gulp');
        var browserSync = require('browser-sync').create();

        // reload task
        gulp.task('bs-reload',function() {
            return browserSync.reload();
        });

        gulp.task('serve', function() {

            // Serve my files localhost:3000, for this example I'm just serving
            // a index.html
            browserSync.init();

            // Listen for changes to compile and reload
            gulp.watch(['*.html']).on('change', browserSync.reload);

        });
    ```
4. Open `package.json` and add the following

    ```
        "name": "test",
        ...
        "scripts": {
            "serve": "gulp serve" // Just enter the command you would usually enter inside your terminal
        },
        "author": "",
        ...
    ```

5. Execute `npm run serve`, this will launch gulp without the need to install it globally.

### How it works

When you install npm modules, they're automatically saved inside `node_modules/.bin` and
npm script uses them if they're not able to find modules globally.

You could also start gulp through `./node_modules/.bin/gulp serve`. 

### But what about bower

You don't really want to use `./node_modules/.bin/bower install SOME_LIBRARY --save` every time you need to 
add new dependencies. Just switch to npm for dependency management, it has the same things that bower has.

### Conclusion

Using the modules this way makes it easier to get up and running with a new project, you just need `npm install`
and everything you need should be installed.

This is just a small example to show the general principle this can be extended and your npm scripts 
can take care of minification of your assets, creating your build, committing and pushing changes to Github.