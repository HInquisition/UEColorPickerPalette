# Color Picker Palettes
This is a simple UE plugin that makes the work under the color guide easier. It extends the color picker, so you can easily access predefined colors straight from the editor.

Supported versions: tested on UE5.2, should work with all the latest versions.

![Pasted image 20231014185645](https://github.com/HInquisition/UEColorPickerPalette/assets/64382796/9004ab13-b3de-453f-adc7-eca441878cd8)

## Table of Contents
> - [Features](#features)  
> - [Settings](#settings)
>    - [Team-shared settings](#team-shared-settings)
>    - [Per-user settings](#per-user-settings)  
> - [How it works](#how-it-works)  
> - [Known issues and limitations](#known-issues-and-limitations)
> - [Why not just use the built-in color themes?](#why-not-just-use-the-built-in-color-themes?)  
> - [Support](#support)  

## Features
- Color palettes. You can define named sets of colors in the project settings.
- Extended color picker. You can access all palettes while editing any color in any editor.
- Unregistered color warnings. You will see warning icons if a color is not listed in any palette. This makes it easy to spot minor disagreements with the color guide.
   
  ![Pasted image 20231014185720](https://github.com/HInquisition/UEColorPickerPalette/assets/64382796/d6feb6a8-6019-4e29-aca2-b29d101a60c5)
- BP access to palettes if you want to change color from code.
- `FStrictLinearColor` type that will only show registered colors while editing.
## Settings 
Not every team member may need functionality from this plugin, so it has flexible settings that allow for adjustments to the user experience.
### Team-shared settings
- Color palettes. They are contained in `UColorPickerPaletteDeveloperSettings`, you can find them in the project settings under the Game section. They are stored in `DefaultGame.ini`. Due to this, they are shared between all team members.
### Per-user settings
- `bEnableColorPickerExtension` – When enabled, you will see color palettes' extension in color picker. Perhaps some types of art don't have strict color rules.
- `bEnableColorWarnings` – When this flag is set, you will see warning icons in color properties. A warning will appear if the color is not listed in any Palettes or in `ColorWhitelist`.
- `ColorWhitelist` – Whitelist for colors that you want neither to add to the palette nor to receive warnings about.
- `bUseCompactMode` – Compact mode reduces the size of color blocks and palette names. It's recommended to enable this mode if you have more than 20 colors or more than 5 palettes.
![Pasted image 20231014183348](https://github.com/HInquisition/UEColorPickerPalette/assets/64382796/dfc327b0-62d3-4b6e-b2cc-89ad5be36e6c)

## How it works
The core of the plugin consists of a few `FPropertyTypeCustomization` inherited from `FColorStructCustomization`. Our property customizations are registered in the editor module on the `PostEngineInit` loading phase, overriding default ones.

`FColorStructPaletteCustomization` extends common color customization, adding a warning icon and overriding color picker creation. Instead of a common color picker, we create a window widget consisting of a color picker and the color palettes' extension (if it's enabled in user settings).

## Known issues and limitations
Due to implementation, the plugin's functionality only works for properties. So color pickers summoned by nodes (for example, a node with a `FLinearColor` parameter or Vector node in a material graph) are unmodified. Please let me know if you know how to adjust this behavior without engine source code modification. However, you can always promote these literals to variables as a simple workaround.

## Why not just use the built-in color themes?
They are ugly, saved per-user, and super messy if you have more than 10 colors. If you've ever noticed that they exist, of course.

## Support 
Please support me if you enjoyed using this plugin or if you are using it as a company. You can buy this plugin on the marketplace.
