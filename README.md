Advanced Node and Express - Authentication with Socket.IO

Currently, you cannot determine who is connected to your web socket. While 'req.user' containers the user object, thats only when your user interacts with the web server and with web sockets you have no req (request) and therefor no user data. One way to solve the problem of knowing who is connected to your web socket is by parsing and decoding the cookie that contains the passport session then deserializing it to obtain the user object. Luckily, there is a package on NPM just for this that turns a once complex task into something simple!

Add 'passport.socketio' as a dependency and require it as 'passportSocketIo'.

Now we just have to tell Socket.IO to use it and set the options. Be sure this is added before the existing socket code and not in the existing connection listener. For your server it should look as follows:
```
io.use(passportSocketIo.authorize({
  cookieParser: cookieParser,
  key:          'express.sid',
  secret:       process.env.SESSION_SECRET,
  store:        sessionStore
}));
```
You can also optionally pass 'success' and 'fail' with a function that will be called after the authentication process completes when a client trys to connect.

The user object is now accessible on your socket object as socket.request.user. For example, now you can add the following: console.log('user ' + socket.request.user.name + ' connected'); and it will log to the server console who has connected!
