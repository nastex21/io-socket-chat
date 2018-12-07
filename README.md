Advanced Node and Express - Send and Display Chat Messages

It's time you start allowing clients to send a chat message to the server to emit to all the clients! Already in your client.js file you should see there is already a block of code handling when the messgae form is submitted! 
```
($('form').submit(function(){ /*logic*/ });)
```
Within the code you're handling the form submit you should emit an event after you define 'messageToSend' but before you clear the text box #m. The event should be named 'chat message' and the data should just be 'messageToSend'. socket.emit('chat message', messageToSend);

Now on your server you should be listening to the socket for the event 'chat message' with the data being named 'message'. Once the event is received it should then emit the event 'chat message' to all sockets io.emit with the data being an object containing 'name' and 'message'.

On your client now again, you should now listen for event 'chat message' and when received, append a list item to #messages with the name a colon and the message!

At this point the chat should be fully functional and sending messages across all clients! Submit your page when you think you've got it right. If you're running into errors, you can check out the project up to this point here for the server and here for the client.
