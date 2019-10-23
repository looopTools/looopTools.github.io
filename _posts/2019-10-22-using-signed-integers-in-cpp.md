---
layout: post
title: "Using signed and unsigned integers in C++"
categories: [C++, programming]
---

I am going to start writing a bit more about C++ as it is the programming language I spend the most time with and I may have some insights that can help others.
This post will cover when to use signed and unsigned integers, and why you mostly should use the later. 

## Notation 

- A number written $n\_{d}$ is a number in decimal 
- A number written $n\_{b}$ is a number in binary 
- A number with out any of the above is in decimal 

# What is signed and unsigned integers 

So first, what is an integer? An integer is a natural number, and it can be both be negative or positive and negative.
We distinguish between positive natural numbers ($N^{+}$) and negative natural numbers ($N^{-}$) by saying that a number $n \in N^{+}$ is any $n$ in the set $[0, \infty^{+}]$ and $n \in N^{-}$ if $n$ is in the set $[-1, \infty^{-1}]$.
__NOTE:__ In computer science we include $0$ in $N^{+}$ that is not always true in mathematics

However, in computers, we cannot represent all the numbers to $\infty$, but we can represent a subset of the numbers. 
In a computer, we use the bits to represent numbers by combining multiple bits into bytes and setting the individual bit to either $0$ or $1$. 
If we say that we have $8$ bits or $1$ byte, we have $2^{8} = 256$ possible combinations of bits of $1$'s and $0$'s.
However, how do we know if a number is negative or positive? 
Well, enter two's complement numbers.
A number in two's complement can be negative or positive, and most often, the left-most bit determines if a number is negative or positive, if it is $1$ it is negative. 
I will use the example from [[1]](https://www.cs.cornell.edu/~tomf/notes/cps104/twoscomp.html).
If we want to represent the number $-28\_{d}$, in two's complement, using $1$ byte, we do the following: 1) Write the number $28\_{d}$ which is $00011100\_{b}$ 2) Swap all $0$'s with $1$'s and vice versa, giving us $11100011\_{b}$ 3) Add $1$ which gives us $11100100\_{b}$ and this represents $-28_{d}$ in two's complement. 

Now the observant reader, would note that if we use the left most bit to represent a number is negative, means any $n >= 128$ cannot be expressed in two's complement as $128\_{d}$ in $1$ byte is represented as $10000000\_{b}$.
So that puts a limit to the number of numbers we can represent. 
We can represent any positive number $n^{+} < 128$ including 0. 
Now recall that our options of possible combinations in $256$ and $\frac{256}{2} = 128$, that our $N^{+}$ using $1$ byte for number representation is the set$[0, (\frac{256}{2} - 1)]$.
That leaves us with $128$ combinations for negative numbers So we can say that $N^{-1}$ is the set $[-1, -128]$. 
We can write this as:

\begin{equation}
N^{+} = [1, (\frac{2^{8}}{2} -1)] \wedge N^{-} = [-1, -\frac{2^8}{2}]
\end{equation}

We make this general, if we say that we $w$ bits, above $w = 8$ to represent our numbers, then we $2^w$ different bit patterns. This means that we can say that for two's complement we have 

\begin{equation}
N^{+}\_{w} = [1, (\frac{2^{w}}{2} -1)] \wedge N^{-}\_{w} = [-1, -\frac{2^w}{2}]
\end{equation}

So now that we have that figured out, let us moved on to signed vs unsigned numbers. 

## Signed Integers

A signed integer is an integer in two's complement and using the leftmost bit to determine if $n \in N^{+}$ or $n \in N^{-}$ is called signing. 
However, $w$ varies depending on the system architecture, but in general we say that the data type `int` has $w = 32$ and `long` has $w=64$. 
However, trouble, I did write _in general_. The problem is that some systems restrict representation to word size, meaning on a $16$-bit system $w$ for both `int` and `long` could be `16`.
_Note:_ To keep up with the C++ standard systems should conform to what is shown in the type table presented in [[2]](https://en.cppreference.com/w/cpp/language/types).
This causes some confusion and therefore C++ comes to the rescue with the header `<cstdint>` which defines the data type `int8_t`, `int16_t`, `int32_t`, and `int64_t` where the number `Y` in `intY_t` is $w$, so for `int8_t` $w = 8$.
The side benefit of having an exact $w$ is also that you know exactly how many bits your variable will take. 
One problem is though that not all compilers support this header as the architecture they support does not support these integers. 

So when to use `int`/`long` vs `intY_t`? Well, you use `intY_t` when you want to know precisely how many bytes you will need and if you know that your variables do not go outside the bounds of $N^{+}\_{w}$ and $N^{-}\_{w}$. So that is what a signed integer is. 

## Unsigned Integers

Some times we do not like negative numbers and some times we do not want to care about them at all, and that is when unsigned integers come into play. 
Because, with unsigned integers, we can only represent numbers in $N^{+}$ and since we do not care about negative numbers we now have all $2^w$ bit patterns available for numbers, meaning we can represent large positive numbers. 
For unsigned numbers our $N^{+}$ is the set $[0, (2^{w} -1 )]$, the $-1$ is due to one pattern is used to represent $0$.

C++ provides `unsigned int` and `unsigned long`, but again $w$ can vary based on the system. 
But as for signed integers, C++ provides `uint8_t`, `uint16_t`, `uint32_t`, and `uint64_t` via the `<cstdint>` header, and they have the same properties as their unsigned counterparts and the same use cases. 

So now we have signed and unsigned integer. When do we use what then?

# When to use Signed or Unsigned Integers?

It is straightforward only use signed integers when you negative numbers, otherwise use unsigned.
Why do I say that? 
First using unsigned integers removes the need to investigate if the statement`var < 0` is true.
I see a lot of people using the signed data types "polluting" their code with some way to check if a number is negative, even though it is never expected to be. 
This can be avoided by using unsigned integers as the number never will be negative. 
Secondly, consider the following C++ code iterating a list by index:

```c++
std::vector<std::string> collection(20);
for (int i = 0; i < collection.size(); ++i)
{
    collection[i] = std::to_string(i);
}
```

Why is the variable `i` an `int`?
It does not need to be.
Also, why are we comparing a signed integer to an unsigned? 
The `std::vector<T,Allocator>::size` [[3]](https://en.cppreference.com/w/cpp/container/vector/size) method returns a value of `std::size_t` [[4]](https://en.cppreference.com/w/cpp/types/size_t) which is an unsigned integer.
It will not cause compiler or run-time errors. It is just weird to do unless needed.
So instead we know that `collection.size()` returns a `size_t` and that it is an unsigned integer, why not use the same data type then and transform our code to:

```c++
std::vector<std::string> collection(20);
for (size_t i = 0; i < collection.size(); ++i)
{
    collection[i] = std::to_string(i);
}
```
__NOTE:__ Fun fact it is generally recommended to use unsigned numbers for indexing as you rarely have a negative index. 

So we are done, right? 
Now we know when to use signed and unsigned integers?
Well yes, but I would like to plant some seeds in the mind of all developers who do not think about this already. 
Recall the data types with `intY_t` and `uintY_y` or even types I have mentioned yet, like `short`. 
Why are we not using them all the time? 
So from the table showing type size presented in [[4]](https://en.cppreference.com/w/cpp/language/types), we can see that an `int` is at least $16$-bit or $2$ bytes wide. 
If we assume a system where an `int` is has $w = 16$ and we have two constants `x = 128` and `y = 255` and both of the type `int`.
then we spend $4$ bytes for both variables. 
If instead `int` has a $w = 32$, we would have spent $8$ bytes.
Now, why am I bring this up?
Well, `x` and `y` are constants.
Both are not exceeding a value of `255`, which means they can be represented in a type where $w = 8$, right?
What if we swapped to use, let us say `uint8_t` instead of `int`, then combined `x` and `y` would use $2$ bytes. 
For `int` with $w=16$, that means we have reduced the memory consumption, roughly, by half using `uint8_t`, and for `w=32` we have reduced it with $\frac{3}{4}$.
Now that may not sound like a lot, but let us say it this way what if we have $1000$ variables of type $int$ on a $32$-bit system with $w=32$. 
Then we would use roughly $3.9$kB of memory to keep the integers in memory. 
But what if, let us say half of those variables could be represented in 'uint16_t'?
Then we would have used $(500 \cdot 32) + (500 \cdot 16)$ bit representing them all which results in $2.9$kB which is a reduction of $1.34$x. 
Now imagine you applied that to all variables, where possible, in a huge software solution.
How many MB and potentially even GB of memory could you save, just by using reasonable data types?
I know writing about kB may not be the best example, bu the $1.34$x should give you an incitement to use more suitable data types. 
I am also aware that we have "unlimited" memory, but why not code, so you have system resource for the more challenging stuff?

I hope you liked this post. I will write more about C++ and C in the future. 

_./Lars_
# References 

- [1] [Finley T. Two's Complement](https://www.cs.cornell.edu/~tomf/notes/cps104/twoscomp.html)
- [2] [cppreference Types](https://en.cppreference.com/w/cpp/language/types)
- [3] [cppreference std::vector<T,Allocator>::size](https://en.cppreference.com/w/cpp/container/vector/size)
- [4] [cppreference std::size_t](https://en.cppreference.com/w/cpp/types/size_t)
