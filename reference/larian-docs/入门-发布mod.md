# 入门-发布mod

> 来源：[Getting_Started:_Publishing_a_Mod](https://docs.baldursgate3.game/index.php?title=Getting_Started%3A_Publishing_a_Mod)
> 抓取自 Larian 官方模组文档

---

This guide covers how to publish your mod locally and to mod.io.

Introduction
To publish your mod to mod.io, you will need a Larian account and a mod.io account, and to have connected them. For instructions on how to do this, see Getting Started: Installing the Toolkit.

Before starting the publish process, you only need to load into your mod project; loading into a level is not necessary.

Open the Project menu in the Editor and select Project Settings.

Navigating to the Project Settings in the Editor.
This view allows you to modify your project’s properties, manage dependencies and conflicts, and publish your mod.

Project Settings
Update the properties in the Project Settings window. The Name, Description and Thumbnail fields are mandatory.

Updating the project's properties.
All of these properties can be adjusted on mod.io after publication.

## Dependencies

Dependencies allow you to tell the game which other mods are required for yours to function correctly.

This is very useful for the regular player, who might not know when or what other mods are required for your mod to function. When set up correctly, dependencies are automatically downloaded and enabled for players when they download a mod.
ⓘ Setting a dependency in the Toolkit is different to doing it on mod.io. You will need to do both to set your dependencies correctly. We’ll go over the mod.io process later in this guide.
On the Dependencies tab, you can see a list of all mods that you are working on, as well as all mods that you have downloaded.

If you don’t see your mod in the list, make sure it's downloaded and present your mod folder located in %localappdata%\Larian Studios\Baldur's Gate 3\Mods\.

Selecting project dependencies.
You can now start selecting which mods your mod is dependent on. By giving your mod a dependency, you are saying that your mod is dependent on something from the other mod in order to function, and thus the other mod should be loaded before yours.

For example:

- The MyClass mod introduces a new class into the game: Artificer.

- The MySubclass mod introduces a new subclass for Artificer into the game: Alchemist.

- Because Alchemist is a subclass of Artificer, and the player can’t use Alchemist without first getting the Artificer class mod, we can say that MySubclass is dependent on MyClass.

In the example above, we would therefore set MyClass as a dependency of MySubclass.

With the MySubclass project loaded in the Toolkit, we can open the Dependencies tab and select MyClass in the list on the left and then press the > button to move it over.

Setting the MyClass mod as a dependency.
MySubclass is now dependent on MyClass. The game will ensure that MyClass is loaded before MySubclass when players start a new game session with the MySubclass mod enabled.
ⓘ When you make changes to a project's dependencies, you need to close and reopen the Toolkit for those changes to appear in the Resource Manager.

## Conflicts

Defining conflicts for your mod allows the game to automatically disable your mod when one of the listed conflicts is detected. This can be used to protect your mod from being loaded in situations where you know it won’t function correctly.

This can save players some pain, as in most cases they won’t have the information to understand why a mod they are using isn’t working correctly.

On the Conflicts tab, you can see a list of all mods that you are working on, as well as all mods that you have downloaded.

If you don’t see your mod in the list, make sure it's downloaded and present your mod folder located in %localappdata%\Larian Studios\Baldur's Gate 3\Mods\.

Selecting project conflicts.
You can now start selecting the conflicting mods. By defining conflicting mods, you are saying that your mod won’t work correctly if the other mods are also active, and thus your mod should be disabled to prevent issues.

For example:

- The MyConflictA mod overrides the Firebolt spell with a new icon.

- The MyConflictB mod also overrides the Firebolt spell with extra damage.

- Because both mods override the same spell, only one of them will work.

In the example above, we would therefore set MyConflictA as a conflict for MyConflictB. To do that, select MyConflictA in the list on the left, then press the > button to move it over. It will now show in the right-hand side.

Setting MyConflictA as a conflict.
MyConflictB now conflicts with MyConflictA, and the game will ensure that MyConflictB is disabled if a game is started with both MyConflictA and MyConflictB enabled.
ⓘ Not only will MyConflictB be disabled, but all of its dependencies will be disabled as well, as long as other mods aren’t also dependent on them.
Make sure to Save before closing the window.

Publishing Locally
The Publish Local button will create a .pak file for you, without uploading it to mod.io. It requires no authentication.

After the packing process is complete, you will be asked where to save the .pak file.

Publishing to Mod.io
To publish a mod to mod.io for public use, you must first authenticate with mod.io.

## Authenticating

Click Authenticate in the upper-right corner of the Project Settings window. The Authentication Wizard will open. You must accept both the Larian and the mod.io Terms and Conditions to continue.

Then, you will be presented with two authentication options: Steam or Larian Account.

The Authentication Wizard.
If you don’t already have a Larian account, you’ll need to create one here.
After logging in, the Publish button will be enabled, and you’ll be able to publish your mod to mod.io. After pressing the Publish button, you should see a progress bar at the top of the Project Settings window while the mod is being packaged and uploaded.

The progress bar indicating that a mod is being published.
Once completed, a webpage will automatically open in your browser. You should see the File Manager page for your mod on mod.io.

The File Manager page on mod.io.
You can also verify that your mod was successfully published by checking the Message Log panel in the Editor, where you should see the following line:

The success message in the Editor.

## Editing Your Mod on Mod.io

Immediately after publishing, on the File Manager page of your mod on mod.io, you’ll likely see a little clock icon under Scan. This means that your mod is still waiting to go through automation scanning. You cannot set your mod live until this scan is complete.

However, during this time, you can edit and set up other important fields for your mod.

### General Settings > Mod Profile

Navigate to General Settings > Mod Profile. If you’ve just published your mod, you’ll likely have a warning at the top of this page. In our case, we’re getting a “Needs File” warning because the mod file is still being scanned (as mentioned above).

A warning at the top of the Mod Profile page on mod.io.
In the Basics section, you can fill in a variety of user-facing information, like the Mod Name, Summary, and full Description; flag any mature content; and set the Tags.

### General Settings > Media

Navigate to General Settings > Media. In this section, you can upload additional screenshots that will be shown for your mod on the mod.io website, the BaldursGate3.game/mods website, and in the in-game Mod Manager. We recommend sticking to .png files for this.

You can also link to YouTube videos showing off your mod, but these will only be displayed on the web, not in-game.

Uploading media to the mod gallery on mod.io.

### Dependencies

Dependencies on mod.io work slightly differently to the Toolkit, but with the same goal in mind. The main difference between the two is that while the Toolkit manages load order, mod.io uses the dependencies to allow the game to download the dependencies of a mod.

On the Dependencies tab of your mod’s page, you’ll be presented with the following view:

The mod dependencies tab on mod.io.
In the Search mods field, you can browse all mods that have been uploaded to mod.io for Baldur's Gate 3, and select which ones are dependencies.

Selecting dependencies for a mod on mod.io.

## Setting the Mod Live

After verifying your mod details in the browser, you'll need to click on the Go live button on mod.io to actually set it live.

The 'Go live' button on mod.io.
You don’t have to immediately set your mod live – you can take your time editing the information and set it live only after you’re ready. Just remember to press the Save button near the bottom of the page to save your changes before exiting.

<div
