---
layout: post
title: "[dDOS part 1] Introduction to dDOS"
date: 2018-06-18 12:04:30
categories: security hacking attack
---

So for a while I have wanted to focus on cyber/computer security from the attackers
perspective and how to implement certain types of attacks. This first guide will focus
on dDOS attack, the theory behind, a stupid attack implementation and a smarter way of
executing an attack.

Now for reasons which should be obvious, I will have to state that these guides are
purely for academic and informative purposes and the techniques presented can/will
results in lawsuits against you and your associates if used outside the law. I hold
no responsibility for your usage of the knowledge, that you obtain through these guides
and associated source code.

# Distributed Denial of Service Attack (dDOS)

So first let us start with the base a attack a _denial of service attack (DOS)_, what we want
to achieve is to ensure that no data can be transmitted from a server serving a service
and essentially also blocking data from being transmitted to that server, though the later
is not the main goal.

![base denial of service]({{ "blog.h4xcode.dk/assets/images/ddos/intro/figure_1.png"}})

So how can we achieve what we want? If we start by looking at the channels of the internet
as sucking straws, only a limited amount of water molecules can run through the straw at
a time. The same goes for data packets, what we send through the network, only a limited amount
of data packets can be handle by the channels at a time. Remember, this is from a very abstract
perspective, though illustrative.

So what happens if we force more water into the straw than it can handle, it overflows, thus
blogging the entrance of water which should go into the straw. Now the approach of a DOS attack
is the same, we overflow the network channel with so many data packets, that not all can parse
through and we attempt to make it our packages which goes through the channel such that "real"
data packets does not. Thereby, we block the access to the services, as shown in figure 2. Thus
our packets overflow the network such that "normal packets" cannot reach their destination.

![base denial of service]({{ "blog.h4xcode.dk/assets/images/ddos/intro/figure_2.png" }})

This is the essence of a DOS attack and also a _distributed denial of service (dDOS)_ attack.

So the first _d_ the distributed part when does this come into play? Well in the old days of the
internet and other large public networks could a single machine or node of machines be used to
take down a service. However, as servers became more powerful and new defence techniques was invented
and used, it became increasingly difficult to execute a successful DOS attack. So how do we overcome
these obstacles? Well we increase our resource, we do this by utilise multiple machines and nodes
of machines locate anywhere in the world. This increase how many data packets we can "throw" at
the server we want to deny access to, as shown in figure 3.

![base denial of service]({{ "blog.h4xcode.dk/assets/images/ddos/intro/figure_3.png"}})

Thus achieving the same result as a DOS attack, just with multiple collaborating attackers. Here we see
machines as individual attackers. Thus, assuming all our attackers have the same resources available, same
network bandwidth, and is configured in the same way. We can assume a linear increase in data packets, we can
throw at the server, with each added attacker machine.

This is a very abstract view on the theory behind a dDOS attack and how it is execute. The next step will be to
implement a program which can actually perform such an attack. This will be the next part of the these guides.

Hope you enjoyed this basic introduction to dDOS.

_-Lars Nielsen_
