# [PacketSent](https://www.chattriggers.com/javadocs/-chat-triggers/com.chattriggers.ctjs.engine/-i-register/register-packet-sent.html) Trigger
This runs the given function every time a packet is sent from the client to the server.<br>
The trigger can be filtered by the packet class.

## Detecting every packet
This will run every time **ANY** packet is sent.
```js
register("packetSent", (packet, event) => {
    // Code here
})
```

## Detecting block breaking
This will run whenever a block breaking packet is sent.
```js
register("packetSent", (packet, event) => {
    const facing = packet.func_179714_b() // getFacing
    const position = packet.func_179715_a() // getPosition
    const status = packet.func_180762_c() // getStatus

    ChatLib.chat(`player digging detected: ${facing} ${position} ${status}`)
}).setFilteredClass(net.minecraft.network.play.client.C07PacketPlayerDigging)
```

## Detecting block placement
This will run whenever a block placement packet is sent.
```js
register("packetSent", (packet, event) => {
    const blockPosition = packet.func_179724_a() // getPosition
    const itemStack = packet.func_149574_g() // getStack

    ChatLib.chat(`block placement detected: ${blockPosition} ${itemStack}`)
}).setFilteredClass(net.minecraft.network.play.client.C08PacketPlayerBlockPlacement)
```

## Detecting closed window
This will run whenever a closing window packet is sent.
```js
register("packetSent", (packet, event) => {
    ChatLib.chat("window closed detected")
}).setFilteredClass(net.minecraft.network.play.client.C0DPacketCloseWindow)
```

> [!TIP]
> All of the client packets start with: **net.minecraft.network.play.client**.