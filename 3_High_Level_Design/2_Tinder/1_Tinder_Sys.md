# Requirements

When designing the system, we will be drawing logical components and defining their interactions with other services based on the microservice architecture. We assume that any internal details can be handled with our prior knowledge of system design concepts. This includes load balancing, message queues, databases etc... The Tinder system has four requirements: storing profiles, recommendations, noting matches and chatting with matches.

# Image Storage: Files vs. Database BLOB

Storing profiles is trivial except for the image storage, where we argue on BLOB vs File storage. The distributed file architecture seems best when storing images.

# Profile Creation and Authentication

Storing profiles is trivial except for the image storage, where we argue on BLOB vs File storage. The distributed file architecture seems best when storing images.

# One to One chat messaging

Direct Messaging or chatting with matches can be done using the XMPP protocol, which uses web sockets to have peer to peer communications between client and server. Each connection is built over TCP, ensuring that the connection is maintained. The session micro service can send messages to the receiver based on connection to user mappings.

XMPP(Extensible Messaging and Presence Protocol) is an open communication protocol designed for instant messaging, presence information, and contact list maintenance.

# Matching right-swiped users

Our system is decoupled as much as possible. We try to maintain accept and reject information on the client. On swiping left or right, the client can note the action and avoid showing the same user again, perhaps using bloom filters.

The server has a validation engine called the matcher micro service, which notes matches and allows or disallows chat between two users.

# Serving recommendations to users

The final requirement of recommendations needs city wise partitioning on the user data. This is achieved using NoSQL databases like Cassandra or Amazon Dynamo. The other option is to use relational databases with horizontal partitioning. The concept is now refered to as sharding.
