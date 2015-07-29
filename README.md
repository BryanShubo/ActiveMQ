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




2.4 JMS Message
A JMS message allows anything to be sent as part of the message, including text and binary data
as well as information in the headers

A JMS message:
headers(used by both client and JMS providers) + a payload (textual and binary data)

Headers:
JMSDestination
JMSDeliveryMode: 
       1) persistent(default) A JMS provider must deliver a persistent message once
          and only once.
       2) nonpersistent: A JMS provider must deliver a nonpersistent message at most once.

JMSExpiration: time to live is zero by default, meaning that the message won't expire.
JMSMessageID: A string that uniquely identifies a message that’s assigned by the
              JMS provider and must begin with ID
JMSPriority: * Priorities 0–4—These priorities are finer granularities of the normal priority.
             * Priorities 5–9—These priorities are finer granularities of expedited priority.
JMSTimestamp: 


JMS MESSAGE PROPERTIES
Properties are simply additional headers that can be specified on a message. JMS provides
the ability to set custom headers using generic methods. Methods are provided
for working with many primitive Java types for header values including Boolean, byte,
short, int, long, float, double, and also the String object type. Examples of these methods
can be seen in the next listing, taken from the Message interface.

There are three types of properties: 
custom properties, 
JMS defined properties,
provider-specific properties.

2.4.6 Message selector
Message selectors allow a JMS client to specify which messages it wants to receive
from a destination based on values in message headers (each message contains a property that identifies the stock symbol of interest.)


Message body:
JMS defines six Java types for the message body, also known as the payload.
1) Message—The base message type. Used to send a message with no payload, only
headers and properties. Typically used for simple event notification.
2) TextMessage —A message whose payload is a String. Commonly used to send simple textual and XML data.
3) MapMessage —Uses a set of name/value pairs as its payload. The names are of type String and the values are a Java primitive type.
4) BytesMessage —Used to contain an array of uninterpreted bytes as the payload.
5) StreamMessage—A message with a payload containing a stream of primitive Java types that’s filled and read sequentially.
6) ObjectMessage—Used to hold a serializable Java object as its payload. Usually used for complex Java objects. Also supports Java collections.


2.4.7 JMS Domains
1) Point to point (queues)
a. messages are sent and received either synchronously or
asynchronously.
b. Each message received on the queue is delivered once and only
once to a single consumer.
c. The queue stores all messages until they’re delivered or until
they expire.

2) Publish / subscribe (topics)
subscribers register to
receive messages from the topic either synchronously using the Message-
Consumer.receive() method or asynchronously by registering a MessageListener
implementation using the MessageConsumer.setMessageListener() method.

Using a durable subscription, when a subscriber disconnects
from the JMS provider, it’s the responsibility of the JMS provider to store messages
for the subscriber.Durable subscriptions allow for subscriber
disconnection without missing any messages.


DISTINGUISHING MESSAGE DURABILITY FROM MESSAGE PERSISTENCE
1) Message durability can only be achieved with
the pub/sub domain.
2) Message persistence is independent of the message domain. Message persistence is a
quality of service property used to indicate the JMS application’s ability to handle
missing messages in the event of a JMS provider failure.


Request/reply messaging in JMS applications: 
The convenience classes for handling basic request/reply are the QueueRequestor
and the TopicRequestor. These classes provide a request() method that sends a
request message and waits for a reply message through the creation of a temporary
destination where only one reply per request is expected. These classes are useful
only for this most basic form of request/reply, as shown in figure 2.8—one reply per
request.


2.4.8 Administered objects: ConnectionFactory and Destination


2.5 Using the JMS APIs to create JMS applications
2.5.1 JMS application
1) Acquire a JMS connection factory
2) Create a JMS connection using the connection factory
3) Start the JMS connection
4) Create a JMS session from the connection
5) Acquire a JMS destination
6) Create a JMS producer, OR
                 a Create a JMS producer
                 b Create a JMS message and address it to a destination
7) Create a JMS consumer
                 a Create a JMS consumer (sync)
                 b Optionally register a JMS message listener(async)
8) Send or receive JMS message(s)
9) Close all JMS resources (connection, session, producer, consumer, and so forth)


A note on multithreading in JMS applications
The JMS spec specifically defines concurrency for various objects in the JMS API and
requires that only a few objects support concurrent access. The ConnectionFactory,
Connection, and Destination objects are required to support concurrent access,
whereas the Session, MessageProducer, and MessageConsumer objects don’t support
concurrent access. The point is that the Session, MessageProducer, and
MessageConsumer objects shouldn’t be shared across threads in a Java applicatio


2.5.2 Message-Driven Beans
















