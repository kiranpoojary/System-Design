# Requirements of a chess website

We set the following requirements to design a chess website:

1. Users can declare challenges, and accept game challenges.
2. A user should be able to play a game with another user.
3. Users can analyze their games later.
4. Optional (Users can spectate games)
5. Optional (The system should identify cheaters and ban them)

Non-functional requirements:

1. The game-play should be smooth, and have low latency.
2. The system must be fault tolerant.

# Handling connections at scale

Reducing latency is critical to the success of any gaming platform. "Lag" is the layman term used to describe this frustrating gap in time between the user doing an action and the server acknowledging that action.

# Consistent Hashing vs. Sharding

Rebalancing load, after a server is added or removed from a topology, is an important problem. Have a look at the consistent hashing video in the "Calling App" design for more details.

Consistent hashing and its variants are popular solutions to rebalancing load on a server.

# Connection related thundering herds

Creating connections to users on the server is an expensive process. What happens when we restart this server?

To reduce latency, and avoid thundering herds, this video talks about how we can continue maintaining connections in a changing code environment.

# Request Batching and Conclusion
