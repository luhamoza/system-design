# System Design

---
 This repo is my high-level notes for learning system design.

1. Computer Architecture

    - Learn about storage (Disk, RAM)
    - RAM and Disk cannot communicate with each other, thus CPU is introduced.
    - CPU perform computation read, execute code from storage. (microsecond)
    - CPU has another component called cache to make CPU perform faster. (nanosecond)
    - Some task that were executed frequently, we can take a fragment of the task from RAM and allocate to the cache.
    - Cache typically in MB, RAM typically in GB, Disk/SSD typically in TB

2. Application Architecture
   
   - Vertical scaling - making a single server/machine/computer better, to improve hardware limitation. 
     
     - Get a better CPU for a server to handle more request/
     - Get more RAM for server to do more.
     - Computer have limitation cannot handle infinite request, thus horizontal scaling is introduced.
   - Horizontal scaling - multiple server running source code, thus user will make request to not  only single server, this way the application able to handle more requests.

     - The problem is how should we know which request for which server, thus load balancer is introduced. 
     - Load balancer will forward a request to a server that has minimal amount of traffic as we don't want one server handling more request while another server handling less.

   - Logging - external service to store log, to tell a developer if the request is actually working or there is something wrong with server.
   - Metrics - get insight on how the application running.
   - Alerts - metrics feed data into alert service to tell developer when some metrics have reach some threshold.

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
    - Reliability (DDoS Attack), Fault Tolerance (one server down, another server can work), Redundancy (backup server in the event of fault/failure)
    - Throughput - amount data can be processed in the period of time (request server can handle per second)
      - Reading from Database (QPS - query per second)
      - Data pipeline (bytes per second)
    - Latency - period of time (when some user made a request to a server, latency is amount of time for it to complete) (how long each request takes usually depends on network)
      - CDN (content delivery network to reduce latency)
    - In conclusion, we want to design a powerful system that can handle failure, handle high throughput and do it efficiently with low latency.
4. Networking Basics
   
   - How to communicate back and forth between a client and server.
   - Every machine communicating over a public address needs to be assigned a public IP address so that server can know which client to send data to.
   - IP address is 32-bit integer (ex. 012.345.678.910) (IPv4 limited as only can store IP address up to 4 billion only) (IPv6 is 128-bit integer)
   - The rule of sending a packet of data over an internet is called Internet Protocol
   - In a packet of data, there is some reserve potion for metadata (describe the entire piece of data just like mailing in real life) - this piece of data is called Header.
   - IP Header - contain source IP address, destination IP address and more.
   - TCP - Transmission control protocol (solves a problem when let's say when user wanted to send a large book and separate each parts by front cover, middle part, ending part etc. When user sends this kind of data, how does the receiving server actually know how to reassemble each part accordingly, this is where TCP comes to solve the problem )
   - TCP Header - contains metadata about sequence number to reassemble data back into the correct order.
   - Typically, in a packet of data, it contains IP Header, TCP and Application Header - Application Header to store stuff about HTTP request.
   - In a single request communication between computer, there are multiple protocol:
     - IP - Network layer - which device, which computer
     - TCP - Transport layer - ensure the data transported and reassemble in correct order and its arrival at the destination
     - HTTP - Application layer  protocol - what application is actually use
   - Public and Private IP address - only Router required for public IP address, and it will assign LAN (local area network) a Private IP address to each client connected to the Router.
   - Ports - ex. port 80, port 42, port 443
     - HTTP - port 80 (default port)
     - HTTPS - port 443 (default port)
     - for client, it typically does not matter which port assigned to, for example (127.0.0.1:4200 - accessing local server in local machine (localhost)) - only able to run single application in a single port at one time.
   