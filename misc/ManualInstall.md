# Manually Installing Modules

### Getting a module
First we need the module we want to install for this we'll head over to the [Chattriggers Modules Website](https://www.chattriggers.com/modules) and search for our module.<br>
Then we click on the `view` button.<br>
Next step will be to scroll down to the bottom and click the `Download` button<br>
> [!IMPORTANT]
> Make sure you download the correct version for your mod (3.0 beta is for mc 1.21+).<br>

### Dependencies
Once we have the zip file downloaded we'll proceed to unzip it and open the folder.<br>
Next step is to open the `metadata.json` file that it contains inside, we'll check whether there is a `"requires":` inside this.<br>
* **if there is not**: do nothing
* if there is: This is a list of modules that the current module depends on, for this we'll need to install each one of them and also check whether those require any dependencies themselves and repeat this cycle.

### Wrapping things up
Once we have all of our folders (aka "modules") we can now go in game and type `/ct files` and hit enter<br>
A file window will pop up, we open the folder that is called `modules` and paste all of the folders that we have gathered thus far<br>
After that we can head back over in game and type `/ct load` and hit enter.<br>
And that should be it, you _should_ have properly manually installed the desired module.
> [!IMPORTANT]
> Make sure that the folders do not have a folder inside otherwise the module will not work properly.<br>
> for example: If i unzipped Vigilance-1.3.2 and it has a folder inside called Vigilance this folder inside is the module itself that i need