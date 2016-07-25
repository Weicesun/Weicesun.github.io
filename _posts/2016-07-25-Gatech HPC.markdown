---
layout: post
title:  "Gatech HPC course note"
date:   2016-07-25 +0800
categories: Course
---

#lecture1

##The multithread model  DAG

Direct acyclic graph is a collection of vertices and directed edge. The final result of these connections is that there is no way to start at some vertex ‘A’, follow a sequence of vertices along directed paths, and end up back at ‘A’. DAG can be used to modeling data flow that flows in constant direction through a metwork of processors.

Each vertex is an operation and directed edge show how operations depend on each other. 'Sink' is depend on the the 'source'.

Cost model assuptions: 
[1]All the processors ran at the same speed. 
[2]1 operation = 1 unit of time 
[3]edges do not have any cost associated with them.

Work and span 
Work = number of vertices in the DAG
Span = longest path through the DAG = D(n) also known as _critical_ _path_

W(n)/D(n) is the average avaliable parallelism in the DAG
Span Law → Tp(n) => D(n)
Work Law → Tp(n) => ceiling of W(n)/P

##Brent's Theorem 
It derives the upper and lower bond of the time consume to finish the task.

## Speed up, work optimality and weak scaling

Speed up is best sequential time / parallel time
The speed up grow linearly is the goal to achieve this the work of the parallel algorithm should match the best sequential algorithm and the work per processor should grow as a function of n.




