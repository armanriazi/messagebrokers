# Queues

## Models of queues

- [x] Mirror/Classic
- [x] Quorum
- [x] Stream

streams may be a better option than quorum queues.

- [quorum vs mirros queues](https://www.rabbitmq.com/docs/quorum-queues#feature-comparison)

In AMQP 0-9-1, queues can be declared as **durable or transient**. Metadata of a durable queue is stored on disk, while metadata of a transient queue is stored in memory when possible.

So, the default **QoS prefetch** setting gives clients an unlimited buffer, and that can result in poor behaviour and performance.

*Delivered messages can be acknowledged by consumer explicitly or automatically* as soon as a delivery is written to connection socket.
**Automatic acknowledgement** mode generally will *provide higher throughput rate* and uses less network bandwidth. However, it offers the least number of guarantees when it comes to failures. As a rule of thumb, consider using **manual acknowledgement mode** first.

## Metrics and Monitoring

RabbitMQ collects multiple metrics about queues. Most of them are available via RabbitMQ HTTP API and management UI, which is designed for monitoring. This includes queue length, ingress and egress rates, number of consumers, number of messages in various states (e.g. ready for delivery or unacknowledged), number of messages in RAM vs. on disk, and so on.
rabbitmqctl can list queues and some basic metrics.
Runtime metrics such as VM scheduler usage, queue (Erlang) process GC activity, amount of RAM used by the queue process, queue process mailbox length can be accessed using the **rabbitmq-top plugin** and individual queue pages in the management UI.

## Persistence (Durable Storage) in Classic Queues

**Classic queues use an on-disk index** for storing message locations on disk as well as a message store for persisting messages.
Both persistent and transient messages are always persisted to disk except when:

- [x] the queue is declared as transient or messages are **transient**
- [x] messages are smaller than the embedding threshold **(defaults to 4096 bytes)**
- [x] for RabbitMQ 3.12 and later versions: the queue is short (queues may **keep up to** #2048 **messages** in memory at most, depending on the consumer delivery rate)

