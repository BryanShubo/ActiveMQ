# ActiveMQ
1.1 Advantage:
JMS compliance
1) synchronous or asynchronous message delivery, 
2) once-andonly-once message delivery, 
3) message durability for subscribers, and much more


Connectivity
HTTP/S, IP multicast, SSL, STOMP, TCP, UDP,
XMPP, and more

Pluggable persistence and security
1) ActiveMQ offers its own style of ultra-fast message
persistence via KahaDB, but also supports standard JDBC-accessible databases.

2) authentication and authorization

Building messaging applications with Java


Integration with application servers

Client APIs

Broker clustering

Many advanced broker features and client options


Dramatically simplified administration

1.2 Why and When use ActiveMQ
Loose coupling

Coupling
refers to the interdependence of two or more applications or systems.

Application one in figure 1.2 sends a message to the MOM in a one-way fashion.
Then, possibly sometime later, application two receives a message from the MOM, in a
one-way fashion. Neither application has any knowledge that the other even exists,
and there’s no timing between the two applications. This one-way style of interaction
results in much lower maintenance because changes in one application have little to
no effect on the other application.


When to use ActiveMQ
Heterogeneous application integration

As a replacement for RPC:
Systems that rely upon synchronous
requests typically have a limited ability to scale because eventually requests will
begin to back up, thereby slowing the whole system. Instead of experiencing
this type of a slowdown, using asynchronous messaging, additional message
receivers can be easily added so that messages are consumed concurrently and
therefore handled faster.


To improve application scalability


2.What’s message-oriented middleware?
Message-oriented middleware (MOM) is best described as a category of software for
communication in an asynchronous, loosely-coupled, reliable, scalable, and secure
manner among distributed applications or systems. MOMs were an important concept
in the distributed computing world.

MOMs added welcome additional features to enterprise messaging that weren’t
previously possible when systems were tightly coupled—features such as message persistence,
robust communication over slow or unreliable connections, complex message
routing, message transformation, and much more



2.3 What’s the Java Message Service?
The Java Message Service (JMS) moved beyond vender-centric MOM APIs to provide an
API for enterprise messaging. JMS aims to provide a standardized API to send and
receive messages using the Java programming language in a vendor-neutral manner.

In standardizing the API, JMS formally defined many concepts and artifacts from
the world of messaging:
 JMS client —An application is written using 100% pure Java to send and receive
messages.
 Non-JMS client —An application is written using the JMS provider’s native client
API to send and receive messages instead of JMS.
 JMS producer—A client application that creates and sends JMS messages.
 JMS consumer—A client application that receives and processes JMS messages.
 JMS provider—The implementation of the JMS interfaces, which is ideally written
in 100% pure Java.
 JMS message—The most fundamental concept of JMS; sent and received by JMS
clients.
 JMS domains—The two styles of messaging that include point-to-point and publish/
subscribe.
 Administered objects—Preconfigured JMS objects that contain provider-specific
configuration data for use by clients. These objects are typically accessible by clients
via JNDI.
 Connection factory—Clients use a connection factory to create connections to the
JMS provider.
 Destination—An object to which messages are addressed and sent and from
which messages are received.
















