---
title: "Networking"
summary: 
date: 2025-12-29
series: ["PaperMod"]
weight: 1
aliases: ["/networking-1"]
tags: ["Networking"]
author: ["Carlos A"]
---

I started my career in IT working the service desk, resetting passwords, replacing equipment, and rebooting machines. Eventually, the opportunity came to learn more about networking, and as I did that, I was able to provide some basic networking support-troubleshooting network connectivity issues, running cables and learning the architecture of our on-prem network.

Learning networking helped decode the mystery of the internet, something used by most on a daily basis and yet most people would struggle to explain. It used to be a common interview question for IT professionals to explain how the internet works in as much detail as possible. This post won't go into that, but will explain some fundamentals of networking. 

## OSI model

The OSI model (Open Systems Interconnection model) is a framework set by ISO (the international organisation for standardisation) to define the flow of data for computer-computer communication.

The 7 layers of the model are:

Application

Presentation

Session

Transport

Network

Data Link

Physical

### Encapsulation

Data flows from the top-down when outgoing, and from the bottom-up when incoming.
The OSI model is a good way for engineers starting out to learn about encapsulation and decapsulation- this is the process by which the data gets "wrapped" in headers (and sometimes trailers) as it is prepared to be sent to another computer. When data is being sent, each layer wraps the data received from the previous layer as it moves down the model. At the receiver, each layer is then "stripped" by their respective layers until the original data is at the desired destination application. 

### Headers

Headers consist of information that help the receiving machine understand and organise the data being sent. An example of information that might be sent in a header is the destination port, which helps identify the apps sending and receiving data, a common example being that computers "listen" on port 443 for HTTPS.

### Network Protocols

I'll now explain each layer in a little bit more detail, but before that I will briefly define network protocols. Network protocols are simply a set of rules which standardise how devices talk to each other. There are many different protocols for different purposes, which allows us to break down complex tasks into simpler ones by having protocols for specific tasks. 

An example of this could be that Internet Protocol (IP) is used for handling routing between networks, whilst Ethernet handles communication and discovery of devices within the local network.

## OSI Layers

### Application Layer
The originating and destination applications live at this layer, examples of this include web browsers and email clients. Protocols like HTTP are used at this layer.

### Presentation Layer
The presentation layer deals with encryption, compression and translation. For example, outgoing data is encrypted in this later and decrypted here at the receiver.

### Session Layer
The session layer is concerned with the management of sessions, including initiation and termination. Examples of this include user logins, token management and streaming.

### Transport Layer
Breaks down data from the Session Layer into smaller chunks to send, ensuring end to end delivery usually using one of either TCP (Transmission Control Protocol) or UDP (User Datagram Protocol).

#### TCP
TCP is known as a "connection-oriented" protocol, which means it sets up a connection and ensures receipt of data through the use of the TCP header, which contains information that helps the receiver to correct errors and retransmit lost data. TCP is used in cases that require reliability and data integrity.

#### UDP
UDP is a "connectionless" protocol, which means it sends data quickly without guaranteed delivery, ordering or error correction. UDP's data structure is much lighter than TCP's, and is used in cases where speed is the most important, such as live streaming.

### Network Layer
The Network layer takes data (known as segments) from the Transport Layer and adds an IP address which tells the router where the data is being sent. This data unit is known as a packet.

### Data Link Layer
This layer deals with physical hardware addresses (otherwise known as MAC address), using protocols such as Ethernet. The headers added here allow data to move within devices on a local network. This layer comes into play when your data arrives at the destination network, using the MAC address to find the destination device on the network.

### Physical Layer
This layer represents the physical cabling and network interfaces between each device, with data being sent as a stream of 0s and 1s.

Side note: the layers are sometimes seen numbered 1 through 7 online and in some books, with layer 1 being the Physical and 7 being the Application. We sometimes jokingly refer to human error as a "Layer 8 error".

## Routers and switches
Networks consist of many different devices, but I will go into the most common ones here. For those unfamiliar with the term "hop", a hop represents a single journey from one network device to another. 

Switches are devices that operate at the Data link layer, using mac addresses to direct traffic to their desired destination. Switches maintain a record of which ports are connected to which devices using a CAM tables. This allows it to only send data to where it needs to go, which is more efficient than broadcasting it across all ports. There are now Layer 3 switches which are more "intelligent", but for simplicity it's easier to think of switches at the Layer 2/Data Link layer level.   

Routers operate at the Network layer. They use IP addresses to route packets to their destination. Routers use routing tables to find the next best hop for the data. If no match is found, routers typically use a default route in the hope that the router at this address knows where to send the packet next. If multiple routes exist, then metrics are taken into account to determine the optimal route. Packets have an attribute called Time-To-Live(TTL) which is the maximum number of hops a packet can make before it gets discarded.  


## Addresses and ports
Addresses are used by network devices to help determine where data needs to go. The two most common types are MAC and IP addresses. This section requires some understanding of binary.

### MAC addresses
Mac addresses are a 48 bit number(12 hex digits), with the first half of the identifying the manufacturer.

Example MAC: 00:1A:2B:3C:4D:5E

### IP addresses
IP Addresses are a digital address for your device. There are a few different kinds of IP addresses e.g. static, dynamic, public and private.

#### Static IP addresses

Static addresses are addresses that are specifically assigned to a device. This is required for cases where you need a permanent address that won't change.

#### Dynamic IP addresses

Dynamic addresses on the other hand, are addresses that are assigned temporarily. A common use case for this is Wi-Fi. When connecting to Wi-Fi networks, devices are usually assigned temporary IP addresses by default through DHCP(Dynamic Host Configuration Protocol) from a pool of available addresses. 

#### Public IPs

Simply put, public IP addresses are internet-facing addresses. This is the address by which your device could be directly accessed from anywhere in the world with an internet connection.

#### Private IPs

Private IP addresses are internal addresses. These are only used internally and typically assigned by your router. The address for your device on your home wi-fi will typically be a private IP address. In order to access the internet, data flows via the router, which will be exposed to the internet via a public IP.

#### IPv4 and IPv6

There are two generations of IP addresses, IPv4 and IPv6.
The older IPv4 addresses are comprised of 32 bits, grouped into 4 octets.

Example IPv4 address: 192.168.0.1
Example IPv6 address: 2001:0db8:85a3::8a2e:0370:7333

IPv6 addresses are 128 bits, commonly grouped into 6 hex octets. IPv6 was developed as the world was running out of public IPv4 address, but an intermediate solution was found to allow IPv4 to still be widely used via Network Address Translation (NAT). This is when the traffic from local network devices is translated to use the public IP address of its router only, as opposed to each network device having its own public IP.

### P.S.
No one asked, but what motivated me to write this what that once upon a time I passed the Cisco Certified Networking Associate 200-301 Certification (now long expired). 

Within IT and tech, the online consensus seems to be that modern cloud certifications are not considered to be valuable measures when hiring, but the CCNA is considered to be a respected and difficult exam that includes practical elements and simulations which involve the configuration and troubleshooting of Cisco network switches and routers. 

I studied pretty hard for this exam- I remember using software called Packet Tracer and GNS3(?) which you could use to emulate Cisco hardware and build networks, but it's now been so long that even outside of the Cisco specific stuff I feel my networking fundamentals are slipping (I just remember copy run start was the most important command, it saved your current active config so it loaded after a reboot).

Recently, I looked through my email to find my score report as I reached the point where I doubted I had even done it at all! (I did manage to find it).

I don't know if I'll need to know how to configure a Cisco switch again, but in the modern AI development world, networking is one of those fundamentals that is unlikely to change. I think having strong fundamentals now will be more valuable than ever. 