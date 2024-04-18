# [PogData](https://www.chattriggers.com/modules/v/PogData) Library
This is a very helpful library, its purpose is to save data between reloads.<br>
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
  "requires": ["PogData"]
}
```

## Example Code
This is how we make a new PogObject and access it in our code!.
```js
// Here we import the PogObject class
import PogObject from 'PogData';

// We define the object here, the const will be the way we access the object.
// The moduleName string must be the name of your module!
const object = new PogObject("moduleName", {
  boolean: true,
  array: ["0", "1"],
  string: "hello!";
})
object.autosave(1) // This will autosave the object, modify the number to change the amount of minutes.

object.boolean = false; // this will change the objects "boolean" value
object.array.push("2") // this will add a new string to the array
object.string = "hello again!" // this will change the objects "string" value 

object.save() // this will manually save the object's variables
```

## Accessing the variables
To access the variables, we do the same method we used to change them without the operator.
```js
if(object.boolean) { // the if statement is checking whether or not our boolean variable is true, we are accessing it using object.boolean
  console.log("our boolean is true!")
} else {
  console.log("our boolean is false!")
}

console.log(object.string) // this will add the objects string into the console.
console.log(object.array[0]) // this will add the objects arrays first value to the console. 
```
