---
layout: post
tags: broccolijs build javascript angularjs angular
---

This post will walk down on how to create an AngularJS front end app with Broccoli. On how to get started with it [please read my previous post.](http://ankeetmaini.github.io/broccolijs/build/javascript/2015/04/04/Setting-up-Broccoli-in-your-JavaScript-project.html).

## [Source Code on Github](https://github.com/ankeetmaini/pro-angular/tree/todo-app) ##

1. Create a folder 'my-angular'.
2. Install the following npm modules

     ```
npm install broccoli
npm install broccoli-concat
npm install broccoli-bower
npm install broccoli-merge-trees
     ```
     * these above plugins help in concatenation of assets, getting bower files and merging different source trees.
3. Add Angular and Bootstrap.

    ```
 bower install angular
 bower install bootstrap
    ```
4. Create a Brocfile.js at the root and add the following code to it.

    ```javascript
    var concat = require('broccoli-concat');
    var bowerDependencies = require('broccoli-bower');
    var mergeTrees = require('broccoli-merge-trees');

    var app = 'app';
    var styles = 'styles';

    // as broccoli-bower returns array of trees
    var sourceTrees = [app, styles].concat(bowerDependencies());

    // creating another tree as the plugins take input
    // a single tree and not array of trees
    var dependencyTree = mergeTrees(sourceTrees);

    // concatenating all js files
    var javascripts = concat(dependencyTree, {
      inputFiles: ['**/*.js'],
      outputFile: '/assets/app.js'
    });

    var css = concat(dependencyTree, {
      inputFiles: ['**/*.css'],
      outputFile: '/assets/app.css'
    });

    // export javascripts, css and public folder
    module.exports = mergeTrees([javascripts, css, 'public']);

    ```

5. You can now go to [http://localhost:4200/assets/app.js](http://localhost:4200/assets/app.js) or [http://localhost:4200/assets/app.css](http://localhost:4200/assets/app.css) to see your concatenated JS file or CSS file.
6. In case you have added an **index.html** in your public directory referencing **/assets/app.js** and **/assets/app.css** you can see the html page at [http://localhost:4200](http://localhost:4200).

That's all for this one. Thanks for stopping by :)
