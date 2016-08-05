---
layout: post
title: My take on Template Programming in C++
categories: programming C++
---
So lately I have been doing a lot of C++ programming with heavy usage of
_template_ programming, which is a type of meta/generic programming. Which have
inspired this blog post. Now I am not an expert at all, that would  take years
and this is not a guide to template programming. This is my take on the
advantages and disadvantages.

So let us get started, what does _template_ programming enable you to do? Well
it enables you to make your code dynamic, in the sense that types are first
determined at compile time, and not while you are coding. This means that we
can create methods which can take different kind of types, depending on how it
is invoked.

    template<typename Type>
    class vector
    {
    public:
        vector(uint32_t size);
        vector();

        void push_back(Type item);
        Type pop();
    private:
        uint32_t m_size;
    };

Let us continue based on the code example above, just so we have some common
ground. We have a template of the following structure `template<typename Type>`,
this is a type template which allow a type to be "dynamic" until compile time,
where the type will be set in stone, and then type checking is performed. This
type for of template allows us to create a vector like `auto x = vector<int>();`
or `auto y = vector<double>();`.

We are also able to create templates of variadic length, and based on a pre set
type. But as this is not a guide, we will not dwell on this. But if you are into
C++ programming take a look at here: [cppreference:Template](http://en.cppreference.com/mwiki/index.php?title=Special%3ASearch&search=template&button=)
. Bonus info [cppreference.com](http://en.cppreference.com/w/) is an awesome
reference database for C++ and I use it often.

So what is the advantages and disadvantages with using templates? Well like
all generic programming, it often lessens the amount of code you actually have
to write. For example can these methods using polymorphism

    int add(int x, int y);
    double add(double x, double y);
    float add(float x, float y);
    int add(int x, float y);

Be replace with a single method utilizing templates:

    template<typename TypeOne, typename TypeTwo>
    TypeOne add(TypeOne x, TypeTwo y)

But is this a good idea, to replace a set of type specific functions with a
single template function? In my opinion both yes and no. No because if you are a
newcomer to software development, you need to understand different concepts such
as polymorphism and type compatibility, writing functions with specified types
seems to be a good way to learn both in my opinion. Therefore I suggest
newcomers to actually write out the code, you can always learn tricks for
writing less code. But it is also a good idea, for the experienced developer it
can be quite the advantage to write lesser code and by such become a more
efficient and accomplished programmer.

However in addition to lessen the amount of code, it can also make it hard to
get and overview of a codebase. If you as a developer is not familiar with
template, heck not only templates, generic programming in general it can be
really hard to get an overview over codebase using generic programming. Some
would argue that if code is hard to write, it should be hard to read. I would
argue that if code is hard to read, you as a developer wrote it wrong.

Another disadvantages with template programming is the header only approach. The
functions I have written above, cannot be defined in a `.cpp` file, why I am not
completely certain about, but it is annoying. But why it is annoying, well it is
because it increase compile time. The smallest change in the code of a header
file can/will result in a recompilation of an entire project. Which can take a
lot of time if you are working on a very large project.

So is template programming a go or a no-go? Well after working with it, everyday
for a week I can say that I love it, and would not be without it. I would like
to recommend template programming for non-novice C++ developers.

_-Lars Nielsen_
