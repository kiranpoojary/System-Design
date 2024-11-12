

# Requirements of a cab aggregator

high-level design of a cab aggregator system, using Uber as an example.

The system design is centered around a user who books a cab from point A to point B, and the use case can be extended to other apps such as food delivery and pick-up/drop-off services. The video explains the challenges involved in pricing, search pricing, and matching, which are all important components of a successful cab aggregator system.

The system relies on real-time calculations to determine the price, dynamic search pricing, and efficient matching of drivers with riders.


# Static Pricing of Rides

The pricing feature must be both accurate and fast to ensure that users do not drop off from the app before making a booking. To achieve this, the app uses a cache to store information about regions and their pricing, but a rule engine is a better alternative as it allows for more flexibility and is easier to maintain.

Pricing is determined based on the user's location, the time of day, and supply and demand in the area. The video also discusses how the rule engine can be implemented and how to choose the right granularity of regions for pricing purposes.


# Ride Matching

The most critical factor is how many riders are available nearby.

The algorithm works by selecting a small region where a person wants to book a cab and finding all the available drivers in that area. If their estimated time of arrival is within a threshold, they will be sent a ride request.

If none of the drivers accepts the request, the size of the region will be increased. Frequent location updates are crucial to finding the right driver and predicting the estimated time of arrival accurately.

The final optimization required is for drivers' paths. The algorithm needs to consider the drivers who will be close enough to accept a ride in the next ten minutes and who will be closest to the person's destination when the ride completes.

The estimated time of arrival from the current location to the destination and from the destination to the pickup point should be less than or equal to the threshold time. All the potential pickups need to be run through this equation to select the best match.


# Matching Drivers with Live Rides

Location updates and the estimated time of arrival are critical in finding the right driver for a passenger.

The ride-matching algorithm works by finding nearby riders and sending them a request to accept the ride. If none accept, the proximity radius is increased, and the request is sent to more drivers.

The video also mentions that optimization for drivers is necessary, considering their current location and the next ride they'll take.

Finally, the video introduces an equation to determine the right driver for a passenger, taking into account the estimated time of arrival from the driver's current location to the destination and then to the pick-up point.
