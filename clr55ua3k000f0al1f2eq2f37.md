---
title: "What is Vertical Scaling? 🤔"
seoTitle: "A Beginner's Guide to Vertical Scaling"
seoDescription: "Explore the world of Vertical Scaling with my latest blog. Uncover the advantages and disadvantages, and discover scenarios where it is useful."
datePublished: Mon Jan 08 2024 16:51:50 GMT+0000 (Coordinated Universal Time)
cuid: clr55ua3k000f0al1f2eq2f37
slug: what-is-vertical-scaling
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704731211769/84928a2b-af34-4f6b-b428-188ea577f086.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1704732535897/e1922c8a-142b-4f24-82d8-1f1555f7e382.png
tags: scaling, software-development, software-engineering, system-design, vertical-scaling

---

Before diving into **vertical scaling**, let's first discuss what actually we mean by **"scaling"**.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">In the context of software engineering, <strong>scaling</strong> refers to the process of increasing the size or capacity of a system to accomodate changing workloads. It involves optimizing the infrastructure to handle increased workload, ensuring the system remains responsive, reliable and efficient as demand fluctuates.</div>
</div>

### **Vertical Scaling**

Suppose we have developed a web server for a cool project. Initially, the traffic was steady and manageable. Users were enjoying the features, and everything was running smoothly. However, one fine day, our project went viral on social media, and suddenly, the traffic spiked to unprecedented levels. The server struggled to handle this massive influx of users.

In response to this unexpected surge in traffic, a straightforward solution is to increase the processing power of the server so that it can handle this increased traffic. This increase in processing power is called **"Vertical Scaling"**.

In vertical scaling, the resources of a single server, such as adding more CPU, RAM, or storage. In the context of our scenario, we quickly upgraded the server by adding more processing power and memory to cope with the increased demand. This allowed our web server to efficiently manage the skyrocketing traffic and ensured a seamless experience for users.

* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704731294902/bc0a3c43-1201-4b88-9355-5cad4c7fe660.png align="center")
    

### **Advantages**

1. **Simplicity:** It is simpler because we have to upgrade the hardware of a single server. No need to reconfigure or distribute the load across multiple servers.
    
2. **Short-term cost effective:** For a short term, upgrading a single server's hardware is cost effective than building a distributed system.
    
3. **Single Point of Maintenance**: Since, there's a single machine that is involved, maintenance tasks, such as updates and patches are generally simpler than a distributed system.
    

### **Disadvantages**

1. **Limited Scalability:** While scaling, we'll eventually reach a point where we have maxed out the limit of hardware upgrade we can do and we are stuck and its impractical or too expensive for further upgrades.
    
2. **Downtime:** To perform upgrades/maintenance the system has to be shut down, which leads to downtime.
    
3. **Hardware Dependency:** In vertical scaling, the application performance is directly related to the capability of a single machine.
    
4. **Distributed Application:** Vertical scaling is not suitable for cases where, there is a need of high computation, parallel processing or geographical distribution.
    

### **Scenarios where vertical scaling is good**

1. **Database Workloads:** Vertical scaling is good for database servers. Increasing the computational power of a db server helps in speeding up the performance especially in the case where a single powerful server can handle the workload efficiently.
    
2. **Legacy Systems:** In situations where rewriting or restructuring an application for horizontal scaling is impractical, vertical scaling can be a quick and effective solution
    
3. **Small to Medium Workload:** For applications with workload ranging between small to medium can be handled by a single server, vertical scaling is a cost-effective and straightforward solution.
    
4. **Spiky Workloads:** In cases where an application experiences occasional workload spikes, vertical scaling is a straightforward solution.
    
5. **Small Businesses:** For small businesses/startups with budget constraints, vertical scaling is more cost effective initially.