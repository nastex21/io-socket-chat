Advanced Node and Express - Communicate by Emitting

Emit is the most common way of communicating you will use. When you emit something from the server to 'io', you send an event's name and data to all the connected sockets. A good example of this concept would be emitting the current count of connected users each time a new user connects!

Start by adding a variable to keep track of the users just before where you are currently listening for connections. var currentUsers = 0;

Now when someone connects you should increment the count before emitting the count so you will want to add the incrementer within the connection listener. ++currentUsers;

Finally after incrementing the count, you should emit the event(still within the connection listener). The event should be named 'user count' and the data should just be the 'currentUsers'. io.emit('user count', currentUsers);

Now you can implement a way for your client to listen for this event! Similarly to listening for a connection on the server you will use the on keyword.

```
socket.on('user count', function(data){
  console.log(data);
});
```

Now try loading up your app and authenticate and you should see in your client console '1' representing the current user count! Try loading more clients up and authenticating to see the number go up.
