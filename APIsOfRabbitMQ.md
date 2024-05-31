# APIs of rabbitmq-management

Based on the followed link let's extract some tips:

- [APIs of rabbitmq-management](https://raw.githack.com/rabbitmq/rabbitmq-management/rabbitmq_v3_5_6/priv/www/api/index.html)

To make a request put in `http://localhost:15672/api/{followed api names}`

Might be you need to leave username and password of guest at header request.

## Note
For some application code that I have worked I set a hashtag like:

> `#gateway getMessageCount: {requeue:false}`

[rabbitmq](https://github.com/armanriazi/rabbitmq) use Amqp-0-9-1 version of amqp Rabbitmq with amqplib in the NodeJS.

## /whoami

Details of the currently authenticated user.

#gateway By Axios GET

## /aliveness-test/vhost 	

Declares a test queue, then publishes and consumes a message. Intended for use by monitoring tools. If everything is working correctly, will return HTTP status 200 with body:

```json
{"status":"ok"}
```

Note: the test queue will not be deleted (to to prevent queue churn if this is repeatedly pinged). 

#gateway By Axios GET

## /vhosts/yourDesireName

#gateway By Axios POST it without body on the initialization of your app.

## /permissions/vhost/user

#gateway By Axios Get it to know if you have read, write, or configure access or not.

## /policies/vhost/name 	

An individual policy. To PUT a policy, you will need a body looking something like this:

```json
{"pattern":"amq.gen-*", "definition": {"amq-gen":"all"}, "priority":0, "apply-to": "all"}
```

pattern and definition are mandatory, priority and apply-to are optional. 

#gateway By Axios PUT it with body and then check it if is there a old policy or not.

## /vhosts 	

A list of all vhosts.

#gateway By Axios GET to find total count of vhosts.

## /nodes 	

A list of nodes in the RabbitMQ cluster.

#gateway By Axios GET to find total count of nodes.

## /queues/vhost 	

A list of all queues in a given virtual host.

#gateway By Axios GET to find total count of queues of a vhost.

## /queues/vhost/name/contents 	

Contents of a queue. DELETE to purge. Note you can't GET this.

#gateway By Axios DELETE to purge a name service queue. Do it on step of initilization.

## /queues/vhost/name 	

An individual queue. To PUT a queue, you will need a body looking something like this:

```json
{"auto_delete":false,"durable":true,"arguments":{},"node":"rabbit@smacmullen"}
```

All keys are optional. This API doesn't have POST method supportation by RabbitMq.

When DELETEing a queue you can add the query string parameters if-empty=true and / or if-unused=true. These prevent the delete from succeeding if the queue contains messages, or has consumers, respectively. 

#gateway By Axios PUT to review above json when you use amqplib.

## /queues/vhost/name/get

Get messages from a queue. (This is not an HTTP GET as it will alter the state of the queue.) **You should post a body looking like**:

```json
{"count":5,"requeue":true,"encoding":"auto","truncate":50000}
```

- [x] **count** controls *the maximum number of messages to get*. You may get fewer messages than this if the queue cannot immediately provide them.
- [x] **requeue** determines whether the messages will be *removed from the queue*. If requeue is true they will be requeued - but their redelivered flag will be set.
- [x] **encoding** must be either "auto" (in which case the payload will be returned as *a string if it is valid UTF-8*, and base64 encoded otherwise), or *"base64"* (in which case the payload will always be base64 encoded).
    If truncate is present it will truncate the message payload if it is larger than the size given (in bytes).
- [x] **truncate** is *optional*; all other keys are mandatory.

**Please note** that the get path in the *HTTP API is intended for diagnostics* etc - it does not implement reliable delivery and so should be treated *as a sysadmin's tool rather than a general API for messaging.* 

#gateway In the getMessageCount() method, adding this params: {"count": 2048, "requeue":false,"encoding":"auto"}

Why we use #2048 ? find it by hashtag.
