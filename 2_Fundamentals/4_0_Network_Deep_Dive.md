# Computer Network

## **Breakdown -The Physical Layer**

start and end delimeter is required to know where msg started and where ended.

start_delimeter+info+end_delimeter

hardware defines the how msgs are passed.

## **Breakdown -The Routing Layer**

not necessary, but useful.

## Breakdown: The behavioral layer

# **Connecting to the internet: ISPs, DNS and everything in between**

1. Client
2. NIC
3. Router
4. DNS(Domain Name Server): helps to find IP for a URL
5. ISP: broadcast IP and URL to DNS to register mapping

# Internal routing: MAC addresses and NAT

1. CDN: cache response across world for fast delivery
2. Repsponse Decoding: send reponse from server to requested client
3. NAT(N/w addr translation):
4. MAC Address:

# HTTP, WebSockets, TCP and UDP

## HTTP

Clinet to server

## Socket

peer to peer seamless connection

**uses**

1. Chat app
2. online presence
3. Contact list mngt

## TCP

Transmission Control Proto

- Guarantees order of delivery
- Ack for deliver
- Retry send

## UDP

User Datagram Proto

- No Guarantees order of delivery
- No Ack for deliver
- No Retry send
- Realtime delivery(no need to resend if fails e,g: live video streaming data)

# Communication Standards: REST, GraphQL and GRPC

## REST(**Representational State Transfer**)



## GrahQL

request specific or required data


## GRPC

**a modern, open-source framework for developing APIs, based on Remote Procedure Calls (RPC)** . Unlike REST APIs which typically use HTTP/1.1 and JSON, gRPC uses HTTP/2 for transport and Protocol Buffers for message serialization, resulting in faster and more efficient communication


# Head of line blocking

ead-Of-Line blocking occurs when the message/data packet at the head of the queue cannot move forward due to congestion even if other messages/packets behind this could.

**HTTP 2.0 solves this problem using Multiplexing.**


# Video transmission: WebRTC and HTTP-DASH

HTTP DASH Proto

DASH(Synamic Adaptive Streaming overHTTP): according to internet speed quality of video decided


Video transmission: WebRTC and HTTP-DASH

* **What do servers do while handling video data?**

  Video files are large and cannot be sent in a single response. They have to be broken into packets.
* **Why HTTP is not good for video transmission?**
  HTTP is stateless. The client has to specify which chunk it wants because the server does not know about the previous requests.


**WebRTC** helps in video conf :- its browser to browser communication
