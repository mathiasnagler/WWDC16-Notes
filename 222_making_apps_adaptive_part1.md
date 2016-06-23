# 222 - Making Apps Adaptive, Part 1

- Takaway: **The system is going most of the work for you**
- 300+ Combinations
    - Devices and Orientation
    - Dyanmic Type
    - Layout Direction

## Trait System

- Traits describe the env your app runs in
- Example: `horizontalSizeClass`
- Trait Collection: Dict maps traits to values
- Layout Trait Examples: Size Classes, Dynamic Type, Layout Direction
- Appearance Traits: Display Gamut, Interface Style
- Capabilities: 3D Touch

### Size Classes

- Describe the experience: How is your information layed out
- 3 Axis of customization: Screen Size, Orientation, Adaptation
- Base your layout on the available space, not device orientation or adaptation
- Specifics: 4 possible Size Class Combinations (wC-hC, wR-hC, wC-hR, wR-hR) 
- Width Class is most common => only 2 combinations

### How Traits Work?

- The trait system propagates a trait collection down the view hierarchy
- Giving each stop a chance to react 
- Screen > Window > ViewController > View
- Every stop conforms to `UITraitEnvironment`: `traitCollectionDidChange`
- Override `traitCollectionDidChange` for customization
- Check for specific trait changes (Only do work if the traits you are interested actually changing)
- Some systems react to `traitCollectionDidChange` for you
    - Interface Builder (the system knows how to automatically apply the size classes)
    - Asset Catalogs
    - `UIAppearance`

### Interface Builder

- Simulator is used to render content (Pixel perfect rendering right in design canvas)
- New Zooming Controls
- New Device Configuration Bar
- Vary for Traits:
    - Choose for Regular Width / Any Height
    - Choose for Regular Height / Any Width
- Edits in the device bar are reflected to the correct size class
