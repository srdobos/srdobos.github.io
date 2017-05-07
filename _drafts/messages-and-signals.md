---
layout:post
title: Messages and Signals
---

React to signals
Respond to messages

Each subscriber to a message queue has its own read head and tail.
Subscribers increment their read head when they "dequeue" a message.
Messages are removed from the queue only when all subscribers tails have surpassed its value.

