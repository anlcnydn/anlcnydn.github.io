---
layout: post
title: Introduction to RabbitMQ
desc: Aim of this post is to record and share things, that I learned from the hard way, in a tidy manner.   
keywords: "messaging,rabbitmq,rabbit-mq,amqp,AMQP,broker,message-broker"
date: 2017-12-21
categories: [Mobile]
tags: [messaging, rabbitmq, rabbit-mq, amqp, AMQP, broker, message-broker]
icon: fa-bookmark-o
---

[//]: <> (This is also a comment.)

> Messaging or message queuing is a style of communication between applications or components that 
> enables a loosely coupled architecture.

[RabbitMQ](https://www.rabbitmq.com/) is one of the most powerful and widely used message brokers, 
which enables to design and develop loosely coupled, scalable and distributed applications. Not only
for its popularity, but also it is used by the company that I work for(it means that there is a 
possiblity to encounter with a problem related to RabbitMQ and solving this problem requires at 
least a base level knowledge); I decided to refresh what I know and push my limits harder to gain 
more advanced knowledge about it. This post and the posts that will be added later with similar tags
will be compilations of underlined sentences and handwritten notes from my readings while studying 
RabbitMQ. I have started with [this](http://files.hii-tech.com/book/rabbitmq/RabbitMQ%20Essentials.pdf) 
book, so if you cannot persuade yourself to a sentence you have read belongs to me, definitely it is 
from the book. So, lets hit it.

<div style="text-align:center"><img src ="http://anilcanaydin.com/static/img/posts/one-way-queue.png" style="width: 50%; height: 50%" /></div>

In the above scheme, commonly referred to as messaging or message queuing, systems play the role of 
message publishers (producers) and message consumers. They publish a message to a broker on which 
they rely on to deliver it to the intended consumer. If a response is required, it will eventually 
come at some point on time through the same mechanism, but reversed (the consumer and producer 
roles will be swapped).

## A loosely coupled architecture

<div style="text-align:center"><img src ="http://anilcanaydin.com/static/img/posts/loosely-coupled.png" style="width: 50%; height: 50%" /></div>

From the above architecture of a loosely coupled system followings can be deduced:   
* The publishers or consumers fail without impacting each other

* The performance of each side to leave the other side unaffected

* The number of instances of publishers and consumers to grow and reduce and to accommodate their 
workload in complete independence

* The publishers are unaware of the location and technology of the consumers and vice-versa

> The main downside of this approach is that programmers cannot rely on the mental model of procedural 
> programming where things immediately happen __one after another__. In messaging, things happen 
> over time, so systems must be programmed to deal with it.

## Cores of AMQP

__Broker__: This is a middleware application that can receive messages produced by publishers and 
deliver them to consumers or to another broker.

__Virtual host__: This is a virtual division in a broker that allows the segregation of publishers, 
consumers, and all the AMQP constructs they depend upon, usually for security reasons (such as 
multitenancy).

__Connection__: This is a physical network (TCP) connection between a publisher/consumer and a 
broker. The connection only closes on client disconnection or in the case of a network or broker 
failure.

__Channel__: This is a logical connection between a publisher/consumer and a broker. Multiple 
channels can be established within a single connection.

__Exchange__: This is the initial destination for all published messages and the entity in charge 
of applying routing rules for these messages to reach their destinations. Routing rules include the 
following: direct (point-to-point), topic (publish-subscribe) and fanout (multicast).

__Queue__: This is the final destination for messages ready to be consumed. 

__Binding__: This is a virtual connection between an exchange and a queue that enables messages to 
flow from the former to the latter. A __routing key__ can be associated with a binding in relation 
to the exchange routing rule.

> Each message delivered to an exchange first, to a queue at last.

Following figure is an overview of concepts defined above.

<div style="text-align:center"><img src ="http://anilcanaydin.com/static/img/posts/overview-of-concepts.png" style="width: 50%; height: 50%"/></div>

## The RabbitMQ broker

RabbitMQ is an Erlang implementation of an AMQP broker. Erlang has been chosen to build it because 
of its intrinsic support for building highly-reliable and distributed applications. 
Indeed, it is used to run telecommunication switches for which a proverbial total system's 
availability of 9 nines has been reported (__that's 32 milliseconds of downtime per year__). 
Erlang is also able to run on any operating system.

Apparent use cases for RabbitMQ can be multilingual, distributed micro-service architectures. 


## References: 

Dossot, D., "RabbitMQ Essentials", Packt Publishing, 2014














