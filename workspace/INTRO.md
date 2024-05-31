# Introductory 

## Protocols

`Port 5672`: AMQP 0-9-1 protocol, used for client-broker communication
`Port 15672`: HTTP/HTTPS protocol, used for web management interface

‍‍‍```bash
curl -u guest:guest localhost:15672/api/overview
‍‍‍```

## Setup

### Docker

```bash
docker run -d --hostname localhost --network=gateway --name localhost_rabbit13 -p 8080:15672 -p 5672:5672 -p 25676:25676 rabbitmq:3-management
```