# Direct Publish/Subscribe

This tutorial assumes you’ve already reviewed the basic concepts found in the [Hello World](../HelloWorld) tutorial. This tutorial expands on those, and increases the performance.

Note that these samples are using **Direct Messaging**, Solace’s “at-most-once” or “best-effort” quality of service.  This is in contrast with **Guaranteed** Messaging, or _persistent_ messaging, which offers a high quality-of-service in terms of reliability and guarantees against message loss if used correctly.

Use of Direct Messaging is great for:
- Introductory applications like this one
- *High performance* applications where every millisecond (or even microsecond) count!
- Compatibility with Internet of Things (IoT) applications that use MQTT QoS 0, at-most-once delivery
- Applications that can tolerate some message loss in failure scenarios:
    - Low-value data (e.g. temperature sensor publishing every second)
    - Real-time requirement, where cached/buffered/delayed data is useless
    - Use of sequence numbers to detect gaps
    - Local caches / datagrids available to fetch lost data


## 1. DirectSubscriber

For Direct messages to be received, a consumer/subscriber application must be online (connected to a PubSub+ event broker) and subscribed to the appropriate topics. If there is a requirement that a consumer receives all messages that were sent, even when offline, then consider looking at the Guaranteed Pub/Sub samples.

So we'll start by looking at the `DirectSubscribe` sample application.

### 1. a) Connection Options

[![image](img/1.png)](https://github.com/SolaceSamples/solace-samples-java-jcsmp/blob/275739cb858cacea5140c5c7c8310cfb50868695/src/main/java/com/solace/samples/jcsmp/patterns/DirectSubscriber.java#L51-L63)

As with the `HelloWorld` sample, the `DirectSubscriber` reads connection parameters from command line.  Some additional connection parameters include changing the default values of reconnection attributes "retries per host" and "reconnect retries".  For more info on reconnection parameters, check [this section of the Developers Guide](https://docs.solace.com/Solace-PubSub-Messaging-APIs/API-Developer-Guide/Configuring-Connection-T.htm).


### 1. b) `onReceive()` callback

[![image](img/2.png)](https://github.com/SolaceSamples/solace-samples-java-jcsmp/blob/275739cb858cacea5140c5c7c8310cfb50868695/src/main/java/com/solace/samples/jcsmp/patterns/DirectSubscriber.java#L76-L89)

This time, in the callback handler that the API runs when it receives a message, rather than printing it out to the console (which is quite slow), we will simply increment an integer counter to keep track of how many messages have been received.

There are many methods, checks, and properties you can query on the received message.  As an example, you may want to check if the message has a discard flag indication set.  This is available on most Solace native APIs, and returns true if at least one Direct message was discarded by the broker before receiving this message.  This can happen if the publisher is publishing too fast, or this subscriber is too slow.










