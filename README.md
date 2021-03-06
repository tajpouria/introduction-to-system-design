# Introduction To System Design

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

## Performance metrics for system design:

- Scalability: Bad design can introduce some set of bottlenecks for scaling a system and it affects the volume of the data or the number of requests that a system can handle. In other words, we should be able to scale a system with a minimum amount of performance loss
- Reliability: An arbitrary indicator for this factor could be measuring the mean time between failures: `MTBF = (Total elapsed time - Total downtime) / number of failures`, in this case, bigger MTBFs designate the more sustainable system
- Availability: A poorly design system not going to available from time to time, a simple way to calculate availability is: `Availability time = (Overall available time / Whole-time) * 100`, You can compensate for more availability by increasing the redundancy. 99.999% available system is kinda bottom line of industry-standard and it is equivalent to 5 minutes and 15 seconds down time in one year:

<a href="https://imgbb.com/"><img src="https://i.ibb.co/RD0wyYg/audin59table.png" alt="audin59table" border="0"></a>

Reliable vs available:
A reliable system is always an available system
Availability can be maintained by redundancy, but the system may not be reliable
You can think of an airplane to compare this to factor if the airplane needs maintenance it could be replaced with another one and the service going to be always available but for the plane, one thing that you wanna do is to make sure plane is always reliable cuz once that plane's in the air you do not want a failure.

- Efficiency: Describes how efficient a system perform, often used metrics are system latency and throughput

- Manageability: Examples of the factors that impact system manageability are: Observability, the ability to be able to spot a bug or track a certain action, Speed and difficulty that involves maintaining the system, Difficulty of deploying the updates, etc.

## Quick math for capacity estimates

Here's an example data access latency in compare to each other:

<a href="https://ibb.co/2kRr93V"><img src="https://i.ibb.co/71BDftM/Screenshot-from-2021-03-27-10-09-00.png" alt="Screenshot-from-2021-03-27-10-09-00" border="0"></a>

Latency key takeaways:

- Avoid network call as much as possible by storing frequently accessed data locally
- Replicate data across multiple data center for disaster reconvey as well as improving performance
- Use CDNs to reduce latency
- Keep frequently accessed data in the memory if that's possible instead of seeking from disk

Basic conversions:

- 8 bit = 1 byte, 1024 byte = 1 kilobyte, 1025 kilobyte = 1 megabyte, 1024 megabyte = 1 gigabyte, 1024 gigabyte = 1 terabyte
- Char = 1 bytes, Integer = 4 bytes, UNIX timestamp = 4 bytes
- 60 seconds \* 60 minutes = 3_600 seconds per hour, 3_600 seconds \* 25 hours = 86_400 seconds per day, 86_400 seconds \* 30 days = 2_500_000 seconds per month

Estimation example: Let's say we've we need a photo hosting system with 10 million daily active user, which in average every day each user reads 30 photo and writes 1 photo.

Traffic:

- 10 million daily active user \* 30 photo read per day = 300 million photo read per day
- 10 million daily active user \* 1 photo write per day = 10 million photo write per day

=>

- 300 million photo read per day / 86_400 seconds per day ~= 3472 photo read per seconds
- 10 million photo write per day / 86_400 seconds per day ~= 115 photo write per seconds

Memory:

- (300 million photo read per day \* 500 byte each photo size) / 1024\*\*3 (to gigabyte) ~= 150 gigabyte
- 150 gigabyte \* 0.2 (Based on the 80-20 rule only 20% percent of the photos needs to be highly accessible) ~= 30 gigabyte
- 50 gigabyte \* 3 replication ~= 90 gigabyte

Bandwidth:

- (300 million photo read per day \* 1.5 megabyte each request size) / 1024 (to gigabyte) ~= 450_000 gigabyte
- 450_000 gigabyte / 86_400 seconds per day = 5.2 gigabyte per second (In the real world, rarely applications going experience a steady flow with the same rate, instead there's going to be a lot of peaks)

Storage:

- (10 million photo write per day \* 1.5 megabyte each photo) / 1024\*\*2 = 15 terabytes per day
- 15 terabytes \* 365 days each year \* 10 years = 55 petabyte each ten years

## Horizontal vs vertical scaling
