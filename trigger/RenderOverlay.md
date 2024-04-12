# [Render Overlay](https://www.chattriggers.com/javadocs/-chat-triggers/com.chattriggers.ctjs.engine/-i-register/register-render-overlay.html) Trigger
This runs the given function every time the game overlay is rendered.<br>
This is usually used to make 2D **(in screen)** rendering.

## Drawing a text in screen
This will draw a text in the screen with position (x: 10, y: 10)
```js
register("renderOverlay", () => {
    Renderer.drawString("&aHello", 10, 10)
})
```

## Drawing an item in screen
This will draw a item in the screen with position (x: 10, y: 10)
```js
const item = new Item("minecraft:skull")

register("renderOverlay", () => {
    item.draw(10, 10)
})
```

## Drawing a centered text
This will draw a text in the middle of the screen
```js
const text = "&aHello"

register("renderOverlay", () => {
    // We remove the text's formatting so that the text
    // is centered correctly
    Renderer.drawString(
        text,
        Renderer.screen.getWidth() / 2 - Renderer.getStringWidth(text.removeFormatting()) / 2,
        Renderer.screen.getHeight() / 2
        )
})
```