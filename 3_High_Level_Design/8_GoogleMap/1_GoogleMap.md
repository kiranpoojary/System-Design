# Requirements of a Map application

the system design of a map application like Google Maps, which is used for estimated times of arrival and providing the best possible routes.

The primary responsibility of the application is to track the location of the user and update them with the best possible routes. It also discusses the feature of adding locations and finding nearby stores, like restaurants and gyms.

Searching for nearby locations is filtered using a Cartesian distance and ETA is an important feature. Traffic updates and estimated time of arrival is also important.

Here is what we will be covering:

1. Finding the best route from a source to destination
2. Adding Locations in the map
3. Finding Nearby Stores
4. Notifying users with traffic updates
5. Calculating the estimated time of arrival

# Routing Challenges in Maps

Finding the optimal route amongst an infinite number of intermediate points, with potentially infinite number of paths, is hard.

We tackle the following two problems in this video:

1. How do we reduce the number of points to contend with in a map?
2. How do we efficiently find a solution route amongst a large number of potential solutions?

# Partitioning Algorithm: Splitting the graph into regions

How Google Maps deals with the problem of too many possible routes between two points?

One solution is to reduce the number of routes by finding popular hubs or common routes that most people use, even though this may not be the optimal route. The other solution is to compute the result faster, which may require approximation.

Google uses graph partitioning algorithms and artificial intelligence to split roads or entire regions in an optimal way to find these hubs. This technique can also be applied to public transport like bus and metro stations.

# Finding the shortest path - A\* search

A start, this algorithm takes into account the time taken to move from one position to another as well as the estimated time to reach the final destination.

To get accurate times for the edges, Google Maps relies on actual, real-time data from people moving from one position to another. The best way to store this information is to use a graph database that can store points and edges.

We recommend using Neo4j, which provides built-in graph algorithms.

# GeoHash and other proximity filters

We discuss the technology used in Google Maps, specifically the location tracking, adding new locations, and finding nearby stores.

Gaurav Sen explains that location tracking involves sending a request to the server every five seconds to notify the server of your location. The speaker then suggests using a graph database to add new locations, and also suggests using open-source libraries to render locations on the client.

To find nearby stores, we suggest using a keyword search and filtering out stores that are too far away. Finally, we discusses the use of Geo hash to build a hash of a location by splitting the 2-D space recursively.

# Detecting traffic jams and broadcasting updates

The traffic updates are relevant when a user is traveling from a particular position to a destination, and there is an update on an intermediate road that the user is supposed to travel on.

There are three factors that Google Maps uses to update the time it takes to finish a stretch of road: user updates, average time spent in the last five minutes, and the number of users in a particular stretch.

To update a user's ETA, Google Maps needs to store the active routes of each user and inform them of any updates to their route. The server is responsible for giving the user the most efficient route, even if it means going through the same road.

# Calculating an accurate and efficient estimated time of arrival
