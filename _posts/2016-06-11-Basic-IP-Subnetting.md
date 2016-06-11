---
layout: note
title: Basic IP Subnetting
---

# IP Subnetting
* IP addresses are made up of 32 bits
    - Broken into 4 octets (1 octet = 8 bits)
* The right most bit contains 2^0
    - The octet max is 255
* Octets are borken down to provide an addressing scheme that can accommodate large and small networks
* There are 5 different classes of networks A to E.
    - D and E are reserved
* Class can be determined from 3 high order bits
* In Class A  the first octet is the network portion
    - Octets 2, 3, and 4 are for the network manager to divide into subnets and hosts as they see fit
    - Class A addresses are used for netowrks that have more than 65,536 hosts
* In Class B the first two octets are the network portion
    - Used for networks that have between 256 and 65534 hosts
* In Class C the first three octets are the netowrk portion.
    - Class C is perfect for networks with less than 254 hosts

## Network Masks
* Network Mask helps you know which portion of the address identifies the network and which portion of the address identifies the node
* Default Masks
    - Class A: 255.0.0.0
    - Class B: 255.255.0.0
    - Class C: 255.255.255.0
* An IP address on a Class A network that has not been subnetter would have an address/mask pair similar to 8.20.15.1 255.0.0.0
    - 8.20.15.1 = 00001000.00010100.00001111.00000001
    - 255.0.0.0 = 11111111.00000000.00000000.00000000
* Any address bits which have corresponding mask bits set to 1 represent the network ID
    - 8.20.15.1 = 00001000.00010100.00001111.00000001
    - 255.0.0.0 = 11111111.00000000.00000000.00000000
    -------------------------------------------------
    -           = net id  |      host id

* netid = 00001000 = 8
* hostid = 00010100.00001111.00000001 = 20.15.1

## Understand Subnetting
* Subnetting allows you to create multiple logical networks that exist within a single Class A, B, or C network.
* Any device, or gateway that connects n networks/subnetworks has n distinct IP addresses, one for each network/subnetwork that it interconnects
* In order to subnet a network, extend the natural mask with some of the bits from the host ID portion of the address in order to create a subnetowrk ID.
* For example, given a Class C netowrk of 204.17.5.0 which has a natural mask of 255.255.255.0
    - 204.17.5.0 -      11001100.00010001.00000101.00000000
    - 255.255.255.224 - 11111111.11111111.11111111.11100000
                        --------------------------|sub|----
* By extending the mask to be 255.255.255.224 you have taken 3 bits from the original host portion of the address and used them to make subnets
* With these 3 bits it is possible to create 8 subnets.
* Each subnet can have up to 32 host addresses
    - 30 of which can actually be assigned to a device
    - Can be denotated as 255.255.255.224 or as /27
    - Since there are 27 masked bits
* Following this example if 2 routers are used:
    - Each router is connected to 4 subnets
        + One of these subnets is common to both routers
* The more host bits you use for a subnet mask, the more subnets you have availble
* However the more subnets available, the less host addresses available per subnet
    - Class C network of 204.17.5.0 and a mask of 255.255.255.224(/27) allows you to have eight subnets, each with 32 host addresses
    - If a mask of 255.255.255.240(/28) the break down is as follows:
    - 204.17.5.0 -      11001100.00010001.00000101.00000000
    - 255.255.255.240 - 11111111.11111111.11111111.11110000
                        --------------------------| sub|---
    - So only 4 bits are used for both subnets and hosts
        + 16 subnets and 16 host address (14 are usable)


[Source](http://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/13788-3.html "Source")
