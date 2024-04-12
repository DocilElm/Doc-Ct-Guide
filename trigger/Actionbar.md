# [ActionBar](https://www.chattriggers.com/javadocs/-chat-triggers/com.chattriggers.ctjs.engine/-i-register/register-action-bar.html) Trigger
This runs the given function every time a actionbar message is recieved.<br>
if a criteria is set it'll only run whenever the actionbar message recieved matches said criteria.<br>
This trigger essentially works the same as a [Chat](Chat.md) Trigger

## No criteria
This will only recieve the event of the message.
```js
register("actionBar", (event) => {
    ChatLib.chat(`actionbar event recieved: ${event}`)
    // prints the event into the chat
})
```
If we want to get the message recieved we'll have to get that ourselves **(this can be avoided by using criteria)**.<br>
### Getting a message from the Event

```js
const message = ChatLib.getChatMessage(event, false)
```

Params:
* (Event) Actionbar Event.
* (Boolean) Whether it should get the message formatted.

### No criteria with message event
Knowing all the above we can now use the Event to get the chat message.
```js
register("actionBar", (event) => {
    // we can leave the second param empty
    // this is because it defaults to false
    const message = ChatLib.getChatMessage(event)

    ChatLib.chat(`actionbar message recieved from event: ${message}`)
    // this will print "actionbar message recieved from event: 4,556/4,556❤     716❈ Defense     1,938/1,938✎ 600ʬ" into the chat
})
```

## Using criteria
This will recieve any captured message from the criteria.
```js
register("actionBar", (seconds) => {
    // This recieves "4,556/4,556❤     716❈ Defense     CASTING IN 3s"
    ChatLib.chat(`actionbar message recieved: ${seconds}`)
    // prints: "action message recieved: 3" into the chat
}).setCriteria("${*}CASTING IN ${seconds}s")
```
> [!TIP]
> The criteria does not need formatting **(mc color codes)** to work.

As we can see, the criteria will return the matched groups for this event without us having to get the message from the event.<br>
A couple things to take into consideration:
* Every capture group starts with ``${}`` and inside we define the name of this group.
* Using ``${*}`` will match the criteria but the captured group wont be passed through.
* You can also use regex as the criteria.

> [!NOTE]
> If the criteria does not have any matching groups it will return the Actionbar Event.