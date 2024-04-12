# [PacketRecieved](https://www.chattriggers.com/javadocs/-chat-triggers/com.chattriggers.ctjs.engine/-i-register/register-packet-received.html) Trigger
This runs the given function every time a packet is sent to the client from the server.<br>
The trigger can be filtered by the packet class.

## Detecting every packet
This will run every time **ANY** packet is recieved.
```js
register("packetReceived", (packet, event) => {
    // Code here
})
```

## Detecting block change
This will run whenever a block change packet is recieved.
```js
register("packetReceived", (packet, event) => {
    const blockPos = packet.func_179827_b() // getBlockPosition
    const blockState = packet.func_180728_a() // getBlockState

    ChatLib.chat(`detected block change packet: ${blockPos} ${blockState}`)
}).setFilteredClass(net.minecraft.network.play.server.S23PacketBlockChange)
```

## Detecting window open
This will run whenever a window open packet is recieved.
```js
register("packetReceived", (packet, event) => {
    // Removing the formatting just in case
    const windowTitle = packet.func_179840_c().func_150254_d().removeFormatting() // getWindowTitle

    ChatLib.chat(`open window detected: ${windowTitle}`)
}).setFilteredClass(net.minecraft.network.play.server.S2DPacketOpenWindow)
```

> [!TIP]
> All of the server packets start with: **net.minecraft.network.play.server**.