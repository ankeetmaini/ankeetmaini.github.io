---
layout: post
tags: broccolijs build javascript
---

Broccoli is an awesome building tool, it can build, serve your front end app and save you a lot of headache. **[Source Code] (https://github.com/ankeetmaini/my-broccoli)**

We'll start nice and slow...

We'll be creating the following folder structure in the course of this post. Create a main 'my-broccoli' directory now which will contain everything. Inside **my-broccoli** create a directory js and add three JavaScript files in it. I've just put a console.log statement in each file.

        my-broccoli
        |____Brocfile.js
        |____js
        | |____file-1.js
        | |____file-2.js
        | |____file-3.js
        |____public
        | |____index.html
        |____styles
        | |____css-1.css
        | |____css-2.css

``` javascript
 // file-1.js
 console.log('This is file-1.js');

 // file-2.js
 console.log('This is file-2.js');

 // file-3.js
 console.log('This is file-3.js');
```

Install Node.js, then run the following commands in your shell

``` bash
npm install broccoli-cli
npm install broccoli
npm install broccoli-concat
```
Create **Brocfile.js** at the root of your project. This is the file which does all of the building.

Write the following in the above created Brocfile.js

``` javascript
 // a plugin which concatenates the files
 var concat = require('broccoli-concat');

 var javascripts = concat('js', {
   inputFiles: ['**/*.js'],
   outputFile: '/assets/app.js'
 });

 module.exports = javascripts;
 ```
The above code does a few things.

 - it requires the 'concat' plugin.
 - creates a new tree 'javascripts' by concatenating all the JavaScript files under the folder 'js', which is the first argument of the concat method.
 - the second argument is the options hash, which specifies the input files and the output file.
 - the last line tells the final output of Broccoli, which in this case is the app.js file which should contain the code of all the files in the 'js' directory.

Now switch back to your Terminal, bash for Mac users and Command Prompt for Windows, and type in the following command.

```
broccoli serve
```
Open your browser and point to [http://localhost:4200/assets/app.js] (http://localhost:4200/assets/app.js). You should be able to see the contents of all your JavaScript files concatenated together. This means that broccoli is working :)

This is very simple and probably won't do much good as we've not referenced them in the HTML and may not seem very useful to you. Hold on!

### Levelling up ###
Let's introduce HTML and CSS into the mix.

1. Create a directory 'styles' and add files 'css-1.css, css-2.css' to it.
2. Add the following code to the files above.

    ```css
    /* css-1.css file */
    .one {
    background: 'pink';
    }

    /* css-2.css file */
    .two {
    background: 'blue';
    }
    ```
3. The intention is to combine the css files under 'styles' and build into a single file.
4. At this point of time open your Terminal and run the following command

     ```
     npm install broccoli-merge-trees
     ```
  * up till now we're only exporting the javascripts in our Brocfile.js, since we also need to export the css style tree as well, we need a tool to merge both trees and hence we included the above plugin. We'll use it shortly.

5. Open *Brocfile.js* and add the following lines

     ```javascript
     var mergeTrees = require('broccoli-merge-trees');

     // concatenating all CSS files
     var css = concat('styles', {
     inputFiles: ['**/*.css'],
     outputFile: '/assets/app.css'
     });

     // exporting both JS tree and css as well
     module.exports = mergeTrees([javascripts, css]);
     ```
     * above here we're concatenating the css files and exporting a merge of both JS and CSS instead of just JS earlier.

6. If now you go to [http://localhost:4200/assets/app.css] (http://localhost:4200/assets/app.css), you'll see all the content of files together.

Let's now add an HTML page thereby finishing this app.

### Adding HTML ###
1. Create a 'public' directory and add an 'index.html'
2. Add the following code to it.

    ``` html
    <!DOCTYPE html>
<html>
<head>
  <title>Broccoli Rocks!</title>
  <script src="/assets/app.js"></script>
  <link href="/assets/app.css" rel="stylesheet">
</head>
<body>
  <h1>Sample app to show the powers of Broccoli</h1>
  <hr>
  <h2>Below are two divs, whose styles are defined in different css files. See the source, I'm including just one.</h2>
  <div>
    <div class="one">
      Hey, I'm div#1.
    </div>
    <div class="two">
      Hey, I'm div#2.
    </div>
  </div>
</body>
</html>
    ```
3. Now we need to export this too along with our JavaScripts and CSS files. To do this we just add 'public' to the **mergeTrees()** in our Brocfile.js. As there's no processing to be done on this.

    ``` javascript
    module.exports = mergeTrees([javascripts, css, 'public']);
    ```

4. Now see the browser and you should see your whole app bundled nicely :)
