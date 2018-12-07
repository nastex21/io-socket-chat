Advanced Node and Express - Set up the Environment

Add Socket.IO as a dependency and require/instantiate it in your server defined as 'io' with the http server as an argument. const io = require('socket.io')(http);

The first thing needing to be handled is listening for a new connection from the client. The on keyword does just that- listen for a specific event. It requires 2 arguments: a string containing the title of the event thats emitted, and a function with which the data is passed though. In the case of our connection listener, we use socket to define the data in the second argument. A socket is an individual client who is connected.

For listening for connections on our server, add the following between the comments in your project:
```
io.on('connection', socket => {
  console.log('A user has connected');
});
```

Now for the client to connect, you just need to add the following to your client.js which is loaded by the page after you've authenticated:
```
/*global io*/
var socket = io();
```
The comment suppresses the error you would normally see since 'io' is not defined in the file. We've already added a reliable CDN to the Socket.IO library on the page in chat.pug.

Now try loading up your app and authenticate and you should see in your server console 'A user has connected'!

Note
io() works only when connecting to a socket hosted on the same url/server. For connecting to an external socket hosted elsewhere, you would use io.connect('URL');.
