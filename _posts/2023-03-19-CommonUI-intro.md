---
title: Common UI introduction
date: 2023-03-19 22:22:22 -500
author: Luq
categories: [CommonUI]
tags: [UMG, UI, CommonUI]
img_path: /assets/img/Posts/CommonUI-intro/
---

Common UI is a plugin which supports multi-platfrom UI development. It provides a functionality which helps to resolve complex cases with menu layers/submenus management. It makes it easier to control widgets with a gamepad. 
The plugin also enhances a couple of basic UMG widgets and introduces a bunch of new ones to unify the implementation as much as possible, no matter the target platform.

<h4>Features:</h4>
- introduces a menu stack and input routing functionality (top widget on the stack receives the input)
- gives a possibility to specify common input actions (e.g common accept on PC keyboard can mapped to "Enter" and on gamepad to "A" button)
- platform specific button icons (you can specify button brushes per each platform/controller, plugin will automaticaly change the brushes if you'll change a controller)
- several new widgets, which helps to implement platform independent UI (e.g Common Hardware Visibility Border - hides/shows content on specific platform)


> This tutorial/documentation mostly explains the plugin usability on Windows platfrom (mainly UI implementation for gamepad and keyboard/mouse control). The true power of the plugin shows up if your project is intended to build on various platforms (PS4/5, Xbox, NS, PC etc). I do not have a knowledge and posibility (external SDKs required) to show up UI implementation for other platform than Windows, but I hope it will be useful also for multi-platform projects.
{: .prompt-info }


## Plugin enabling

Open plugins browser, `Edit > Plugins`, search for **Common UI Plugin** and enable it. Editor restart is required after plugin enabling.

![Desktop View](1.png){: .normal .shadow}
_Plugin to be enabled_

Under `Project Settings > General Settings > Default Classes`, set **Game Viewport Client Class** to **CommonGameVieportClient**. It mainly implements input routing functionality.

![Desktop View](2.png){: .normal .shadow}
_Class setting_

## Common Input Settings

### CommonInputActionDataBase

Create a new Data Table and pick **CommonInputActionDataBase** row structure.

![Desktop View](3.png){: .normal .shadow}
_Pick row structure_

This table lets you define common actions and map them to multiple different sets of input controllers. In this example I have defined 4 common actions: CommonAccept, CommonBack, CommonNext and CommonBack.

![Desktop View](4.png){: .normal .shadow}
_Data table structure_

Each action has a several options to be setup:
- Display Name - this name can be displayed on a navigation bar
- Hold Display Name - same as above but for hold action
- Nav Bar Priority - allows you to set up an order of actions displayed on navigation bar
- Keyboard Input Type Info - keyboard key mapping
- Default Gamepad Input Type Info - gamepad key mapping
- Gamepad Input Overrides - useful for changing mapping for a specific platform, e.g different key mapped on PS5
- Touch Input Type Info - touch key mapping

![Desktop View](5.png){: .normal .shadow}
_Row config_

### CommonUIInputData

The next step is to create a blueprint class based on the **CommonUIInputData** class. You can call it UIInputData. In this class you have to set up Default Click Action and Common Back Action. 

![Desktop View](6.png){: .normal .shadow}
_Parent class selection_

These two actions have to be selected from a previously created data table **CommonInputActionDataBase**.

![Desktop View](7.png){: .normal .shadow}
_BP class settings_

### CommonInputBaseControllerData

Next, make a blueprint class based on the **CommonInputBaseControllerData** class. Basically, this is an asset that contains icons library for the controller. Make one for a keyboard and call it WindowsKeyboardControllerData and the second one for a gamepad and call it XboxControllerData.

![Desktop View](8.png){: .normal .shadow}
_Parent class selection_

![Desktop View](9.png){: .normal .shadow}
_Keyboard brush settings_

![Desktop View](10.png){: .normal .shadow}
_Gamepad brush settings_

### Common Input Settings

The last configuration step is to link Input Data class and platform specific classes in `Project Settings > Game > Common Input Settings`.
For Input Data, select the class created in [CommonUIInputData](#commonuiinputdata) section.

Next, configure default input for Windows platform. You can specify Default Input Type between keyboard/mouse or gamepad. You can also specify if some input type should be disabled, e.g I have disabled touch support to completly disabled input from touch screen in my game.

And last but not least, Controller Data. Set the classes configured in [CommonInputBaseControllerData](#commoninputbasecontrollerdata) section.

![Desktop View](11.png){: .normal .shadow}
_Common Input Settings_

That’s all. Common UI is now fully configured and you’re good to go with widgets creation.