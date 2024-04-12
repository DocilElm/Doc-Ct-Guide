# [Render World](https://www.chattriggers.com/javadocs/-chat-triggers/com.chattriggers.ctjs.engine/-i-register/register-render-world.html) Trigger
This runs the given function every frame.<br>
This is usually used to make 3D **(in world)** rendering.

## Drawing a text in world
This will draw a text in the world with position (x: PlayerX + 1, y: PlayerY + 2, z: PlayerZ + 1)
```js
register("renderWorld", () => {
    Tessellator.drawString("Hello", Player.getX() + 1, Player.getY() + 2, Player.getZ() + 1)
})
```

## Drawing a text in world with color
This will draw a text in the world with color Red with position (x: PlayerX + 1, y: PlayerY + 2, z: PlayerZ + 1)
```js
register("renderWorld", () => {
    Tessellator.drawString("Hello", Player.getX() + 1, Player.getY() + 2, Player.getZ() + 1, Renderer.RED)
})
```

### #drawString params
These are the params that you can **also** use inside the drawString function:
* (Boolean) Renders a black border.
* (Number) The scale of the text.
* (Boolean) Whether to scale the text up as the player moves away.