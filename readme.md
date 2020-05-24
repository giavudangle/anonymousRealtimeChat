# Anonymous Real-time Chat demo Socket.io

## Introduction

> This is anonymous chat app was created use Nodejs, Express, and Socket.io and MongoDB.

You should have a good understanding of how socket.io works at the end of this repo or after taking a look at the code.

You will also learn how to show that someone is typing in a chat application.

Here is a screenshot of it looks and functionality.

![alt text]("https://github.com/giavudangle/anonymousRealtimeChat/blob/master/screenshots/chatscreenshot.gif")

## Code Samples

> Backend 

```javascript
//integrating socketio
socket = io(http);

//database connection
const Chat = require("./models/Chat");
const connect = require("./dbconnect");

//setup event listener
socket.on("connection", socket => {
 console.log("user connected");

 socket.on("disconnect", function() {
   console.log("user disconnected");
 });

 //Someone is typing
 socket.on("typing", data => {
   socket.broadcast.emit("notifyTyping", {
     user: data.user,
     message: data.message
   });
 });

```

> Frontend ( Dont forget to import socket library front end :))

```javascript
(function() {
  $("form").submit(function(e) {
    let li = document.createElement("li");
    e.preventDefault(); // prevents page reloading
    socket.emit("chat message", $("#message").val());

    messages.appendChild(li).append($("#message").val());
    let span = document.createElement("span");
    messages.appendChild(span).append("by " + "Anonymous" + ": " + "just now");

    $("#message").val("");

    return false;
  });

  socket.on("received", data => {
    let li = document.createElement("li");
    let span = document.createElement("span");
    var messages = document.getElementById("messages");
    messages.appendChild(li).append(data.message);
    messages.appendChild(span).append("by " + "anonymous" + ": " + "just now");
    console.log("Hello bingo!");
  });
})();
```

## Installation

> Clone this repository and run

```bash
npm install 

```

Then run:

```bash
npm start
```

goto your browser

and visit localhost:3000 and start chatting.

Note:

You should have mongoDB installed and started for this application to work correctly.
If you want to demo-deploy try to use NGROK to map localhost -> public link .

In package.json add a script
```
 "server": " ngrok http 3000"
```
