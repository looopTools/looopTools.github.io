---
layout: post
title: "Alexandria - A book management system for private book collections"
date: 2018-12-21 10:00:00
categories: foss bsd-license book-management
---

So for quite some time I have had an issue with my book collection and that problem is simply that it has gotten out of hand. I no longer have a full
overview over what books I have, who have lent what, and what I actually what I thought about all my books.

For some time I tried to use Delicious Library 2 and 3 [[1]][dll] by delicious monster and I have been quite happy with it for a long time. But unfortunately the prices is more than I am willing to pay for what for me essentially was a library system. I looked for open source alternatives, but most was either too complex to use, required custom building of the software, and most required me to have a server running. None of which I was interested at the time. Another issue is that most of the open software solutions out there were developed with the intent of being run in a full library setting, integrating with identification system, I also did not want to use. I did find a solution at one point called _books_ which was all what I wanted but it is unfortunately no longer maintained. I finally ended up using Good Reads [[2]][gdr] started by Otis Chandler and Elizabeth Khuri, now owned by Amazon. However, it has a lot of faults, firstly I couldn't create a account without a Facebook account and the site is extremely slow, it also have a lot of features I never use, and a lot of features I am missing.

Due to the above mentioned reasons I have for a while wanted to implement my own system, and I have from the start wanted to call it Alexandria, after the _Library of Alexandria_. [[3]][lalex] I have started the implementation, dropped it, and started again over and over again. Because I couldn't decide on the correct technologies to use, where my main problem was what to use for the frontend user interface and for the programming language on the backend.

The reasons for my indecision on the programming language for the backend, is that I over the past two to three years have run into so many programming languages that I wanted to learn and try, that I simply could not decide between one I knew or one to learn. One of the longest running contestants have been Rust [[4]][rust], but I simply had to realise that Rust is a programming language of epic proportions, but I simply do not have the time at the moment to learn to use it for more than a system programming language. Another contender was Go [[5]][go], I like the structure of Go and how it feels like C, but does not want to kill you pointers (I like pointers). But I also through my experience at Chocolate Cloud, realised that Go may not be ready for such as system and the way Object Oriented Programming (OOP) is done in Go I don't really like and this is purely from a syntax and structure perspective. As these are just two of the language, you can see that I have had some problems deciding. I have come to the decision using either Ruby [[6]][ruby] or Python [[7]][python]. Most who know me in person, will know that of the programming languages I have ever tried, Ruby will for ever be my greatest love, it is actually one of the reasons this blog uses Jekyll and not Pelican. But that is simply not fair to use as an argument for choosing it for this project. Also I have some experience developing similar systems in Python, so Python makes more sense. So the plan is as follows, use Python until I am done with PhD afterwards I may switch to another language, I may even write a few parts of Alexandria in other languages just to test the out, sound idiotic but HEY! my project. My issue on the frontend is that I do not really know what is good and what is crap, the only thing I know is that I don't really like Angular. However, after reading about different libraries and frameworks, I have come to the conclusion that I will be using Vue.js [[8]][vue]

So what I will be using is _Python_, _Vue.js_, and I will design the system to be usable with multiple database backends.

The system will be developed incremtially and when I have time, and I will release it under either the BSD-3 software license haven't decide yet.

Hope you will follow the development on gitlab [[9]][alex].


_./Lars_



1. [Delicious Library][dll]
1. [Good Reads][gdr]
1. [Library of Alexandria][lalex]
1. [Rust][rust]
1. [Go][go]
1. [Ruby][ruby]
1. [Python][python]
1. [Vue.js][vue]
1. [Alexandria GitLab Account][alex]


[dll]: https://www.delicious-monster.com/ "Delicious Library"
[gdr]: https://www.goodreads.com/ "Good Reads"
[lalex]: https://en.wikipedia.org/wiki/Library_of_Alexandria "Library of Alexandria"
[rust]: https://www.rust-lang.org/ "Rust"
[go]: https://golang.org/ "Go"
[ruby]: https://www.ruby-lang.org/en/ "Ruby"
[python]: https://www.python.org/ "Python"
[vue]: https://vuejs.org/ "Vue.js"
[alex]: https://gitlab.com/looopTools/alexandria "Alexandria GitLab Account"
