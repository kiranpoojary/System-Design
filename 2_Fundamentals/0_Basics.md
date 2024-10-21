# 1. Scaling( Horizontavl vs Vertical)

Increate the ability of the system to handle more load

## i. Horizontal Scaling

Add more machine to increase the ability to handle more request/process

1. load balancing required
2. Resilient(no single point of failure)
3. Communication b/w services through n/w calls(slow)
4. Data Inconsistemce(n/w calls)
5. scales well(unlimited attach)

## ii.Vertical Scaling

add more capacity configuration to single machine(RAM, CPU, Proccessor) to increase the ability to handle more request/process.

1. load balancing NOT required
2. Not Resilient(no single point of failure)
3. Inter process communication(fast)
4. Data Consistent
5. Hardware limit(can't scale unlimited)

# 2. Monoliths vs Microservices

## i. Monoliths

### Advantages

1. Single service/sytem handling all the proccess.
2. This single sytem can be nore than one
3. This use 1 or more db
4. good for small team
5. deployment is easy
6. configuration are same no duplicates
7. faster(no n/w calls)

### Disadvantage

1. understanding the sys for new person
2. deployment monitoring
3. Single point of failure
4. 

## ii. Microservices

multiple services/system split the task according to its category/module, each service is independent of each other, each can have separate DB, connect via Gateways

### Advantages

1. easy scaling
2. easy for new comer to understand service by service
3. easy monitoring and debugging
4. 

### Disadvantages

1. need skilled architect
2. hard to setup and takes time to setup
3. 

# 3. Load Balancing

When horizontal scale happenend system should inteligently split forward traffic to multiple system so that traffic burden can be stabilized and save const as well.

## Load Balancing Algorithm

1. Round Robin
2. Geo based
3. Least connection

In the below diagram same service is using multple LB in each level.


    🖥️(IND)	--------->  🖥️🖥️🖥️(round-robin)


🙍‍♂️🙍‍♂️(geo-based)		🖥️(USA))  -------->  🖥️🖥️🖥️(least-connection)


    🖥️(UK)  --------->	🖥️🖥️🖥️(geo-based)


# 4. Sharding

1. Splitting DB for performance
2. Consistency is IMP
3. Availability
4. shard based of shard key(locationId, userId etc)
5. index on shards column(age)


## Disadvantages

1. shard joins are expensive


## Shard Fail

Master: Up-to-date shard

Slave: keep sync from master: If master fails choose on2 master from slaves


# 5. Single Point Of Failure

1. Means Architecture is not resilient
2. if multiple things are connected to one entity and  that entity fails then entire system fails.


## How to Avoid:

1. create one more replica of sys/nodes
2. Master and Slave for DB/ Read Replicas
3. Loadbalancer+multiple load balance
4. Multi Region replication for above 4 things
5. Chaos Monkey: for load testing
6. 


# Service discovery and Heartbeats



Servers crash due to various reasons like hardware faults and software bugs. Service Discovery and Health Checks are essential for maintaining a service ecosystem's availability and reliability. We talk about how a heartbeat service can be used to maintain system state and help the load balancer decide where to direct requests. Now when a server crashes, the heartbeat service and identify and restart the service immediately on the server.

Service Discovery is another important part of deploying and maintaining systems. The load balancer is able to adapt request routing. Both features allow the system to report and heal issues efficiently.

## Heath Service:

machine which check the heath of a node and take necessary action if not healthy

actions: try restart dead node or create new node and inform LB about inactive(dead) node so that LB don't send traffic to dead node.

2 way health check/heartbeat check: node is alive service is dead(example ec2 is running but app crashed): check ec2 health as well as app health

zombie node: node is active app crashed but some cron calling other service with stale data(reduce with 2way heartbeat check)


# Capacity Planning and Estimation: How much data does YouTube store daily?

Back-of-the-envelope calculations are often expected in system design questions. They help logically state the parameters influencing a result, and estimating the capacity requires multiple estimations on the way. Also lets us individually state our assumptions.

Eg: Estimate the hardware requirements to set up a system like YouTube


## capacity estimation of youtube content

### Storage

Let's start with storage requirements:

About 1 billion active users.

I assume 1/1000 produces a video a day.

Which means 1 million new videos a day.

What's the size of each video?

Assume the average length of a video to be 10 minutes.

Assume a 10 minute video to be of size 1 GB. Or...

A video is a bunch of images. 10 minutes is 600 seconds. Each second has 24 frames. So a video has 25*600 = 150,000 frames.

Each frame is of size 1 MB. Which means (1.5  *10^5) * (10^6) bytes = 150 GB.

This estimate is very inaccurate, and hence we must either revise our estimate or hope the interviewer corrects us. Normal video of 10 minutes is about 700 MB.

As each video is of about 1GB, we assume the storage requirement per day is 1GB * 1 million = 1 PB.

This is the bare minimum storage requirement to store the original videos. If we want to have redundancy for fault tolerance and performance, we have to store copies. I'll choose 3 copies.

That's 3 petabytes of raw data storage.

What about video formats and encoding? Let's assume a single type of encoding, mp4, and the formats will take a 720p video and store it in 480, 360, 240 and 144p respectively. That means approximately half the video size per codec.

If X is the original storage requirement = 1 PB,

We have X + X/2 + X/4 + X/8 == 2*X.

With redundancy, that's 2X *3 = 6*X.

That's 6 PB(processed) + 3PB (raw) == 10 PB of data. About 100 hard drives. The cost of this system is about 1 million per day.

For a 3 year plan, we can expect a 1 billion dollar storage price.

Now let's look at the real numbers:

Video upload speed = 3 * 10^4 minutes per minute.

That's 3 ** *10^4* * *1440 video footage per day = 4.5 * 10^7 minutes.

Video encoding can reduce a 1-hour film to 1 GB. So 1 million GB is the requirement. That's 1 PB.

So the original cost is similar to what the real numbers say.

If we are off by order of magnitude, it's good. However, being off by 3 or more orders of magnitude is too much. We can then highlight the following:

Where our assumption was wrong, or

Which factor we didn't take into account.

### Processor

Read+Proccess+Write


# Content Delivery Networks(CDN)

Content Delivery Networks are a bunch of servers spread across the globe to serve information. These networks are available on rent to deliver static content quickly to nearby users.

Some examples of CDNs are Amazon CloudFront and the Akamai CDN. They are (relatively) cheap to rent and have high availability. They also provide pluggable algorithms to invalidate and fetch data.


## Best Thing CDN Provides

1. Boxes(cache) near to users.
2. ease of following regulations
3. Content update from server(direct sync by cdn)
4. ex: AWS Cloud Front(cheap, reliable, easy)
