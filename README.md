# System Design

---
 This repo is my high-level notes for learning system design.

1. Computer Architecture

    - Learn about storage (Disk, RAM)
    - RAM and Disk cannot communicate with each other, thus CPU is introduced.
    - CPU perform computation read, execute code from storage. (microsecond)
    - CPU have another component called cache to make CPU perform faster. (nanosecond)
    - Some task that were execute  frequently, we can take a fragment of the task from RAM and allocate to the cache.
    - Cache typically in MB, RAM typically in GB, Disk/SSD typically in TB

2. Application Architecture
   
   - Vertical scaling - making a single server/machine/computer better, to improve hardware limitation. 
     
     - Get a better CPU for a server to handle more request/
     - Get more RAM for server to do more.
     - Computer have limitation cannot handle infinite request, thus horizontal scaling is introduced.
   - Horizontal scaling - multiple server running source code, thus user will make request to not  only single server, this way the application able to handle more request.

     - The problem is how should we know which request for which server, thus load balancer is introduced. 
     - Load balancer will forward a request to a server that have minimal amount of traffic as we don't want one server handling more request while other server handling less.

   - Logging - external service to store log, to tell developer if the request is actually working or there is something wrong with server.
   - Metrics - get insight on how the application running.
   - Alerts - metrics feed data into alerts service to tell developer when some metrics have reach some threshold.

3. Design Requirements

   - Thought process - analyzing  which tradeoff can be made, which sacrifice can be made to get improvement. 
   - Typically design requirements involve

     - move data
     - store data
     - transform data
     
   - Availability - benchmarks to ensure the design is good or not.

   ``Availability = Uptime / Uptime + Downtime``
   
    - SLO - service level objective
    - SLA - service level agreement (ex. if AWS don't reach some level SLA, AWS will partially refund)