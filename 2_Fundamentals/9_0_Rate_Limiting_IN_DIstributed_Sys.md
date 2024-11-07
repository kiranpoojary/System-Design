# Rate Limiting

The ways in which rate limiting can be implemented in a distributed environment.

**The Oracle and the Timer Wheel**

- If our services are overloaded with requests then the time required to send a response will increase resulting in a bad user experience.
- If the number of requests keeps on increasing then our servers might crash due to Out of Memory exceptions.
- We want to avoid cascading failure.

A cascading failure is a failure that grows over time due to positive feedback. It can occur when one service of a distributed system fails, increasing the probability that other services fail. Let's understand this with an example.

We have two servers A and B. Both can handle at most 500 requests.

Currently, A is serving 400 requests and B is serving 300 requests.

Now suddenly B is getting 600 requests. It cannot handle that many requests and crashes. Now we need to route all the requests to the other server i.e., A. But A cannot handle 400 + 600 requests so it also crashes. This is known as cascading failure.

**Timer Wheel**

In a timer wheel,

- Size of the wheel (Number of buckets) = Timeout of the incoming request
- Each bucket is numbered from 0 to Timeout -1
- Each bucket can store a limited number of requests
- Every time we add a request to the bucket number Time % Number of buckets
- Our system can pull requests from this queue one by one.
- Before inserting a new request into a bucket it deletes all the existing requests (These requests have not been processed by the system).

**Note:** If there are a lot of slots then the distance between any two requests can be very large. In such cases, we will be wasting a lot of system resources and time. To tackle this issue we can use Hierarchal Timer Wheel.

Well now we have rate-limited external requests but our internal services are also talking to each other. One service sending a lot of requests to another service might cause the other service to fail. So let's discuss how we are going to solve this issue in the course video!!

# Partitioning and Real-life Optimisations

**Rate Limiting Internal Requests**

If we are optimistic we can have a Service Level Agreement which states the number of requests one service can handle.

But a better approach is to have rate limiters in the service itself.

But how does a service know that it cannot handle any more requests?

**1. Average Response**

Time If the average response time is increasing then either the service is not functioning or it is under too much load and cannot process requests fast enough.

**2. Age of requests**

Let's say the service takes at most 1s to process each request but many requests are present in the queue for more than 2s. That means the number of incoming requests >> the Number of requests the service can process.

**3. Dead letter queue**

Every time our service is unable to process a request it sends the request to the dead letter queue. If the number of requests keeps on increasing in the dead letter queue then we know that our system is failing to process requests.
