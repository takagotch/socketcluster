### socketcluster
---
https://github.com/SocketCluster/socketcluster

```sh
npm install -g socketcluster
sudo npm install -g socketcluster
socketcluster create myapp
node server
curl http://localhost:8000/
npm install socketcluster
npm install soketcluster-client

docker run -d /home/tky/controllers/:/usr/src/controllers/ -p 8000:8000 -e "SOCKETCLUSTER_WORKER_CONTROLLER=/usr/src/controllers/worker.js" socketcluster/socketcluster

socketcluster create myApp
node server.js
```

```js
var socketCluster = new SocketCluster({
  workers: 3,
  brokers: 3,
  port: 8000,
  appName: 'myapp',
  workerController: 'worker.js',
  protocol: 'https',
  protocolOptions: {
    key: fs.readFileSync(__dirname + '/keys/enc_key.pem', 'utf8'),
    cert: fs.readFileSync(__dirname + '/keys/cert.pem', 'utf8'),
    passphrase: 'passphase4privkey'
  }
});

var socket = socketCluster.create();
socket.emit('sampleClientEvent', {message: 'This is an object with a message property'})

var SocketCluster = require('socketcluster');
var socketCluster = new SocketCluster({
  workers: 1,
  brokers: 1,
  port: 8000,
  appName: 'myapp',
  
  wsEngine: 'ws',
  
  workerController: __dirname + '/worker.js',
  
  brokerController: __dirname + '/broker.js',
  
  rebootWorkerOnCrash: true
});

app.use(serveStatic(__dirname + '/public'));
httpServer.on('req', app);

var count = 0;
scServer.on('connection', function (socket){
  socket.on('ping', function (data) {
    count++;
    console.log('PING', data);
    scServer.exchange.publish('pong', count);
  });
});

socket.emit('ping', 'This is a PING message');

scServer.exchange.publish('pong', count);

var pongChannel = socket.subscribe('pong');
pongChannel.watch(function (count) {
  console.log('Client received data from pong channel:', count);
});

socket.unsubscribe('pong');

socket.publish('pong', 'This PONG event comes from a client');
pongChannel.publish('This PONG event comes from a client');

scServer.exchange.publish('foo', 123);
```

```dockerfile
FROM socketcluster/socketcluster
MAINTAINER Tky

LABEL version="1.0.0"
LABEL description="custom app based on SocketCluster"

WORKDIR /usr/src/
COPY . /usr/src/

RUN npm install

EXPOSE 8000

CMD ["npm", "start"]
```

```json
{
  hostname: 'securedomain.com',
  secure: true,
  port: 443,
  rejectUnauthorized: false
}
```
