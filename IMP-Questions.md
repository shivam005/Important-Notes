# Important Questions

# Why redis is faster, even after being single threaded ?? 
**Redis uses IO multiplexing, hence it's faster even after being single threaded.**
![image](https://user-images.githubusercontent.com/38420375/186170463-4ce02807-2dc1-4cd8-88d1-c5dd31dd0ece.png)

# How many types of I/O Model is there?

There are 5 I/O models -  
### Blocking I/O  
By default, all sockets are blocking. 
### Non-blocking I/O  
When a socket is set to be nonblocking, we are telling the kernel "when an I/O operation that I request cannot be completed without putting the process to sleep, do not put the process to sleep, but return an error instead".
### I/O multiplexing 
It is the capability to tell the kernel that we want to get notified when one or more I/O conditions are ready. 
### Signal driven I/O  
Signals are used to tell the kernel to notify applications with the SIGIO signal when the descriptor is ready. It is called signal driven I/O Model.
### Asynchronous I/O  
In this the kernel is told to start operation and to notify when the **entire** operation (including the copy of the data from the kernel to our buffer ) is over.

# which constructor of the thread class accepts runnable parameter.
Thread(Runnable target)

# What are the steps followed by computer when it starts? 
The CPU starts and fetches instructions into RAM from the BIOS, which is stored in the ROM. The BIOS starts the monitor and keyboard, and does some basic checks to make sure the computer is working properly. For example, it will look for the RAM. The BIOS then starts the boot sequence. It will look for the operating system. If you don’t change any of the settings, the BIOS will fetch the operating system from the hard drive and load it into the RAM. The BIOS then transfers control to the operating system.

# What is WebSocket API?
The WebSocket API is an advanced technology that makes it possible to open a two-way interactive communication session between the user's browser and a server. With this API, you can send messages to a server and receive event-driven responses without having to poll the server for a reply.

# What is JSR (Java Specification Request) Annotations ?
JSR annotations are part of the Java standard, and they play a significant role in improving code readability, maintainability, and portability by providing a standard way to express various semantics and configurations in Java applications. Developers can also create custom annotations to suit their specific needs, but JSR annotations represent the set of standard annotations provided by the Java platform. Eg; @Resource @PostConstruct @PreDestroy @Nullable @Inject @Entity @GeneratedValue etc.

