---
layout: post
title:  "Talk about some basic idea about photo sharing system"
date:   2016-07-21 +0800
categories: system
---

When we design a system it is more important to get something done than make it perfect.

After we complete a system we can improve it by consider avaliability, scaliability, performance, reliability.

#Basic version

The basic system should have two function the upload storage function and the RESTFUL API query to get the certain image function. CDN (Content deliver network) is needed since it can make the content closer to the user. It can provide faster performance. Building a simple version of software on a single server will be trivial.

#Scalable version

When it comes to large scale we need to separate the service to get decouple the functions. In this case, it is image write service and image retrival service. The problem is that the write process is slow and the _Apache_ and lighttpd can only allow some numbers of cuncurrent connections.

To deal with concurrency, we can shard the users' visits by user id and we can make more replicate server to prevent the server from failing. And the image file should be store in file system like GFS.

When to deal with fast access we can also add cache and load balancer. However load balancer may increase the cahce miss. We can use distributed cache and globle cache to deal with this problem. When we design tiny url we should have known that the request should encount the same cache.

Proxy can also decrease the response time. A proxy can filter request log request and sometimes transform request. Proxy server can clapse the result and return the response to the server. 

