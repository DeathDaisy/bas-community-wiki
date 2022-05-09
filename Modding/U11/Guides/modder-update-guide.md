# Modder Update Guide

## Json Changes

### Handle Poses

`handPoseId` and `overrideHandPose` has been removed from the Interactables section

### Previews

Close Up Icon address has been added
```json
"closeUpIconAddress": "Path.to.my.Icon"
```

### Inventory Sounds

```json
  "inventoryHoverSounds": null,
  "inventorySelectSounds": null,
  "inventoryStoreSounds": null,
```

### Category

This has changed to a simple field

```json
  "category": "Daggers",
```

To help mass change your categories, you can use notepad++
and this regex to find and replace to fix your json category

find : `^\s*"categoryPath": \[\s*("[a-zA-Z0-9 ]+")\s*]`

replace: `"category": $1`

Make sure you check `Regular expresssion` AND `. matches newline`
you can do `Find in files` in notepad++ to do it for all the jsons

<video autoplay="autoplay" loop="loop">
  <source src="{{ site.github.url }}/assets/tips/category-regex.mp4" type="video/mp4">
</video>

## C# Changes

### "AlternateUse"

if you use a `HeldActionEvent` or `TouchActionEvent` for an item that used the action `AlternateUseStart` or `AlternateUseStop`, It has been renamed to `SecondaryUseStart` and `SecondaryUseStop` respectively. similarly, `controlHand` now uses the bool `secondaryUsePressed`.

### Saved Values

Saved Values has been removed and replaced with `CustomData`, which accepts any type. Functions include:
```csharp
public bool HasCustomData<T>()
public bool TryGetCustomData<T>(out T customData)
public void AddCustomData<T>(T customData)
public void RemoveCustomData<T>()
```
The most obvious usecase is to create a Save Class which can house all the variables you'd like an item to maintain over loads.
