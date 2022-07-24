---
layout: page
title: Camera Scaler
---

[Get it on Asset Store]()

Camera Scaler component, that works just like Canvas Scaler (Expand/Shrink modes, making camera match width instead of height, etc), for both prespective and orthographics cameras

### How to use it

Add the `Camera Scaler` component to game object with Camera. Set `ReferenceResolution` to the resolution you have set in Game View (or resolution you usually develop & test you game with) and choose `Mode` that fits your game. You can see different modes behaviour on video or in included example scenes

### Modes
* **Constant Width** - this mode keeps camera width (or horizontal fov, in case of perspective camera) constant on all aspect ratios. Works the same as **MatchWidthOrHeight** with **Match** set to 0
* **MatchWidthOrHeight** - this mode requires you to set Match value, and interpolates between **Constant Width** and **Constant Height** modes. It works just like Canvas Scaler's MatchWidthOrHeight mode, so if you have canvas with Canvas Scaler on top of camera, UI objects will line up with world objects
* **Expand** - this mode always keeps area within ReferenceResolution visible at the screen, by expanding camera horizontally if device is wider, or vertically if device is taller. It works just like Canvas Scaler's Expand mode
* **Shrink** - this mode never allows area outside ReferenceResolution visible at the screen, by shrinking camera horizontally if device is narrower, or vertically if device is shorter. It works just like Canvas Scaler's Shrink mode
* **Constant Height** - this mode does nothing, as Unity Camera behaves like this by default

### Scripting APIs

This component controls Camera's `size` (for ortho) or `fov` (for perspective) properties. So you can't write to them from your scripts to zoom camera when using camera scaler. Instead, you can use `CameraScaler.CameraZoom` property, that is set to 1 by default

Additionaly, you can use read-only properties `CameraScaler.HorizontalSize` and `CameraScaler.HorizontalFov`, if you need this values

### Does it works while not in play mode?

No, this component only work in play mode and in game builds. That makes it easier to set up camera, you can change `size` and `fov` however you want in edit mode, and when game launches, CameraScaler takes control over `size`/`fov`. When setting up cameras, make sure resolution in Game panel is the same as in `CameraScaler.ReferenceResolution`

### Example scenes

There is two scenes in Examples folder, **2D Playground** and **3D Playground**. You can launch the game and try to resize Game window, to see how the camera scaler works. Also try to change Mode on Main Camera, to check different working modes

[Get it on Asset Store]()