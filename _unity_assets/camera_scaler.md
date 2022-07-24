---
layout: page
title: Camera Scaler
---

[Get it on Asset Store]()

Camera Scaler component, that works just like Canvas Scaler (Expand/Shrink modes, making camera match width instead of height, etc), for both prespective and orthographics cameras

### How to use it

Add the `Camera Scaler` component to game object with Camera. Set `ReferenceResolution` to the resolution you have set in Game View (or just to resolution you usually test you game with) and choose `Mode` that fits your game

### Modes
* **Constant Width** - this mode keeps camera width (or horizontal fov, in case of perspective camera) constant on all aspect ratios. Works the same as **MatchWidthOrHeight** with **Match** set to 0
* **MatchWidthOrHeight** - this mode requires you to set Match value, and interpolates between Constant Width and Constant Height modes. It works just like Canvas Scaler's MatchWidthOrHeight mode, so if you have canvas with it on top of camera, UI objects will line up with world objects perfectly
* **Expand** - this mode always keeps area within ReferenceResolution visible at the screen, by expanding camera horizontally if device is wider, or vertically if device is taller. It works just like Canvas Scaler's Expand mode
* **Shrink** - this mode never allows area outside ReferenceResolution visible at the screen, by shrinking camera horizontally if device is narrower, or vertically if device is shorter. It works just like Canvas Scaler's Shrink mode
* **Constant Height** - this mode does nothing, as Unity Camera behaves like this by default

### Scripting APIs

This component controls Camera's `size` (for ortho) or `fov` (for perspective) properties. So you can't write to them from your scripts to zoom camera when using camera scaler. Instead, you can use `CameraScaler.CameraZoom` property, that is set to 1 by default
Additionaly, you can use read-only properties `CameraScaler.HorizontalSize` and `CameraScaler.HorizontalFov`, if you need this values

### Example scenes