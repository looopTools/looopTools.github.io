---
layout: post
title:  "Why I do not like JavaScript or rather not exactly JavaScript"
date:   2015-08-27 18:15:00
categories: programming software development
---
I have for the paste 6 weeks been back in the world of JavaScript and will be for a while still. This has reminded me why I did not like JavaScript, and this blog post, will be about why.

Well as some know, I actually have specialisation in web development, and actually did web development for a couple of years. But after a couple of years break, I am using JavaScript again. But why do I not like JavaScript? Well it is not exactly JavaScript, but rather the limitations of using JavaScript.

### Browser based capabilities
When certain features only works in _Google Chrome_, _Mozilla Firefox_, _Apple Safari_ or another browser. It is really frustrating, as it limits a developer in what libraries you as a developer can choose. This is really a problem as it is not always obvious which browsers are supported by a library.

### File System interaction
Now I know JavaScript are designed to run in a "sandbox" within a browser and not have access to the file system, for security reasons.

However I need to have the possibility for sending files from end user to end user. And this results in problems, on the receiving users end, as I cannot decide where to download the file I am sending. And I need to do some really annoying "magic", for uploading images. Also the fact that files are loaded straight into memory BAD CONDUCT in my opinion.

### Multithreading
This is in combination with _Browser based capabilities_. since I use a library which requires access to the windows instance, this makes it impossible for me to do proper Multithreading, as WebWorkers, cannot access the window instances.

### Interpreters and syntax
We have different types of interpreters at our disposal, depending on which browser we use, which is cool enough. Just like using GNU GCC or LLVM Clang, however, these compilers, enforces a certain syntax. However JavaScript interpreters, do not enforces syntax as strictly. This results in the fact that, all the versions of `console.log(string)` below are valid.

    console.log("data");
    console.log('data');
    console.log("data")
    console.log('data')

This makes it close to impossible to enforce a uniform coding style in a project and makes it hopeless to make pretty code.

### Conclusion
Though I do like the syntax of JavaScript, if all developers remembers `;` and keeps same parentheses style guide. The inconveniences mention above, results in JavaScript being one of the few languages I really do not enjoy using, unfortunately.

You will also notice that the only JavaScript used here on the blog, is what comes standard with Jekyll.

I am thinking about learning Dart instead.

_-Lars Nielsen_
