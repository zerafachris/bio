---
title: "Simulating a queue in a post office"
tags:
  - MLOps
  - Productionisation
  - API
link: https://github.com/zerafachris/playGround/blob/master/published/Queueing/README.md
---


This article presents a simulation of a queue system at a post office where customers arrive randomly, wait to be served by one of two clerks, and have a chance to leave the queue or complete their business. The simulation runs for one year, tracking various aspects of the process, including customer arrival rates, the percentage of customers who leave without being served, and the idle time of the clerks. 

Key points of the simulation: 
- **Arrival Rate:** There is a 60% chance of a new customer arriving every minute
- **Service Completion:** A customer being served has a 25% chance of completing their transaction each minute
- **Queue Dynamics:** Customers in the queue have a 5% chance of leaving each minute
- **Clerk Behavior:** If a clerk is free and there’s a customer in the queue, they take the next customer in line. 

The simulation results highlight the average time customers spend in the post office, the percentage of customers who leave without service, and the percentage of time clerks are idle. The data is visualized in a plot illustrating the queue length, people leaving, and customers who completed their business over time. The simulation demonstrates the complexity of queue management in service environments and provides insights into optimizing resource allocation to reduce customer wait times and clerk idle times.
