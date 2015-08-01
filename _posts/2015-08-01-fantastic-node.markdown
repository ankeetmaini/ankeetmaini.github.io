---
layout: post
tags: node nodejs
---

# **This is a WIP**. I will update this as I'll read more and find time.

_The content is not my own, but taken from various books, blogs and internet which I do not own. I'll try to add the references some day. These are meant to be quick-brush-up-notes_

## Node, NPM trivia ##

- Node works in two ways local and global. Default is local, and if you installed a package globally Node will do that in `/usr/local/lib/node_modules`
  - local ```npm install webpack```
  - global ```npm install -g webpack```
- A locally installed module will take priority over globally installed one.
- Since JavaScript was designed for browsers, you can't handle binary data easily with it. Node thus has `Buffers` to account for file uploads, database access and binary data handling.

## Buffers ##

- Creating Buffers

```
var buffer = new Buffer('Hey there!');
console.log('Buffer contents: ', buffer.toString());
```

## File Handling ##
