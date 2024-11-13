# Requirements

1. use can call each other over VOIP or PSTN
2. Call Routing
3. Charge use for making call
4. Choose a provider for each call

# Calling App Design

Things to notice: The candidate does a very good job at describing what the system will do. However, they do not talk about the deep problems, since they haven't spent time to expand on the requirements.

# Concept #1: Breaking calls into dialogs

# Concept #2: The state machine

We model the call's lifecycle as a state machine, and move both state storage and transition logic to the Call State Manager.

# Concept #3: Charging Users

We decide how the billing service should handle call invoicing, decoupling services and polling for call termination.

# Concept #4: Consistent Hashing for caching call state

Load Balancing is a key concept to system design. One of the popular ways to balance load in a system is to use the concept of consistent hashing. Consistent Hashing allows requests to be mapped into hash buckets while allowing the system to add and remove nodes flexibly so as to maintain a good load factor on each machine.

The standard way to hash objects is to map them to a search space, and then transfer the load to the mapped computer. A system using this policy is likely to suffer when new nodes are added or removed from it.

Consistent Hashing maps servers to the key space and assigns requests(mapped to relevant buckets, called load) to the next clockwise server. Servers can then store relevant request data in them while allowing the system flexibility and scalability.

Some terms you would here in system design interviews are Fault Tolerance, in which case a machine crashes. And Scalability, in which case machines need to be added to process more requests. These two principles are allowed by Consistent Hashing, and hence it is an important building block to a system design architect's toolbox.

Another term used often is request allocation. This means assigning a request to a server. Consistent hashing assigns requests to the servers in a way that the load is balanced are remains close to equal.

Server architecture is a subjective concept, and there are outliers for many cases. Don't think of Consistent Hashing as a silver bullet for fault tolerance and scalability, but a useful concept for request allocation.
