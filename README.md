# Passthrough Sample

Different levels are provided for the different features. Always check the Level Blueprint and the widget if any, check VRTPPawn for features common to each level.

## Navigating through the samples

By pressing the Menu button on your left controller you'll open the 'Navigation Menu', where you can see if passthrough is supported on your device, the name and description of the level you're in and a list of levels you can travel to.
Simply aim with your right controller to the level you want and press the right trigger to travel to it. (scroll the list with right thumbstick)

![Navigation Menu](Media/unreal-pt-navigation-menu.png)

## Passthrough Background with Augmented Objects
A common usage of Passthrough is as a background, where you can place virtual objects (Passthrough AR). You can do this easily, starting from the **PTBackground** scene:

1. Import your FBX or 3D object into your project.
2. Place your object in the scene.
3. Give your object a grab component and set its collision preset to "PhysicsActor" so it can be grabbed and moved around your room.
4. Build & Deploy.

Here are relevant assets in this scene that you can use and modify to fit your needs:

* **Level Blueprint**: Creates and add Passthrough layer to the player pawn
* **BP_OculusLogo.uasset**: A standard actor with lit material.
* **BP_Grafitti.uasset**: This is the same as BP_OculusLogo.uasset but with a custom material.

## Using Passthrough Styles For Colorful Effects

The **PTStyles** level demonstrates some of the styling options which are available on Passthrough layers. The styling can be controlled using the widget in the level:

![Styler widget](Media/unreal-pt-styles-widget.png)

* **Color mao Curve**: colorize Passthrough using a predefined curve. The curves are defined in the folder `Content/Passthrough/Data/` and can be customized to achieve different colorizations.
* **Color map Controls**: use the Contrast/Brightness/Posterize sliders to apply image processing effects which are implemented using a color map of type "Grayscale To Color".
* **Edge Color**: use the Red/Green/Blue/Alpha sliders to adjust the color of salient edges in the image (extracted using a Sobel filter).

Here are the relevant assets in this scene that you can use and modify to fit your needs:

* **Level Blueprint**: Creates and adds Passthrough layer to the player pawn, sends layer to the widget
* **BP_Menu.uasset**: The menu actor with the menu widget.
* **W_PTStyler.uasset**: The widget directly modifying the styling of Passthrough

### Color Maps

Instead of specifying color effects via parameters (as demonstrated in the **PTStyles** level), you can define them as an array of 256 values which maps each (grayscale) input value to a new color. This is shown in the level **PTColorMap**.
With the in-game widget you can modify each those 256 values and see the impact on the styling.

![Color Map widget](Media/unreal-pt-color-map-widget.png)

Here are the relevant assets in this scene that you can use and modify to fit your needs:

* **Level Blueprint**: Creates and adds Passthrough layer to the player pawn, sends layer to the widget
* **W_PTColorMap.uasset**: The widget for viewing the color map array and editing each of its 256 values

## Color Look-Up Tables (LUTs)

Passthrough can also be colorized using color LUTs. As demonstrated in the **PTColorLut** level you can use two kinds of LUT use type : *Color LUT* and *Interpolated Color LUT*, the second one will take 2 LUTs (source & target) and blend between them using the LUTWeight value.

![Color Map widget](Media/unreal-pt-color-lut-widget.png)

Here are the relevant assets in this scene that you can use and modify to fit your needs:

* **Level Blueprint**: Creates and adds Passthrough layer to the player pawn, sends layer to the widget
* **W_PTColorLUT.uasset**: The widget for viewing & editing the way the LUTs are used

### Color and Scale Offset

Another way to colorize Passthrough layers is to use color scale and offset.This is illustrated by the **PTColorScaleAndOffset** level, which animate both of those settings.
You can use the in-game widget to stop and edit the color scale and offset

![Color Scale And Offset widget](Media/unreal-pt-color-scale-and-offset-widget.png)

Here are the relevant assets in this scene that you can use and modify to fit your needs:

* **Level Blueprint**: Creates and adds Passthrough layer to the player pawn, sends layer to the widget & animates the color scale and offset
* **W_PTColorScaleAndOffset.uasset**: The widget for viewing and editing the color scale and offset

**Caution**:

The lighting and color in this sample may cause seizures in people with epilepsy or who are sensitive to light and color.

### Passthrough Masking

The **PTMaskedBrush** and **PTMasking** levels demonstrate experiences where a Passthrough layer is masked and only visible in certain screen areas.
In the **PTMaskedBrush** sample the controller can be used as a brush to draw a projected passthrough stroke by pressing the left and right triggers.
**PTMasking** showcases a circle mesh with masked projected passthrough (using the *mPokeAHoleMask* material) that is attached to the controller which allows you to see your hands (you can change attached controller with left/right trigger)

You can re-use and modify the *mPokeAHoleMask.uasset* material to mask areas in your scene.

Here are the relevant assets in this scene that you can use and modify to fit your needs:

* **Level Blueprint**: Creates and adds Passthrough layer to the player pawn, binds inputs and project passthrough to the circle
* **MaskedCircle**: Actor on which the passthrough is projected, using the *mPokeAHoleMask* material to smooth its border

## How to Use

### Load the project

First, ensure you have Git LFS installed by running this command:
```sh
git lfs install
```

Then, clone this repo using the "Code" button above, or this command:
```sh
git clone https://github.com/oculus-samples/Unreal-PassthroughSample
```

### Launch the project in the Unreal Editor using one of the following options.

#### Epic Games Launcher with MetaXR plugin

The easiest way to get started is to use the prebuilt Unreal Engine from the Epic Games Launcher, with MetaXR plugin.

1. Install the [Epic Games Launcher](https://www.epicgames.com/store/en-US/download)
2. In the launcher, install UE5 (recommended).
3. Download and install the MetaXR plugin from the [Unreal Engine 5 Integration download page](https://developer.oculus.com/downloads/package/unreal-engine-5-integration).
4. Launch the Unreal Editor
5. From "Recent Projects", click "Browse" and select `PTSamples.uproject`

#### Meta fork of Epic’s Unreal Engine

The Meta fork of Epic’s Unreal Engine will give you the most up to date integration of Oculus features. However, you must build the editor from its source.

Follow the instructions on [Accessing Unreal Engine source code on GitHub](https://www.unrealengine.com/en-US/ue-on-github) to obtain:
- an Epic account
- a GitHub account
- authorization to access the Unreal Engine source repository
Disregard instructions on downloading Epic’s Unreal Engine source code as you will be building the Meta fork of Epic’s Unreal Engine source.

Make sure you have Visual Studio installed properly:
- Launch the Visual Studio Installer and click Modify for the Visual Studio version you want to use.
- Under the Workloads tab, click Game development with C++ if it isn’t checked and then click Modify.

1. Download the source code from the [Meta fork of Epic’s Unreal Engine on GitHub](https://github.com/Oculus-VR/UnrealEngine).
2. Follow Epic’s instructions on [Building Unreal Engine from Source](https://dev.epicgames.com/documentation/en-us/unreal-engine/building-unreal-engine-from-source/) to complete the process.
3. Launch the Unreal Editor
4. From "Recent Projects", click "Browse" and select `PTSamples.uproject`

Depending on your machine, the build may take awhile to complete.

# Licenses
The [Meta License](./LICENSE) applies to the SDK and supporting material. The MIT License applies to only certain, clearly marked documents. If an individual file does not indicate which license it is subject to, then the Meta License applies.
