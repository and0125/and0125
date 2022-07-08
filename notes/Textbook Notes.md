# Textbook Notes

A place to jot down concepts from any one of my programming textbooks.

## From Mastering Python Networking

### OSI Model

The OSI model of networking consists of seven layers, which are below from top to bottom:

- Host layers:
    - application layer
        - protocol data unit: data
        - function: high-level APIs including resource sharing and remote file access
    - presentation layer
        - PDU: data
        - function: translation of data between a networking service and an application, inlcuding character encoding, data compression, encryption and decryption.
    - session layer
        - PDU: data
        - function: managing communication sessions, which are the exchange of information in the form of back and forth transmissions between two nodes.
    - Transport layer
        - PDU: segment (TCP) or Datagram (UDP)
        - function: reliable transmission of data segments between points on a network, including segmentation, acknowledgement, and multiplexing.
- Media Layers:
    - network layer
        - PDU: packet
        - function: structring and managing a mult-node network, including addressing, routing and traffic control
    - Data link layer
        - PDU: frame
        - funciton: relaible transmission of data frames between two nodes connected by a physical layer.
    - Physical layer
        - PDU: bit
        - function: Transmission and reception of raw bit streams over a physical medium.

### TCP/IP

The TCP/IP model is another developed at the same time as the OSI model, but is the one the internet was originally built on. Its similar to the OSI model in that it divides the end-to-end data communication process into abstraction layers, but TCP/IP model has only 3 layers.

- Application layer: 
    - includes the application, presentation, and session layers from the OSI model.
- Link layer:
    - includes the data link and physical layer from the OSI model.
- The other two layers are the network and transport layers in the OSI model.

TCP is one of the main protocols used on the interent today. This protocol operates at layer 4 of the OSI model, and is responsible for delivering the data segment between two nodes in a reliable and error-checked manner. This protocol consists of a 160-bit header that contains source and destination port information, a sequence number, an acknowledgement number, control flags, and a checksum. 

TCP uses datagram sockets or ports to establish a host-to-host communication. 

There are common ports dedicated to particular services, like port 80 is for http connections, and port 25 is for SMTP connections (email).

The TCP connection is managed by the operating system by the socket that represents the local endpoint for connection. 

The protocal operation consists of a state machine, where the machien needs o keep track of when it is listening for an incoming connection, when it's listening during the connection, and when it needs to release resources once the connection is closed. Each TCP connection goes through a series of states (see book for list). 

TCP guarantees that data is transmitted in an ordered and relaible fashion. Because it guarantees delivery, it is ofteen called a connection-oriented prtocol. It does this by first establishing a 3-way handshake to synchronize the sequence number between the transmitter nad receive, this is the SYN, SYN-ACK, and ACK states. 

The ACK state is used to track subsequent segments of the conversation, then one side will send a FIN message, and the other side will acknowledge the FIN message and send a FIN message. The FIN initiator will then ACK the FIN message, and close the connection. 

### Client Server Model

Most modern applications are built on the client-server model.

This is the model that has workstation nodes and server nodes, with the server nodes serving content to the workstation nodes. 

The servers typically sit idle, waiting for a client to initiate a request for their resources. 

This model of distributed resources that are requested by the client is referred to as the client-server model.

The server in the client-server model typcially lisens on one of the well known ports (above) to receive communication request from the client. 

### User Datagram Protocol

This is a core member of the internet protocol suite. like TCP it operates on layer 4 of the OSI model, and is also responsible for delivering data segments between the application and the IP layer. 

This protocol has a 64 bit header, which only has the source and destination port, length, and checksum.

This is a lightweight header, which makes it great for lightweight applciations that prefer faster delivery without setting u pthe session between two hosts or needing reliable data delivery. 

This made a big difference of the speed of transmission in the early days. 

### Internet protocol

We live at this layer, which is layer 3 of the OSI model. IP has the job of addressing and routing between end nodes, amoung others.  The addresing of an IP is its most important job. The address space is divided into two parts: the network and the host portion. 

The subnet mask is used ot indicate which portion in the network address consists of the network and which portion is the host by matching the network portion with a 1 and the host portion with a 0. IPv4 expresses the address in the dotted notation: 192.168.0.1. The subnet mask can either by in dotted notation (255.255.255.0) or use a forward slash to express the nubmer of bits that should be considered in the network bit (/24).

The IPv6 header has a fixed portion and various exxtension headers, including a next header field which can indicate an extension header to be followed that carries additional information. It can also identify the upper layer protocol such as TCP and UDP. The extnesion headers can include routing and fragment information. 

Today, the internet is still pretty much addressed with IPv4, with some of the service provider networks addressed with IPv6 internally. 

IP routing is about having the intermediate devices between the two endpoints transmit the packets between them based on the IP header. For all communication via the internet, there will be intermediate devices. This networking book is aout managing and optimizing these intermediate devices. 

### AWS Cloud Networking

AWS was the first company to offer IaaS public cloud services and was the clear leader in the space by market share in 2019. AWS could be considered the world's largest implementer of software-defined networking (i.e. software services working together to create network constructs). 

#### Regions and Availability Zones

AWS has 22 geographic regions and 69 availability zones around the world. Some of the services offered are global, but some are regionallly based. We should aim to build our infrastructure in a region closest to our intended users. This will reudce the latency of the service for our customers. 

These regions have services and cost implications. The cost per servce may be more per hour in different regions (book has an EC2 price comparison between Virginia and Frankfurt).

Some regions are not available by default, like the GovCloud, or the China region. All the regions are completely independent of one another, therefore most resources are not replicated across regions. That means if you are offering the same web application in multiple regions, say between US-East and US-West, to back up the services, you will need to replicte the necessary resources in each region yourself. 

Each region has a number of availability zones within it. Each Avilability zone is its own isolated infrastructure with a redundant power supply, intra-data center networking, and facilities. All AZs in a region are connection through low-latency fiber routes that are typically within 100 km of each other within the same region. 

Resources are copied across availability zones automatically, and you can configure this replication. 

This is important to understand because AWS's networking services are usually bound by the region and the availability zone. For instance, a virtual private cloud (VPC) netowkr needs to reside entirely in one region, and each subnetwork of the VPC needs to reside entirely in one AZ. On the other hand NAT gateways are AZ-bound, so we would need to crate one per AZ if we needed redudancy. 


#### VPCs

Since December 2013, all EC2 instances are VPC only, so you can no longer create an EC2 instance without a VPC. 