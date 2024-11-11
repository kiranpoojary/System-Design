# Scope and Requirement setting

We identify the key features of the system by noting down its:

1. Services
2. APIs
3. Database schemas

# Chapter #1: Service Registration and Proxies

We tackle the first few requirements here: Registering a user with 2-factor authentication, and allowing them to "login".

client-> Gayeway->service reg./manager to get service details

then Gayeway forward request /auth to ay=uth-service

Gateway can cache the service manager details for a while to avoid sample api calls.

# Chapter #2: Authentication & Global Caching

The authentication service needs to authenticate every user request. How do you balance efficiency and security?

# Chapter #3: API contracts & Versioning

How are API contracts made and managed in a micro-service architecture?

backward version compatability

# Chapter #4: Sending, Tagging & Searching Emails

The core of the system: sending and searching emails with their metadata.

# Chapter #5: Contacts & Groups
