# [Vigilance](https://www.chattriggers.com/modules/v/Vigilance) Library
This is a very helpful library, its purpose is to make a Configuration Gui easily.<br>
Despite the module having documentation on how it is meant to be used, more often than not new developers struggle to get it going.

> [!WARNING]
> The information used here was mostly taken from the example of the module.<br>

## Metadata
Your ``metadata.json`` might be looking like this<br>
from [Chattrigger Slate](https://chattriggers.com/slate/#the-metadata-file)
```json
{
  "name": "ExampleModule",
  "creator": "YourNameHere",
  "description": "Our first module!",
  "version": "1.0.0",
  "entry": "index.js"
}
```
although this is correct, we need to add the module we're going to be using, we do this so that the module gets automatically imported to the user's modules folder that way it won't give them an error whenever they try to use our module.<br>
This would be the correct ``metadata.json`` **for this occasion**
```json
{
  "name": "ExampleModule",
  "creator": "YourNameHere",
  "description": "Our first module!",
  "version": "1.0.0",
  "entry": "index.js",
  "requires": ["Vigilance"]
}
```

## Example Config
This is how we make a simple settings gui using the library.
```js
// This right here should be on it's own file
// in this case we can call this "config.js"

// Here we import the necessary decorators
import { @Vigilant, @TextProperty, @ColorProperty, @ButtonProperty, @SwitchProperty, Color } from 'Vigilance';

// We define our vigilance config this way
// and assign the name of the module/folder where this is going to be in
@Vigilant("MyModuleName")
class Settings {
    // Make a text input setting
    @TextProperty({
        name: "text",
        description: "Example of text input that does not wrap the text",
        category: "General",
        subcategory: "Category",
        placeholder: "Empty... :("
    })
    textInput = ""; // This variable has the input

    // Make a color picker setting
    @ColorProperty({
        name: "Color Picker",
        description: "Pick a color! (hopefully...)",
        category: "General",
        subcategory: "Category"
    })
    myColor = Color.BLUE; // This variable has the input

    // Make a button setting
    @ButtonProperty({
        name: "Do action!!!",
        description: "print some cool stuff :)",
        category: "General",
        subcategory: "Category",
        placeholder: "Activate"
    })
    myButtonAction() {
        // Whenever the button is clicked it will run this function
        // Something to take into consideration is that each button
        // has to have its own function if they do not do the same thing.
        console.log("wow i have a button?!?");
    }

    // Make a switch setting
    @SwitchProperty({
        name: "exampleswitch",
        description: "Switch off/on!",
        category: "General",
        subcategory: "Category"
    })
    switch = false; // This variable has the input

    // Make a hidden switch setting
    // that will unhide whenever [exampleswitch] is enabled
    @SwitchProperty({
        name: "exampleswitchhidden",
        description: "Switch off/on!",
        category: "General",
        subcategory: "Category"
    })
    hidden_switch = false; // This variable has the input

    constructor() {
        this.initialize(this);
        // Registers a listener that runs a function every time
        // the setting with name "text" gets changed.
        this.registerListener("text", newText => {
            console.log(`Text changed to ${newText}`);
        });

        this.setCategoryDescription("General", "shows... cool stuff :)")
        this.setSubcategoryDescription("General", "Category", "Shows off some nifty property examples.")

        // Example of settings being hidden whenever
        // the main setting is disabled

        // Main feature name to the right
        // hidden feature name to the left
        this.addDependency("exampleswitchhidden", "exampleswitch")
        // Now the [exampleswitchhidden] will only be shown whenever
        // [exampleswitch] is enabled
    }
}

// Export new class so we can use it outside of this file!
export default new Settings();
```

## Example Usage
After we've made our ``config.js`` we can now use it.
```js
// This would be the file we want to use the settings on.
// in this example we'll be assuming this is "index.js"

// First of all, we need to import the settings (how else do we use it).
import Settings from "./config";

// to open the config gui use the "openGUI" function
register("command", () => Settings.openGUI()).setName("mycommand");
```

To see the value of a config we can simply use the variables that we set in our ``config.js`` file<br>
For example taking the value of the ``exampleswitch``
```js
Settings.switch // This will return [false] if disabled and [true] if enabled
```

We can now combine this with Chattriggers triggers<br>
For example checking whether the user has a setting enabled before sending something in chat.
```js
register("step", () => {
    // If the setting is disabled we return
    // this means that the code below won't run.
    if (!Settings.switch) return

    ChatLib.chat("switch is enabled!")
}).setFps(1)
```

Something to take into consideration is that if you define a setting on the main scope for example:
```js
const mySwitch = Settings.switch
```
This will always stay the same value as whenever the file was loaded<br>
so say we have it ``false`` as default it'll always be ``false``
unless you use it inside a trigger or function as we did in the previous example.

> [!IMPORTANT]
> Since the [Vigilance](https://www.chattriggers.com/modules/v/Vigilance) module uses decorators your code editor might make them into a red color though this does not mean that it does not work simply ignore this.<br>