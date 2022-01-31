# Direct Publish/Subscribe

This tutorial assumes you’ve already reviewed the basic concepts found in the [Hello World](../HelloWorld) tutorial, and will go into a bit more detail on the

Note that these samples are using Direct Messaging, Solace’s “at-most-once” or “best-effort” quality of service.  This is in contrast with Guaranteed Messaging, or persistent messaging, which offers a high-quality service in terms of reliability and guarantees against message loss if used correctly.
Using Direct Messaging is great for:
- Introductory applications like this one
- High performance applications where every millisecond (or even microsecond) count!
- Applications that can tolerate some message loss in failure scenarios:
    - Sequence numbers to detect gaps
    - Local caches available to resend data
    - Internet of Things (IoT) applications where data is constantly being published by, say, a temperature sensor or a connected car
    - Etc.

In the `Hello World` application, it both published and subscribed to messages.







