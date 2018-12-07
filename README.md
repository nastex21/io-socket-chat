Advanced Node and Express - Handle a Disconnect

You may notice that up to now you have only been increasing the user count. Handling a user disconnecting is just as easy as handling the initial connect except the difference is you have to listen for it on each socket versus on the whole server.

To do this, add in to your existing connect listener a listener that listens for 'disconnect' on the socket with no data passed through. You can test this functionality by just logging to the console a user has disconnected. socket.on('disconnect', () => { /*anything you want to do on disconnect*/ });

To make sure clients continuously have the updated count of current users, you should decrease the currentUsers by 1 when the disconnect happens then emit the 'user count' event with the updated count!

Note
Just like 'disconnect', all other events that a socket can emit to the server should be handled within the connecting listener where we have 'socket' defined.
