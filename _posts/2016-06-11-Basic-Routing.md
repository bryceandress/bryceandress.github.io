---
layout: note
title: Basic Routing
---
#Routing
## RIPv2:
* Legacy, Link State is perferred
* Periodic updates - 30s
* Invalid timer - 180s
    - After a route has not been heard from for 6 consecutive updates
* Holddown timer - 180s
    - After a route has changed metrics, no more updates are accepted
* Flush Timer - 240s
    - The between when a route becomes invalid and its removal from the routing table
* Metric - hop count
    - Range from 1-15, 16 being invalid
* v2 is classless
* Uses IP/UDP at its transport
    - Port 250
* Split Horizon
    - Information about a route should never go back in the direction that it was received
* Poison Reverse
    - A means of ensuring a split horizon, the routes DOES advertise a route back to the router from which it was learned. BUT it sets the metric to 16
    - Prevents routing loops

## IS-IS
* Used mainly in service provider networks
* Adjacencies are all directly connected routers (neighboring)
* Not as reliant on timers as RIPv2 but does maintain some to insure integrity
    - Hello interval  - 10s
    - Hello multiplier - 3
    - Holdtime = interval * multiplier = 30s
        + After 3 missed hellos a router tears down the adjaceny with the missing neighbor
* Metric default is 10, configurable per interface
     - Max is 1023, the maximum per interface metric 64(2^6)
     - Metric-style allows a maximum metric of 16777214(2^24)
* Every multi-access netowrk has a DR
     - Becomes adjacent to all other routers on multi-access network
     - Prevents all routers from forming mesh adjacencies
     - Elected through voting, priority can be changed to determin ahead of time who will be DR and BDR
* Does not use IP, uses Connectionless Newtork Services (CLNS)
     - Layer 3 protocol, analogous to IP
     - Each router needs to be configured with some basic CLNS settings
         + Network Entity Title (NET) one such address globally configured and it must be unique across the entire netowrk
* IS type is a way of creating a heirarchical routing architecture
     - Type 1 is used for routing within an area
     - Type 2 is used for routing between areas
* Type 1 routers only from adjacencies with other Type 1 routers and Type 1-2 routers
* Type 2 routers only form adjacencies with other Type 2 routers and Type 1-2 routers

## BGP
* Combination of distance vector and link state methods
    - Counts hops as the length of the path
    - Sends updates on topology changes, like a link state protocol
* BGP uses TCP as the transport protocol
    - Port 179
    - A pair of BGP peers forms a TCP connection between one another to exchange routing information
* Used for intra (iBGP) and inter (eBGP) Autonomous System (AS) route exchanges
* AS is contigous network that is controlled by one entity
    - PTD's network is 1 AS
* Each AS is represented by an Autonomous System Number (ASN) assigned by ARIN
    - PTD's ASN is 3737
* ASN is an important part of any BGP configuration
* BGP Synchronization is generally disabled in a network
* iBGP is fully meshed
* Ultimate goal is to have all BGP routers agree on what is the best path for any BGP route
    - If this does not occur, routing loops will happen
* PTD sends our upstream Providers only our internal customer routes while we receive full routes from each peer
* BGP has no load balancing

## Route Redistribution
* Route learned via one protocol does not automatically get learned/propagated by another protocol runnong on the same router
* Route redistribtuion is the process of taking the routes learned via one protocol and forcing another routing protocol to send those routes to its peers in effect "redistributing" them
* Should be filtered in some way to avoid looping
* RIP is redistributed into IS-IS and vice-versa
* Route-maps are used to filter the redistribtuion
* PTD does not redistribute BGP

## Label Switching
* Provider (P)
* Provider Edge (PE)
* Customer Edge (CE)
* Custoemr (C)

## Label Distribution Protocol (LDP)
* TCP protocol
    - Port 646
    - Uses multicasted hellos

## Fiber Optic Networking
* The greater the dB the less light that will reach the far end of the link

## Fiber Types
* Multimode (MM)
* Single mode (SM)
* PTD normally uses multimode fiber for connections between devices inside a building, single mode fiber for connections between devices in different buildings
* Simplex is usually in a yellow jacket, means only one fiber in the jumper
* Multimode tend to have an orange jacket. Consisted of two fibers used for transmition and receiving
