Advanced Node and Express - Announce New Users

Many chat rooms are able to annouce when a user connects or disconnects and then display that to all of the connected users in the chat. Seeing as though you already are emitting an event on connect and disconnect, you will just have to modify this event to support such feature. The most logical way of doing so is sending 3 pieces of data with the event: name of the user connected/disconnected, the current user count, and if that name connected or disconnected.

Change the event name to 'user' and as the data pass an object along containing fields 'name', 'currentUsers', and boolean 'connected' (to be true if connection, or false for disconnection of the user sent). Be sure to make the change to both points we had the 'user count' event and set the disconnect one to sent false for field 'connected' instead of true like the event emitted on connect. io.emit('user', {name: socket.request.user.name, currentUsers, connected: true});

Now your client will have all the nesesary information to correctly display the current user count and annouce when a user connects or disconnects! To handle this event on the client side we should listen for 'user' and then update the current user count by using jQuery to change the text of #num-users to '{NUMBER} users online', as well as append a <li> to the unordered list with id 'messages' with '{NAME} has {joined/left} the chat.'.

An implementation of this could look like the following:
```
socket.on('user', function(data){
  $('#num-users').text(data.currentUsers+' users online');
  var message = data.name;
  if(data.connected) {
    message += ' has joined the chat.';
  } else {
    message += ' has left the chat.';
  }
  $('#messages').append($('<li>').html('<b>'+ message +'<\/b>'));
});
```
