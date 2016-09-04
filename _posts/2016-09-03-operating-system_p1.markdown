---
layout: post
title:  "Advanced Operating System"
date:   2016-09-03 +0800
categories: course
---

# Some class note

This is gatech advanced operating system note. I write some core idea about this course this is part 1.

For the operating system architecture there are two model monolithic model and microkernal model. Monolithic model focus on performance and microkernal model focus on portability. Because the microkernal first model mach which is developed by CMU has bad performance following microkernal like spin and exokernal all can't improve the performance of the operating system. 

## Microkernal based 

All of operating system services run at the same privilege level as user-level applications. All of them in their own individual address spaces. And only the microkernel runs at a different level of privilege provided by the processor architecture. Since all of the service of OS is running on the kernal when they need to cooperate with others they need a lot of communication. 

The mainly reason for this architecture lose performance is that there are many broad crossing, The explicit cost is the fact that from an application which is at a particular protection level, namely the user level protection level of the processor architecture. 

## L3 microkernal

To solve the problem of microkernal, L3 microkernal says that we need to provide abstraction of address space, threads, inter-process communication, and UID which are often needed for the operating system. 

To solve the problem we need to figure out the reason of this porblem. Reason one: broad crossing Reason two: address switching. Reason three: the cost for doing thread switches. L3 solve these problem by reduce the cycles to 123. For CMU mach version it took 900 cycles to do the same thing. What makes this thing happen? The reason is that L3's design priority is different from Mach. To deal with address switch we need to avoid TLB flush. There are so called address space tag TLBs which contain the process ID for which a particular TLB entry is present in the TLB. MIPS Architecture for instance uses address space tagged TLBs. But on the other hand, an architecture may not use an address space tagged TLB. For architecture that has address base tag we can help the tlb avoid being flushed. For those that do not have address based tag. If we do not have these tag we can take advantage of segment, it is also hardware that can help preserve warm TLB.

When the protection domain is very large TLB flush can not be avoid at that time we need to use cache to help us. For soling IPC problem L3 solve it by construction, L3 debunks that myth that microkernel based OL structure is going to be more expensive for thread switching compared to SPIN or exokernel or even a monolithic operating system.