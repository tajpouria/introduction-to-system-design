## What is a distributed system

Let's start by answering this question, What is a distributed system?

A distributed system is a system whose components are located on different networked computers, which communicate and coordinate their actions by passing messages to one another from any system The components interact with one another to achieve a common goal.

There are huge use cases for distributed systems in the computing industry and it is widely used in tech companies. But here's the thing, they don't make such complicated systems for fun! I bet if there was a magic computer that could handle tons of heavy calculations instantly and respond to the requests all around the world without latency and downtime, they deploy the entire system on that machine, but unfortunately, that's not the case in the real world! All I try to say is that we need to keep the system as simple as possible and only make changes when that is necessary.

There are some characteristics that architectures not thinking about when creating small scale stuff, but it becomes an issue when you working with distributed systems here's some fallacies about the distributed systems:

- The network is reliable: When the entire system runs a single node network issues between components doesn't make sense, but when you got thousands of services that each one runs on an independent machine and constantly talking to each other, the network will often break at some point.
- Latency is zero: Not true, you gonna have latency between those machines
- Bandwidth is infinite: When you moving data around on all those different servers that will become an issue
- Topology doesn't change: In a real system constantly some components go down and others brought up
  Network is secure
- Only one administrator: There is gonna be multiple people working on a system and potentially changing it
- The cost of moving data is zero

Distributed system characteristics:

- Concurrency and consistency of components
- Lack of a global clock
- Independent failure of components
- Shared resources

Communication issues that happen on a distributed system more often:

- The client can't find the server
- Server crash mid request
- The server handles the request but the response is lost
- Client crashes

Benefits that come with distributed systems:

- More release, fault-tolerant
- Horizontal scalability
- Lower latency increased performance
- Cost-effective
