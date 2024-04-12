# [Chat](https://www.chattriggers.com/javadocs/-chat-triggers/com.chattriggers.ctjs.engine/-i-register/register-chat.html) Trigger
This triggers the given function every time a chat message is recieved **(not client side)**.<br>
if a criteria is set it'll only run whenever the chat message recieved matches said criteria.

## No criteria
This will only recieve the event of the message.
```js
register("chat", (event) => {
    ChatLib.chat(`chat event recieved: ${event}`)
    // prints the event into the chat
})
```
If we want to get the message recieved we'll have to get that ourselves **(this can be avoided by using criteria)**.<br>
### Getting a message from the Event

```js
const message = ChatLib.getChatMessage(event, false)
```

Params:
* (Event) Chat Event.
* (Boolean) Whether it should get the message formatted.

### No criteria with message event
Knowing all the above we can now use the Event to get the chat message.
```js
register("chat", (event) => {
    // we can leave the second param empty
    // this is because it defaults to false
    const message = ChatLib.getChatMessage(event)

    ChatLib.chat(`message recieved from event: ${message}`)
    // this will print "message recieved from event: [410] ➶ [MVP+] DocilElm: a" into the chat
})
```

## Using criteria
This will recieve any captured message from the criteria.
```js
register("chat", (level, rank, name, message) => {
    // This recieves "[410] ➶ [MVP+] DocilElm: a"
    ChatLib.chat(`chat message recieved: ${level} ${rank} ${name} ${message}`)
    // prints: "chat message recieved: 410 MVP+ DocilElm a" into the chat
}).setCriteria("${level} ${*}${rank}${name}: ${message}")
```
> [!TIP]
> The criteria does not need formatting **(mc color codes)** to work.

As we can see, the criteria will return the matched groups for this event without us having to get the message from the event.<br>
A couple things to take into consideration:
* Every capture group starts with ``${}`` and inside we define the name of this group.
* Using ``${*}`` will match the criteria but the captured group wont be passed through.
* You can also use regex as the criteria.

> [!NOTE]
> If the criteria does not have any matching groups it will return the Chat Event.