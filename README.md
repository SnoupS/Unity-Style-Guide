# Unity Style Guide

This article contains rules regarding project structure and naming conventions for game developement in Unity. It is designed to be as compact as possible in order to provide a quick overview, for detailed thoughts and considerations behind this style-guide see [this document](https://www.google.de/).

<a name="toc"></a>
## Table of Contents

> 1. [Project Structure](#project-structure)
> 2. [Scripts](#scripts)
> 3. [Asset Naming Conventions](#asset-naming-conventions)

<a name="project-structure"></a>
## 1. Project Structure

### Sections
> 1.1 [Assets Folder Structure](#assets-folder-structure)

> 1.2 [Scene Structure](#scene-structure)

<a name="assets-folder-structure"></a>
### 1.1 Assets Folder Structure
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
### 1.2 Scene Structure
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

**[Back to Top](#table-of-contents)**

<a name="scripts"></a>
## 2. Scripts

### Sections
> 2.1 [Class Structure](#class-structure)

> 2.2 [Variables](#variables)

> 2.3 [Functions](#functions)

<a name="class-structure"></a>
### 2.1 Class Structure
<pre>
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
### 2.2 Variables
XXX

<a name="functions"></a>
### 2.3 Functions
XXX

**[Back to Top](#table-of-contents)**

<a name="asset-naming-conventions"></a>
## 3. Asset Naming Conventions

### Sections
> 3.1 [Rules](#rules)

> 3.2 [Asset Name Modifiers](#asset-name-modifiers)

**All asset names use PascalCase**

**All asset names should follow the standard of `Prefix_BaseAssetName_Variant_Suffix`.**

<a name="rules"></a>
### 3.1 Rules

All assets should have a _Base Asset Name_. It represents a logical grouping of related assets.

Here are some detailed rules regarding each element:
* `Prefix` and `Suffix` are to be determined by the asset type through the following [Asset Name Modifier](#asset-name-modifiers) table.
* `BaseAssetName` should be a short and easily recognizable name related to the context of this group of assets. For example, if you had a character named Bob, all of Bob's assets would have the `BaseAssetName` of `Bob`.
* For _unique and specific variations_ of assets, `Variant` is a short and easily recognizable name that represents logical grouping of assets that are a subset of an asset's base name. For example, if Bob had multiple skins these skins should still use `Bob` as the `BaseAssetName` but include a recognizable `Variant`. An 'Evil' skin would be referred to as `Bob_Evil`.
* For _unique but generic variations_ of assets, `Variant` is a two digit number starting at `01`. For example, if you have an environment artist generating nondescript rocks, they would be named `Rock_01`, `Rock_02`, `Rock_03`, etc. Except for rare exceptions, you should never require a three digit variant number. If you have more than 100 assets, you should consider organizing them with different base names or using multiple variant names.
* Depending on how your asset variants are made, you can chain together variant names. For example, if you are creating flooring assets for an Arch Viz project you should use the base name `Flooring` with chained variants such as `Flooring_Marble_01`, `Flooring_Maple_01`, `Flooring_Tile_Squares_01`.

Exceptions:
* Scenes
    * Scenes should be named in accordance with the specific [Level Structure](#level-structure) chosen for the project. Thus, `Prefix` and `Suffix` are not determined by asset type, but follow a unique convention (example found under [Asset Name Modifiers(#asset-name-modifiers)]).
* Scripts
    * Unlike other asset types, scripts are all stored in the same folder. Additionally, the contained C# Class must have the same name as the script's asset name. Therefore, scripts should only be named with a `BaseAssetName`.

<a name="asset-name-modifiers"></a>
### 3.2 Asset Name Modifiers

| Asset Type                    | Prefix    | Suffix    | Notes                            |
| ----------------------------- | --------- | --------- | -------------------------------- |
| Scene                         | *         |           | Should be in a folder called [Levels](#level-structure), e.g. `Levels/A4_C17_Parking_Garage.unity` |
| > Persistent                  |           | _P        |                                  |
| > Audio                       |           | _Audio    |                                  |
| > Lighting                    |           | _Lighting |                                  |
| > Geometry                    |           | _Geo      |                                  |
| > Gameplay                    |           | _Gameplay |                                  |
| Script                        |           |           | Should be in a folder called [Scripts](#project-structure), e.g. `Scripts/PlayerMovement.cs` |
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

**[Back to Top](#table-of-contents)**