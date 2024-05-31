# ResponseTime

Let's say it takes 50ms for Rabbit to take a message from this queue, put it on the network and for it to arrive at the consumer. It takes 4ms for the client to process the message. Once the consumer has processed the message, it sends an ack back to Rabbit, which takes a further 50ms to be sent to and processed by Rabbit. So we have a **total round trip time of 104ms**. If we have a QoS prefetch setting of 1 message then Rabbit won't sent out the next message until after this round trip completes. Thus the **client will be busy for only 4ms of every 104ms**, or **3.8%** of the time. 
If we do total round trip time / processing time on the client for each message, we get **104 / 4 = 26 messages**

Using it is pretty much the same as the normal QueueingConsumer except that you should provide three extra parameters to the constructor to get the best performance:
- [x] The first is **requeue** which says whether, when messages are nacked, should they be requeued or discarded. If false, they will be discarded which may trigger the dead letter exchange mechanisms if they're set up.
- [x] The second is the **targetDelay** which is the acceptable time in milliseconds for messages to wait in the client-side QoS prefetch buffer.
- [x] The third is the **interval** and is the expected worst case processing time of one message in milliseconds. This doesn't have to be spot on, but within an order of magnitude certainly helps.


## Calculate ResTime on the level of a cluster

The federation plugin can transmit messages between brokers (or clusters) in different administrative domains.