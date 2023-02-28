# Unity Style Guide

This article contains ideas for setting up a projects structure and a naming convention for scripts and assets in Unity.

<a name="toc"></a>
## Table of Contents

> 1. [Introduction](#introduction)
> 2. [Unity Setup](#unity-setup)
> 3. [Project Structure](#project-structure)
> 4. [Scripts](#scripts)
> 5. [Asset Naming Conventions](#asset-naming-conventions)

<a name="introduction"></a>
## 1. Introduction

### Sections
> 1.1 [Important Terminology](importantterminology)

> ##### *Arguments over style are pointless. There should be a style guide, and you should follow it.*
> [_Rebecca Murphey_](https://rmurphey.com)

#### All structure, assets, and code in any project should look like a single person created it, no matter how many people contributed.
Moving from one project to another should not cause a re-learning of style and structure. Conforming to a style guide removes unneeded guesswork and ambiguities.

It also allows for more productive creation and maintenance as one does not need to think about style, simply follow instructions. This style guide is written with best practices in mind, meaning that by following this style guide you will also minimize hard to track issues.

#### Friends do not let friends have bad style.
If you see someone working either against a style guide or no style guide, try to correct them.

When working within a team or discussing within a community, it is far easier to help and to ask for help when people are consistent. Nobody likes to help untangle someone's spaghetti code or deal with assets with names they can't understand.

If you are helping someone who's work conforms to a different but consistent and sane style guide, you should be able to adapt to it. If they do not conform to any style guide, please direct them here.

<a name="importantterminology"></a>
### 1.1 Important Terminology

<a name="terms-cases"></a>
#### Cases
There are a few different ways you can name things. Here are some common casing types:

> ##### PascalCase
> Capitalize every word and remove all spaces, e.g. `DesertEagle`, `StyleGuide`, `ASeriesOfWords`.
> 
> ##### camelCase
> The first letter is always lowercase but every following word starts with uppercase, e.g. `desertEagle`, `styleGuide`, `aSeriesOfWords`.
>  ##### lowercase
> All letters are lowercase, e.g. `deserteagle`, 
>
> ##### Snake_case
> Words can arbitrarily start upper or lowercase but words are separated by an underscore, e.g. `desert_Eagle`, `Style_Guide`, `a_Series_of_Words`.

**[⬆ Back to Top](#table-of-contents)**

<a name="unity-setup"></a>
## 2. Unity Setup

### Sections
> 2.1 [Layout](#layout)

> 2.2 [Script Editor](#script-editor)

<a name="layout"></a>
### 2.1 Layout
XXX

<a name="script-editor"></a>
### 2.2 Script Editor
XXX

**[⬆ Back to Top](#table-of-contents)**

<a name="project-structure"></a>
## 3. Project Structure

### Sections
> 3.1 [Assets Folder Structure](#assets-folder-structure)

> 3.2 [Scene Structure](#scene-structure)

The directory structure style of a project should be considered law. Asset naming conventions and content directory structure go hand in hand, and a violation of either causes unneeded chaos.

In this style, we will be using a structure that relies more on filtering and search abilities of the Project Window for those working with assets to find assets of a specific type instead of another common structure that groups asset types with folders.

> Using a prefix [naming convention](#asset-name-modifiers), using folders to contain assets of similar types such as `Meshes`, `Textures`, and `Materials` is a redundant practice as asset types are already both sorted by prefix as well as able to be filtered in the content browser.

<a name="assets-folder-structure"></a>
### 3.1 Assets Folder Structure
<pre>
Assets
    <a name="structure-sandbox">_Sandbox</a>
        DeveloperName
            Testing
            WIP
    <a name="structure-top-level">ProjectName</a>
            _Levels
            Environment
                Architecture
                Props
            Gameplay
                Characters
                Equipment
                Items
                Vehicles
            MaterialLibrary
                Materials
                Shaders
                Utility
            Scripts
                AI
                Gameplay
                    Input
                    Player
                Tools
            Settings
                Input
                    Controls
                RenderPipeline
            Sound
            UI
</pre>

<a name="scene-structure"></a>
### 3.2 Scene Structure
<pre>
SceneName
    Debug
    Management
    UI
    Cameras
    Lights
    World
        Terrain
        Props
    Gameplay
        Actors
        Items
    _Dynamic
</pre>

**[⬆ Back to Top](#table-of-contents)**

<a name="scripts"></a>
## 4. Scripts

### Sections
> 4.1 [Class Structure](#class-structure)

> 4.2 [Variables](#variables)

> 4.3 [Functions](#functions)

This section will focus on C# classes and their internals. When possible, style rules conform to Microsoft's C# standard.

<a name="class-structure"></a>
### 4.1 Class Structure
Class members should be alphabetized, and grouped into sections:
* Constant Fields
* Static Fields
* Fields
* Constructors
* Properties
* Events / Delegates
* LifeCycle Methods (Awake, OnEnable, OnDisable, OnDestroy)
* Public Methods
* Private Methods
* Nested types

Within each of these groups order by access:
* public
* internal
* protected
* private
</pre>

<a name="variables"></a>
### 4.2 Variables
XXX

<a name="functions"></a>
### 4.3 Functions
XXX

**[⬆ Back to Top](#table-of-contents)**

<a name="asset-naming-conventions"></a>
## 5. Asset Naming Conventions

### Sections
> 5.1 [Rules](#rules)

> 5.2 [Asset Name Modifiers](#asset-name-modifiers)

Naming conventions should be treated as law. A project that conforms to a naming convention is able to have its assets managed, searched, parsed, and maintained with incredible ease.

**All asset names use [PascalCase](#terms-cases)**

**All asset names should follow the standard of `Prefix_BaseAssetName_Variant_Suffix`.**

<a name="rules"></a>
### 5.1 Rules

All assets should have a _Base Asset Name_. A Base Asset Name represents a logical grouping of related assets. Keeping the pattern `Prefix_BaseAssetName_Variant_Suffix` in mind and using common sense is generally enough to warrant good asset names. Here are some detailed rules regarding each element:
* `Prefix` and `Suffix` are to be determined by the asset type through the following [Asset Name Modifier](#asset-name-modifiers) tables.
* `BaseAssetName` should be determined by short and easily recognizable name related to the context of this group of assets. For example, if you had a character named Bob, all of Bob's assets would have the `BaseAssetName` of `Bob`.
* For _unique and specific variations_ of assets, `Variant` is a short and easily recognizable name that represents logical grouping of assets that are a subset of an asset's base name. For example, if Bob had multiple skins these skins should still use `Bob` as the `BaseAssetName` but include a recognizable `Variant`. An 'Evil' skin would be referred to as `Bob_Evil` and a 'Retro' skin would be referred to as `Bob_Retro`.
* For _unique but generic variations_ of assets, `Variant` is a two digit number starting at `01`. For example, if you have an environment artist generating nondescript rocks, they would be named `Rock_01`, `Rock_02`, `Rock_03`, etc. Except for rare exceptions, you should never require a three digit variant number. If you have more than 100 assets, you should consider organizing them with different base names or using multiple variant names.
* Depending on how your asset variants are made, you can chain together variant names. For example, if you are creating flooring assets for an Arch Viz project you should use the base name `Flooring` with chained variants such as `Flooring_Marble_01`, `Flooring_Maple_01`, `Flooring_Tile_Squares_01`.

Exceptions:
* Scenes
    * Scenes should be named in accordance with the specific [Level Structure](#level-structure) chosen for the project. Thus, `Prefix` and `Suffix` are not determined by asset type, but follow a unique convention (example found under [Asset Name Modifiers(#asset-name-modifiers)]).
* Scripts
    * Unlike other asset types, scripts are all stored in the same folder. Additionally, the contained C# Class must have the same name as the script's asset name. Therefore, scripts should only be named with a `BaseAssetName`.

<a name="asset-name-modifiers"></a>
### 5.2 Asset Name Modifiers

| Asset Type                    | Prefix    | Suffix    | Notes                            |
| ----------------------------- | --------- | --------- | -------------------------------- |
| Scene                         | *         |           | Should be in a folder called [Levels](#level-structure), e.g. `Levels/A4_C17_Parking_Garage.unity` |
| > Persistent                  |           | _P        |                                  |
| > Audio                       |           | _Audio    |                                  |
| > Lighting                    |           | _Lighting |                                  |
| > Geometry                    |           | _Geo      |                                  |
| > Gameplay                    |           | _Gameplay |                                  |
| Script                         |          |           | Should be in a folder called [Scripts](#project-structure), e.g. `Scripts/PlayerMovement.cs` |
| 3D-Model                      |           |           |                                  |
| > Character                   | CH_       |           |                                  |
| > Vehicle                     | VH_       |           |                                  |
| > Weapon                      | WP_       |           |                                  |
| > Static Mesh                 | SM_       |           |                                  |
| > Skeletal Mesh               | SK_       |           |                                  |
| Texture                       | T_        |           |                                  |
| > Diffuse/Albedo/Base Color   |           | _D        |                                  |
| > Normal                      |           | _N        |                                  |
| > Roughness                   |           | _R        |                                  |
| > Alpha/Opacity               |           | _A        |                                  |
| > Ambient Occlusion           |           | _AO       |                                  |
| > Bump                        |           | _B        |                                  |
| > Emissive                    |           | _E        |                                  |
| > Mask                        |           | _M        |                                  |
| > Specular                    |           | _S        |                                  |
| Material                      | M_        |           |                                  |
| Shader                        | SH_       |           |                                  |
| Particle System               | PS_       |           |                                  |
| Render Pipeline               | BRP_/URP_/HDRP_ |     |                                  |

**[⬆ Back to Top](#table-of-contents)**