# 入门-新建mod

> 来源：[Getting_Started:_Creating_a_New_Mod](https://docs.baldursgate3.game/index.php?title=Getting_Started%3A_Creating_a_New_Mod)
> 抓取自 Larian 官方模组文档

---

This guide covers the first steps in mod creation: how to launch the Toolkit, create an empty mod, and assign the Source Asset Data Path.

The guide assumes that you have already installed Baldur's Gate 3 and the Baldur's Gate 3 Toolkit following the instructions in Getting Started: Installing the Toolkit.

Launching the Toolkit
The first time you launch the Toolkit, you will be asked to input the Data path. The default data folder depends on where your Baldur's Gate 3 game is installed.

On Steam, the default data path is: C:\Program Files (x86)\Steam\steamapps\common\Baldur's Gate 3\Data

On GOG, the default data path is: C:\Program Files (x86)\GOG Galaxy\Games\Baldurs Gate 3\Data
ⓘ If at any point you’d like to clear the config completely:

- Close the Editor

- Open File Explorer

- Paste the following in the address bar: C:\Users\<username>\AppData\Local\Larian Studios\Glasses

- Delete Config.xml from that folder

- Relaunch the Editor

ⓘ Make sure there aren't any vertical pipe symbols (|) in your data path. If there are, you may get an error that will cause the Toolkit to close.

Creating a New Mod
Once the Editor has launched, you’ll see the Browser window. In this window, select either New Project or the Create + button.

Creating a new mod in the Editor's Browser window.
You will be taken to the following view. Input your Project Name (mod name), and then select Create.

Naming a new mod in the Editor's Browser window.
At this point, you’ll need to wait for the Editor to load the basic mod setup. When it's done, you’ll see another Browser window that prompts you to Select your level.

Open the directory Act_1A_WLD and select the WLD_Crashsite_D level, which is the beginning of Act I, just after the nautiloid crashes on the beach.
ⓘ Some levels contain many smaller ones. For example, WLD_Main_A contains quite a bit of content, including the Crashsite, Emerald Grove, Goblin Camp, Underdark, and much more! Because it's so big, it also takes long time to load.
To save on loading times, load smaller levels with the specific content you want, like WLD_Crashsite_D.

Loading a level in the Editor.
Once the level loads, it should look like this:

A loaded level in the Editor.
Setting Up the Source Asset Data Path
If you plan to import assets as part of your mod (e.g. hairstyles, weapon models, textures), you will need to make sure you’ve defined a Source Asset Data Path.

In the Options menu, select Preferences (Ctrl+P).

Navigating to the Editor's Preferences.
Navigate to Global Settings, and scroll down to the Source Asset Data Path field.

Selecting the Source Asset Data Path in the Editor's Global Settings.
Click on “…” to select your Source Asset Data Path.

Your Source Asset Data Path must end in a \Data\ folder. It can live under a more complex hierarchy, or just inside your mod’s main folder (e.g. ...\steamapps\common\Baldurs Gate 3\Data\Mods\MyMod\Data).

Because it’s specific to the mod you’re working on, you will need to update this data path every time you change which mod project you have loaded, so long as you want to import resources.

Once selected, click Save & Close in the Preferences window.

Some assets must be located inside the Source Asset Data Path in order to import correctly. If there are additional requirements, the relevant guides will let you know.

Understanding the Mod Folders
Currently, files related to your mod project are stored in five different folders inside the Baldur's Gate 3 /Data/ folder, depending on what kind of file they are.

1. Data/Projects/<YourMod>

- Contains the data for the mod project to show up in the Toolkit.

- You can also add a PNG image into this folder (must be called thumbnail.png), and it will show up in the Editor as the image for your project.

2. Data/Editor/Mods/<YourMod>

- Not packed.

- For Editor files, like UUID or Stats files that contain Editor-specific data.

3. Data/Mods/<YourMod>

- Mod data that will be packed.

- Examples: UI assets, localisation, Osiris scripts, some level data, Thoth scripts.

4. Data/Public/<YourMod>

- Mod data that will be packed.

- Examples: stats files, root templates, UUID tables, any created Resources (VisualResources, AnimationResource, etc.) and their corresponding assets, texture atlases.

5. Data/Generated/Public/<YourMod>

- Mod data that will be packed.

- Examples: Virtual Textures, .dds files for overwritten textures.

Next Steps
Now that you’ve created a new mod project, you’ll probably want to delve a little bit deeper into the Editor's interface. Check out Editor Navigation for a quick introduction to some of the most commonly used panels and tools.

Alternatively, if you want to look through the list of available guides and follow a tutorial suited to the kind of mods you’d like to create, see the Main Page.

<div
