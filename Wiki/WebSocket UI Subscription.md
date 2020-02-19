## First approach (formal messaged declaration)
- Declare new message
```js
messages: {
    // Message name.
    "NewUserSet": {
        // Message type — broadcasting, without a specific subscriber.
        "mode": Terrasoft.MessageMode.BROADCAST,
        // Message direction — subscription.
        "direction": Terrasoft.MessageDirectionType.SUBSCRIBE
    }
}
``` 

- Overwrite init method to include message subscription
```js
methods: {
    init: function() {
        this.callParent(arguments);
        // Subscription to receiving the NewUserSet message.
        this.sandbox.subscribe("NewUserSet", this.onNewUserSet, this);
    }
}
```

- Create method (handler) to do print message content when the message is received
```js
// Receiving NewUserSet message event handler.
onNewUserSet: function(args) {
    // Saving the message content to local variables.
    var birthday = args.birthday;
    var name = args.name;
    // Displaying content in the console.
    window.console.info("Message received: NewUserSet. Data: name: " +
        name + "; birthday: " + birthday);
}
```

## Second approach (Terrasoft.EventName.ON_MESSAGE handler)
```js
init: function() {
    this.callParent(arguments);
    // Subscribe to ANY and ALL webSocketMessages
    Terrasoft.ServerChannel.on(Terrasoft.EventName.ON_MESSAGE, this.onMessageReceived, this);
}
```
- Handler, method has to handle message filtering and processing
```js
onMessageReceived: function(scope, message) {
    if (!message || message.Header.Sender !== "NewUserSet") {
        return;
    }   
    //Useful business logic here
    var r = JSON.parse(message.Body);
}
```

## Comparison
- [ ] When to use the first approach
    - [ ] A
    - [ ] B
    - [ ] C
- [ ] When to use the second approach
    - [ ] A
    - [ ] B
    - [ ] C


