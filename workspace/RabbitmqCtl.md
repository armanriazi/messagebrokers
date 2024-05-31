# RabbitmqCtl

‍‍‍```bash
rabbitmqctl help
‍‍‍```

‍‍‍```bash
rabbitmqctl -n rabbit@451f4ab695e9 [Put-in a command after executed help command]
‍‍‍```

```bash
rabbitmq-diagnostics -s listeners

Interface: [::], port: 15672, protocol: http, purpose: HTTP API
Interface: [::], port: 15692, protocol: http/prometheus, purpose: Prometheus exporter API over HTTP
Interface: [::], port: 25672, protocol: clustering, purpose: inter-node and CLI tool communication
Interface: [::], port: 5672, protocol: amqp, purpose: AMQP 0-9-1 and AMQP 1.0
```

```bash
rabbitmq-plugins list

Listing plugins with pattern ".*" ...
 Configured: E = explicitly enabled; e = implicitly enabled
 | Status: * = running on rabbit@451f4ab695e9
 |/
[E*] rabbitmq_amqp1_0                  3.13.1
[  ] rabbitmq_auth_backend_cache        (pending upgrade to 3.13.1)
[  ] rabbitmq_auth_backend_http         (pending upgrade to 3.13.1)
[  ] rabbitmq_auth_backend_ldap         (pending upgrade to 3.13.1)
[  ] rabbitmq_auth_backend_oauth2       (pending upgrade to 3.13.1)
[  ] rabbitmq_auth_mechanism_ssl        (pending upgrade to 3.13.1)
[  ] rabbitmq_consistent_hash_exchange  (pending upgrade to 3.13.1)
[E*] rabbitmq_event_exchange           3.13.1
[e*] rabbitmq_federation               3.13.1
[  ] rabbitmq_federation_management     (pending upgrade to 3.13.1)
[  ] rabbitmq_jms_topic_exchange        (pending upgrade to 3.13.1)
[E*] rabbitmq_management               3.13.1
[e*] rabbitmq_management_agent         3.13.1
[  ] rabbitmq_mqtt                      (pending upgrade to 3.13.1)
[  ] rabbitmq_peer_discovery_aws        (pending upgrade to 3.13.1)
[  ] rabbitmq_peer_discovery_common     (pending upgrade to 3.13.1)
[  ] rabbitmq_peer_discovery_consul     (pending upgrade to 3.13.1)
[  ] rabbitmq_peer_discovery_etcd       (pending upgrade to 3.13.1)
[  ] rabbitmq_peer_discovery_k8s        (pending upgrade to 3.13.1)
[E*] rabbitmq_prometheus               3.13.1
[  ] rabbitmq_random_exchange           (pending upgrade to 3.13.1)
[  ] rabbitmq_recent_history_exchange   (pending upgrade to 3.13.1)
[  ] rabbitmq_sharding                  (pending upgrade to 3.13.1)
[  ] rabbitmq_shovel                    (pending upgrade to 3.13.1)
[  ] rabbitmq_shovel_management         (pending upgrade to 3.13.1)
[E*] rabbitmq_stomp                    3.13.1
[E*] rabbitmq_stream                   3.13.1
[  ] rabbitmq_stream_management         (pending upgrade to 3.13.1)
[  ] rabbitmq_top                       (pending upgrade to 3.13.1)
[E*] rabbitmq_tracing                  3.13.1
[  ] rabbitmq_trust_store               (pending upgrade to 3.13.1)
[e*] rabbitmq_web_dispatch             3.13.1
[  ] rabbitmq_web_mqtt                  (pending upgrade to 3.13.1)
[  ] rabbitmq_web_mqtt_examples         (pending upgrade to 3.13.1)
[  ] rabbitmq_web_stomp                 (pending upgrade to 3.13.1)
[  ] rabbitmq_web_stomp_examples        (pending upgrade to 3.13.1)
```

Plugin of `rabbitmq_web_stomp` is a good choice to enable it by using the web applications.

```bash
rabbitmqctl -n rabbit@451f4ab695e9 set_log_level debug
```

```bash
rabbitmq-diagnostics consume_event_stream | jq
```

To make sure your ran amqp have worked properly, you can use tools of Vuls/NMAP.

- [Vuls](https://vuls.io)

‍‍‍‍‍‍‍‍‍```bash
nmap -sV -Pn -n -T4 -p 5672 --script amqp-info <IP>

PORT     STATE SERVICE VERSION
5672/tcp open  amqp    RabbitMQ 3.1.5 (0-9)
| amqp-info: 
|   capabilities: 
|     publisher_confirms: YES
|     exchange_exchange_bindings: YES
|     basic.nack: YES
|     consumer_cancel_notify: YES
|   copyright: Copyright (C) 2007-2013 GoPivotal, Inc.
|   information: Licensed under the MPL.  See http://www.rabbitmq.com/
|   platform: Erlang/OTP
|   product: RabbitMQ
|   version: 3.1.5
|   mechanisms: PLAIN AMQPLAIN
|_  locales: en_US
```


After running the code of `return new Rabbit(connection, channel, replyQueue)`
Retrive as random queue by Rabbitmq service.

> "amq.gen-hMwJdOy_-toXdk5dn0LdMg"

#gateway 

```bash
rabbitmqctl list_queues exclusive durable auto_delete  state name | grep amq | sort -n
```
