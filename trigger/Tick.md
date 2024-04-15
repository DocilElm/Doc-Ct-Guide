# [Tick](https://www.chattriggers.com/javadocs/-chat-triggers/com.chattriggers.ctjs.engine/-i-register/register-tick.html) Trigger
This runs the given function every tick **(20 times)**.<br>

## Checking scoreboard
This will check whether the player is in hypixel using the scoreboard
```js
let inHypixel = false

register("tick", () => {
    // Avoid checking if world is not loaded
    // because then scoreboard is not loaded
    // and also avoid checking if we are in hypixel
    if (!World.isLoaded() || inHypixel) return

    // Getting the scoreboard lines
    // then looping through each one of them
    Scoreboard.getLines().forEach(line => {
        // Getting the name of the line (aka the text)
        // Then removing the formatting so we can actually
        // check it with a string
        const name = line.getName()?.removeFormatting()

        inHypixel = name.includes("www.hypixel")
    })
})
```

## Checking tablist
This will check whether the player is in tablist.
```js
let inTab = false

register("tick", () => {
    // Avoid checking if world is not loaded
    // because then tablist is not loaded
    // and also avoid checking if we are in the tablist
    if (!World.isLoaded() || inTab) return

    TabList.getNames().forEach(name => {
        const playerName = name.removeFormatting()

        // We use #toLowerCase just in case
        inTab = playerName.toLowerCase().includes(Player.getName().toLowerCase())
    })
})
```