---
title: "Load Testing Walkthrough I - Introduction"
description: "Basic idea and common setups about loadtest will be discussed in this post."
pubDate: "Mar 28 2024"
heroImage: "/loadtest.webp"
tags: ["load_testing"]
---

# What is Load Testing
Load Testing is always playing an important role in various testing methods for systems and services, espeically those accepting multiple concurrent connections with requests or data stream sending. And it's about adding load using some tools to the target systems or services to dentermine their scalability and reliability, behaviour to respond, fault tolerance etc to see if they are good enough for production use, if there's any more improvement that could be done, and if any critical errors will occur during peak load. Based on the load, load testing sometime could also be categorized as performance testing, endurance testing and stress testing, which the level of the load that's added to the target goes from normal to extreme.

# How to Start Load Testing
**1. Define your objectives**

*1.1.* What target system are you testing?
 
|target system| 
|--------------|
|database system|
|caching system|
|microservices|
|networking system|
|hardware(CPU/GPU/Disk)|

*1.2* What goals do you want to achieve?
Oftemtimes before running a loadtest, we will find one or more goals, the common ones are:

1. Service Reliability

* Need to ensure at a target number of CCU or at a target maximum rate of connections of requests, only a permissible percent of errors are occuring.

* Need to ensure at a target number of CCU or at a target maximum rate of connections of requestsall critical services and features are functioning properly (as desgined).
 
2. Service Availability

* Need to ensure at a target number of CCU or at a target maximum rate of connections of requests, all or a group of services need to be available for use for a target percent of time period.

3. Service Scalability

* When the CCU or request/connection rate grows, the load on each service instance would be higher and higher, which in metrics is usaully about higher CPU or memory consumption, or higher disk usage if it's for heavy data storage services, more instances need to be added to scale the service up, when scaling up, service reliability and availability need to be ensured. And vice versa with service downscaling.

4. Service Fault Tolerance

* Need to ensure at a target number of CCU or at a target maximum rate of connections of requests, the ratio of critical errors are happening with a low probability lower than a tolerable target number, and the system keeps fucntioning. In a microservice system, some crashes in a microservice cannot lead to sever fault for that service and cannot transmit to other microservice or causing any avalanche.

5. Service Resilence

* Need to ensure at a rapid load changes on the system, it's being able to either adapt to the different load or recover from any crashes rapidly within a allowable time period, and with a tolerable number of data loss. 

6. Service Security

* Need to ensure at a large scale DDoS(Distributed Denial-of-Service) attack, the system is capable to detect, prevent and handle it without impacting the major services.

Based on the system under test (SUT), you can choose different targets to focus on, for some financial services, usually service scalability, sercurity and fault tolerance are the main goals to chase, any errors in the services cannot lead to a fault transaction that causes financial loss, service reliability, resilience is also preferred along with availability.
 
*1.3* How to quantify the testing?

* load testing settings

settings for agents/bots:

| category | example |
|-----------|---------|
|number| how many load test agents/bots are created? |
|frequency| how many requests/connections per sec could one agent/bot send to different endpoints?|
|longevity| how long dose the load test plan to run? |
|load distribution| what percentage of load distribution are given to different nodes/services? |
|change rate| what's the increase/decrease rate of numbers of agents/bots?|

settings for the SUT:

| category | example |
|-----------|---------|
|number| how many nodes are there for testing? Is it auto-scaled? |
|CPU | what's the CPU settings for each node? How many cores are there and if all the cores are going to be used (for paralleling?)? |
|memory | how many memory are assigned for each nodes? |
|disk| how many disk storage are used? |
|system| what operating system is used? |
|other hardware|what network adapter/graphics card is used?|

* load testing goals

under the prime load/a time period's load/target CCU number,

| category | example |
|-----------|---------|
|cpu| all the nodes' cpu usage should be lower than 70% |
|memory| all the nodes' memory usage should be lower than 80%|
|disk| all the disk usages should be lower than 80%|
|time| all the response time should be shorter than 500ms|
|critical error rate| error rate should be lower than 10%, critical error rate should be lower than 1% |
| service downtime | service downtime should be lower than 0.1% |

* load testing metrics

Besides the above goals, other metrics worth checking

|category|example|
|-----------|---------|
|network|byte in/out, latency and jitter, packet loss, retransmission rate etc.|
|non-critical error rate|timeout error, bad request error etc.|
|load balancing | load distributions on services and proxies |
|database | read/write rate, disk I/O, query latencies etc.|
|other statistical metrics | other metrics for user behaviour analysis |
