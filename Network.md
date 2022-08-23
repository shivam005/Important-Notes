# Networking-Notes

A protocol is a set of rules that define how communication occurs in a network.  
**Ethernet** is a protocol made for Local Area Networks (LAN).This protocol is a wireless computer networking standard and used to allow laptops and smartphones to communicate without being connected with a cable.
![image](https://user-images.githubusercontent.com/38420375/186122536-d4a7e65d-6a88-4fab-b47d-98a68c036c0a.png)

**Internet Protocol (IP)::** Its goal is to ensure the successful delivery of packets from source to destination. This protocol is responsible for addressing and fragmenting data packets in digital networks

**Internet Control Message Protocol (ICMP)**  It works with the IP protocol. It helps to diagnose network communication issues or  whether or not data is reaching its specified destination in the best ways. Unlike IP, ICMP is a connectionless protocol, no need to establish connection b/w system. Hence, It is used in DDOS attack. 

**Address Resolution Protocol (ARP)**  It maps network addresses to the physical addresses (MAC address) used by a data link protocol. It is the process of finding an address of a computer in a network. 

**Transmission Control Protocol (TCP)**  It is used on the top of IP to provide reliable transmission of packets. TCP is a connection-oriented reliable protocol. It also provides an acknowledgment to the sender device regarding the status of the data being sent. So in case, the sender receives a negative acknowledgment, it resends the data. Eg. the secure shell, the file transport protocol, and the web accessing through the HTTP, World Wide Web (WWW), and email.

**User Datagram Protocol (UDP)** UDP is a connectionless and unreliable protocol. It sends messages without the initiation of a connection, which makes the data transfer real quick which is good for time-sensitive transmissions. UDP is used in real-time services like video communication, online gaming, live streaming of videos, etc. No Packet recovery, no error checking but better than TCP in terms of latency and efficiency. 

**Hypertext Transfer Protocol (HTTP)** It is the protocol helping applications to communicate with the users. HTTP is a connectionless and stateless protocol. A client and server know each other only during communication. As soon as they complete their communication, both of them forget about each other. Any data can be sent through HTTP.

**Dynamic Host Configuration Protocol (DHCP)** This protocol works on IP networks, assigning IP addresses to devices and hosts connected to the network. In addition to the IP address, DHCP also assigns the subnet mask, default gateway address, the domain name server (DNS) address, and other pertinent configuration parameters.

**Spanning Tree Protocol (STP)**   It eliminates redundant links and process network changes and failures. The STP monitors all the links in the network. To find any problem present in the links or a redundant link, it applies the **spanning-tree algorithm (STA)**. The STA builds a topology out of the current network and removes the redundant links. 

**File Transfer Protocol (FTP)**  It is responsible for the reliably and efficient transfer of files which is provided by TCP/IP.The data that can be sent through the FTP is limited to 2GB. The sender system and the receiver server may have different file conventions or different ways to represent data. In some cases, the directory structures of two systems may differ from each other. FTP resolves all of these issues. It establish, two connections;  One connection is for the data transfer, and the other one is for control connection.

**Secure Shell (SSH)** is a popular networking protocol that lets us access a remote computer over an insecure network such as the Internet. Secure Shell also supports both password and key-based authentication. 
![image](https://user-images.githubusercontent.com/38420375/186129234-f1f58bf5-0bc9-49ae-9b5a-5acf396d9242.png)
Secure Shell has a client-server architecture.

It is used for Communication between local and remote machines,
Remote access to server resources,
Executing commands in the remote host machine,
Performing numerous system administration tasks.              

Moreover, the key-based authentication provides convenient Single Sign-On (SSO) access across the remote hosts. 
 
**Secure Shell tunneling** is a technique that enables a user to open a secure tunnel between a local and remote host. It redirect network traffics to a particular port or IP address. 

**SSH File Transfer Protocol (SFTP)** also known as secure FTP is used to secure the connection when a file is sent remotely from one system to another using public-key encryption. File transfer using SFTP is much faster as it transfers files in binary format. FTP uses two connections to send the data. SFTP can send a file through a single connection. This eliminates the inconvenience to server administrators.








