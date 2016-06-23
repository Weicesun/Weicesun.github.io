---
layout: post
title:  "wechat_design"
date:   2016-06-22  +0800
categories: system
---
Application user sign up sign in, chat, group chat
QPS: 1b user DAU 75% 10 message per user peak QPS 200k
How to verify the user login use session 
Create a session and put session key into user’s cookie then every time a client ask server some information the server will check the cookie’s session and decide whether the user is valid or not.
Friendship table should save in two table since NoSQL do not have multiple index to use. Small to large id one table and large to small id in one table. 
Message service: all the message does not need to modify so NoSQL is better. 
Thread table need owner id, thread id, participates hash, last active date SQL
How to scale message table can auto-increase and thread table need sharding
Speed up the receive message service: use socket to get persistent tcp connection use server to push notification to user. If user is not active in 10 minute we cut the socket connection and free the port. In http connection we probably should need android GCM(google cloud messaging). 
How to support group chat we need another service to keep track of different group’s active user so when someone send out a message first check the corresponding channel table find the online user and then push the message.
Show the online status on facebook you can pull some message after 3-5 second to tell the server you are online.
Read more [wechat] and [whatsapp]

[wechat]: http://www.infoq.com/cn/articles/the-road-of-the-growth-weixin-background
[whatsapp]:   http://highscalability.com/blog/2014/2/26/the-whatsapp-architecture-facebook-bought-for-19-billion.html
