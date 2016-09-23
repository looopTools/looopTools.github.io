---
layout: post
title: Why using immutable restriction in programming is good
categories: programming
---

I have developed software libraries for some years now and part of that have been learning to designing
API's for idiots. What I mean with that is; People with gladly use a software library without reading
the full documentation for it, and then when do something which the API was never intend for. They
complain that it is not acting as it is supposed to. One of the things I have experienced are people
whom either expect and object to change or not change if it is parsed to a function or procedure.
Therefore if either happens, they think the library is broken and needs to be fixed. This often happens
when a user have not read the documentation for a function they are using. I found that a way to actually
avoid this is by applying a restriction on the input given to a function. This is the restriction of saying
this will not change or this is constant. Effectively making a object immutable, for a given function or
and entire application.

So what does this mean? Well before we get started let me explain the concept of constant. I will base
this in C++ but it can be applied in C#, Java and such, but it might need the application of other keywords.
For instance in C# it is `sealed` and `readonly`. Now back to C++, in C++ we have two usages of constant I will explain
but both using the keyword 'const'. One is the application of making a variable immutable by applying the `const` keyword
when we declare the variable.

    const int x = 10;

Let us break down, we have a integer x, x is 10 and it is constant 10. What this means is that x will ALWAYS be 10
and it cannot be changed. Therefore if yourself or another developer uses x, you can always be certain that it is
10. This is very neat as there will be no confusion, when testing and function and its results. It also ensures
that there are no discussion when you have to determine the value of variable.

The second usage of ´const´ is function based immutability. Just to emphasis I will show a function signature;

    float avg(const int[] data, const int size);

What we have is the function signature for method calculating the average of integer values in an array. As you
can see, I have applied the 'const' keyword to both data and size. This is to tell the user of the function that
in the function ´avg´ we will never change either data nor size. Emphasising to the user that if he/she uses this
function, the content of data and size will not change and are in good hands.

There is a third option of using `const` in C++, but I have never actively used it myself, but it is used to
explicitly tell that a function cannot change member variables of a class and are only applicable when doing object
oriented programming
