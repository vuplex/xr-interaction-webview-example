# XR Interaction Toolkit WebView Example

This Unity project demonstrates how to use [Vuplex 3D WebView](https://developer.vuplex.com) with Unity's [XR Interaction Toolkit (XRI)](https://docs.unity3d.com/Packages/com.unity.xr.interaction.toolkit@1.0/manual/index.html). It includes XRI and its dependencies, so all you need to do is [import 3D WebView](https://store.vuplex.com/webview/overview) into the project. Please note that input with XRI requires 3D WebView's [CanvasWebViewPrefab](https://developer.vuplex.com/webview/CanvasWebViewPrefab). XRI input with the non-canvas [WebViewPrefab](https://developer.vuplex.com/webview/WebViewPrefab) is not supported.

<p align="center">
  <img alt="demo" src="./demo.gif" width="640">
</p>

## Steps taken to create this project

1. Created a new project with Unity 6 (6000.0.21).

2. Imported the following via the Package Manager:
    - [XR Interaction Toolkit](https://docs.unity3d.com/Packages/com.unity.xr.interaction.toolkit@3.0/manual/index.html) (com.unity.xr.interaction.toolkit) v3.0.7
    - From the "Samples" tab of the XR Interaction Toolkit package, imported the "Start Assets" sample.
    - [3D WebView for Android](https://store.vuplex.com/webview/android) (omitted from this repo via the .gitignore)

3. Created a copy of the DemoScene.unity scene from the XRI Starter Assets sample, which I named XRInteractionWebViewExample.unity:

```sh
cp "Assets/Samples/XR Interaction Toolkit/3.0.7/Starter Assets/DemoScene.unity" Assets/Scenes/XRInteractionWebViewExample.unity
```

4. Made the following changes to the new XRInteractionWebViewExample.unity scene:
    - Added a [CanvasWebViewPrefab](https://developer.vuplex.com/webview/CanvasWebViewPrefab) and [CanvasKeyboard](https://developer.vuplex.com/webview/CanvasKeyboard) to the scene's UI Sample canvas.
    - Added a "Scripting API Example" object with an [XRInteractionWebViewExample.cs script](Assets/Scripts/XRInteractionWebViewExample.cs) that demonstrates how to use 3D WebView's scripting APIs.
    - Removed all objects from the scene that aren't necessary for demonstrating interaction with the webview.
    - Modified the color settings of the controllers' LineVisual objects to make the controller ray easier to see.

5. In Project Settings -> XR Plugin Management:
    - Clicked "Install XR Plugin Management".
    - In the Android tab -> Plug-in Providers, enabled Oculus.

## Troubleshooting

3D WebView's prefabs detect input through Unity's event system like described in [this article](https://support.vuplex.com/articles/clicking). In the case of XR Interaction Toolkit, the scene's [XRUIInputModule](https://docs.unity3d.com/Packages/com.unity.xr.interaction.toolkit@3.0/api/UnityEngine.XR.Interaction.Toolkit.UI.XRUIInputModule.html) sends input through Unity's event system, which 3D WebView's prefabs then detect. If your CanvasWebViewPrefab and CanvasKeyboard aren't responding to clicks or scrolling, then that indicates that your scene is not configured correctly. I recommend using this project as a reference and verifying the following settings in your scene:

- The canvas must have a [TrackedDeviceGraphicRaycaster](https://docs.unity3d.com/Packages/com.unity.xr.interaction.toolkit@3.0/api/UnityEngine.XR.Interaction.Toolkit.UI.TrackedDeviceGraphicRaycaster.html) attached to it.
- The canvas's [Event Camera](https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/class-Canvas.html#properties) must be set to the scene's main camera.
