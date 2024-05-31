
```javascript
app.get('/', (req, res) => {
 open.then((conn) => {
  return conn.createChannel();
 }).then(function(ch) {
  let q = 'test';

  return ch.assertQueue(QUEUE_NAME).then(function(ok) {
   if (ok.messageCount == 0) {
    return NO_MESSAGES;
   }

   return ch.get(QUEUE_NAME, (msg) => {
    if (msg !== null) {
     ch.ack(msg);
    }
   });
  });
 }).then((msg) => {
  if (msg === NO_MESSAGES) {
   res.send({ message: "No messages. Waiting..." });
  } else {
   res.send({ message: `Message received: ${msg.content.toString()}` });
  }
 }).catch(console.warn);
});
```