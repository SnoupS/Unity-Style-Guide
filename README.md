# Unity Style-Guide

This article contains rules regarding project structure and naming conventions for game developement in Unity.

#### Shortcuts
- [Assets Folder Structure](#assets-folder-structure)
- [Scene Structure](#scene-structure)
- [C# Class Structure](#class-structure)
- [Asset Name Modifiers](#asset-name-modifiers)

<a name="toc"></a>
## Table of Contents

> 1. [Introduction](#introduction)
> 1. [Project Structure](#project-structure)
> 2. [Scripts](#scripts)
> 3. [Asset Naming Conventions](#asset-naming-conventions)

<a name="introduction"></a>
## 1. Introduction

#### If your project already has a style guide, you should follow it.
If you are working on a project or with a team that has a pre-existing style guide, it should be respected.  Any inconsistency between an existing style guide and this guide should defer to the existing.

Style guides should be living documents however and you should propose style guide changes to an existing style guide as well as this guide if you feel the change benefits all usages.

> ##### *Arguments over style are pointless. There should be a style guide, and you should follow it.*
> [_Rebecca Murphey_](https://rmurphey.com)

#### All structure, assets, and code in any project should look like a single person created it, no matter how many people contributed.
Moving from one project to another should not cause a re-learning of style and structure. Conforming to a style guide removes unneeded guesswork and ambiguities.

It also allows for more productive creation and maintenance as one does not need to think about style, simply follow instructions. This style guide is written with best practices in mind, meaning that by following this style guide you will also minimize hard to track issues.

#### Friends do not let friends have bad style.
If you see someone working either against a style guide or no style guide, try to correct them.

When working within a team or discussing within a community, it is far easier to help and to ask for help when people are consistent. Nobody likes to help untangle someone's spaghetti code or deal with assets with names they can't understand.

If you are helping someone who's work conforms to a different but consistent and sane style guide, you should be able to adapt to it. If they do not conform to any style guide, please direct them here.

<a name="project-structure"></a>
## 2. Project Structure

### Sections
> 2.1 [Assets Folder Structure](#assets-folder-structure)

> 2.2 [Scene Structure](#scene-structure)

<a name="assets-folder-structure"></a>
### 2.1 Assets Folder Structure

The directory structure style of a project should be considered law. Asset naming conventions and content directory structure go hand in hand, and a violation of either causes unneeded chaos.

In this style, we will be using a structure that relies more on filtering and search abilities of the Project Window for those working with assets to find assets of a specific type instead of another common structure that groups asset types with folders.

> Because we are using a prefix [naming convention](#asset-name-modifiers), using folders to contain assets of similar types such as `Meshes`, `Textures`, and `Materials` is a redundant practice as asset types are already both sorted by prefix as well as able to be filtered in the content browser.
<a name="assets-folder-structure-preview"></a>
<pre>
Assets
    <a name="structure-sandbox">_Sandbox</a>
        DeveloperName
            Testing
            WIP
    <a name="structure-project-specific">ProjectName</a>
            _Levels             // Scenes
                Frontend
                Act1
                    Level1
            FX                  // Particle Systems, Textures, etc.
                Vehicles
            Gameplay            // Meshes, Textures, Prefabs, Materials, etc.
                Characters
                Equipment
                Items
                Vehicles
            MaterialLibrary     // (Debug) Materials, Shaders, Generic Noise Textures, etc.
                Debug
                Shaders
                Utility
            Objects             // Meshes, Textures, Materials, etc.
                Architecture
                Props
            Scripts             // C# Scripts
                AI
                Gameplay
                    Player
                Tools
            Settings            // Input System Assets, Render Pipeline Assets, etc.
                Input
                    Controls
                RenderPipeline
            Sound               // Audio files
            UI                  // UI related assets and resources
                Art
                    Buttons
                Resources
                    Fonts
</pre>

#### 2.1.1 Folder Names

- Always use PascalCase
- Never use spaces
- Never use unicode characters and other symbols
- Start folder name with "_" to move them to the top of the hierarchy

#### 2.1.2 Top Level Folder For Project Specific Assets

All of a project's assets should exist in a folder named after the project. For example, if your project is named 'Generic Shooter', _all_ of it's content should exist in `Assets/GenericShooter`.

> The `Sandbox` folder provides developers separate areas for WIP assets and local testing. Your project does not rely on these assets and so they are not project specific.

> `Third-party Assets` will import directly into the Assets folder. Moving them around can break their functionality and the top level folder for project specific assets ensures nothing gets overwritten, which is why third-party asset imports can be left where they are.

#### 2.1.3 All Scene Files Go In A Folder Called Levels

Level files are incredibly special and it is common for every project to have its own map naming system, especially if they work with sub-levels or streaming levels. No matter what system of map organization is in place for the specific project, all levels should belong in a dedicated levels folder.

Being able to tell someone to open a specific map without having to explain where it is is a great time saver and general 'quality of life' improvement. It is common for levels to be within sub-folders, such as `Levels/Campaign1/` or `Levels/Arenas`, but the most important thing here is that they all exist within `Assets/ProjectNameName/Levels`.

This also simplifies the job of cooking for engineers. Wrangling levels for a build process can be extremely frustrating if they have to dig through arbitrary folders for them. If a team's levels are all in one place, it is much harder to accidentally not cook a map in a build. It also simplifies lighting build scripts as well QA processes.

#### 2.1.4 Very Large Asset Sets Get Their Own Folder Layout

There are certain asset types that have a huge volume of related files where each asset has a unique purpose. The two most common are Animation and Audio assets. If you find yourself having 15+ of these assets that belong together, they should be together.

For example, animations that are shared across multiple characters should lay in `Characters/Common/Animations` and may have sub-folders such as `Locomotion` or `Cinematic`.

#### 2.1.5 MaterialLibrary

If your project makes use of master materials, layered materials, or any form of reusable materials or textures that do not belong to any subset of assets, these assets should be located in `Assets/ProjectName/MaterialLibrary`.

This way all 'global' materials have a place to live and are easily located.

> This also makes it incredibly easy to enforce a 'use material instances only' policy within a project. If all artists and assets should be using material instances, then the only regular material assets that should exist are within this folder. You can easily verify this by searching for base materials in any folder that isn't the `MaterialLibrary`.
The `MaterialLibrary` doesn't have to consist of purely materials. Shared utility textures, material functions, and other things of this nature should be stored here as well within folders that designate their intended purpose. For example, generic noise textures should be located in `MaterialLibrary/Utility`.

Any testing or debug materials should be within `MaterialLibrary/Debug`. This allows debug materials to be easily stripped from a project before shipping and makes it incredibly apparent if production assets are using them if reference errors are shown.

<a name="scene-structure"></a>
### 2.2 Scene Structure
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
## 3. Scripts

### Sections
> 3.1 [Class Structure](#class-structure)

> 3.2 [Naming Conventions](#script-naming-conventions)

> 3.3 [Coding Style](#coding-style)

> 3.4 [Script Template](#script-template)

<a name="class-structure"></a>
### 3.1 Class Structure

Class members should be ordered alphabetically, and grouped into sections:
1. Constant Fields
2. Static Fields
3. Fields
4. Constructors
5. Properties
6. Events / Delegates
7. LifeCycle Methods (Awake, OnEnable, OnDisable, OnDestroy)
8. Public Methods
9. Private Methods
10. Nested types

Within each of these groups, class members should be order by access:
1. public
2. internal
3. protected
4. private

<a name="script-naming-conventions"></a>
### 3.2 Naming Conventions

The naming of class members should follow the following rules:
- Constant Fields: UPPERCASE_VARIABLE
- Static Fields: camelCase
- Fields: camelCase
- Constructors: PascalCase
- Properties: PascalCase
- Events / Delegates: PascalCase
- Methods: PascalCase
- Nested types: PascalCase

<a name="coding-style"></a>
### 3.3 Coding Style

#### 3.3.1 Curly Brackets

A consistent approach for the placing of curly brackets / braces should be adopted. The choice is mostly subjective, but in this Style-Guide, the following format is used:
<pre>
private void Update()
{
    // ...
}
</pre>

Despite scripts becoming more compact when placing curly brackets on the same line and not on a new one, there are other compelling reasons for using the format above:
1. It is in line with [Microsoft's C# Coding Conventions](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions) and Unity's standard
2. The otherwise empty line breaks with the curly brackets provide a symmetrical framing of the code inside, which - especially for longer scripts - can provide a better overview of the code's structure
3. For functions with many different parameters, placing the curly brackets on a new line helps destinguish function parameters from function code. See the two examples below:
<pre>
public void MyFunction(
    Vector2 parameterOne,
    Vector2 parameterTwo,
    int parameterThree,
    int parameterFour) {
    int localOne,
    int localTwo
}
</pre>

<pre>
public void MyFunction(
    Vector2 parameterOne,
    Vector2 parameterTwo,
    int parameterThree,
    int parameterFour)
{
    int localOne,
    int localTwo
}
</pre>

#### 3.3.2 Summaries

All classes and functions that have an access modifier of `public` should have a summary.

<pre>
/// <summary>  
/// Brief summary of what the class does
/// </summary>
public class MyClass : MonoBehaviour
{
    private void Start()
    {
        // ...
    }

    /// <summary>  
    /// Brief summary of what the function does
    /// </summary>
    public void MyFunction()
    {
        // ...
    }
}
</pre>

#### 3.3.3 Serialization

Prefer to use the attribute [SerializeField] instead of making a variable public.

When serializing fields, make use of Attributes to make editor interaction in the inspector easier to understand:
- Always use `Header` to group different fields - common groups are "Config" and "Interactable"
- Use `Tooltop` to add a short description of how changing this value affects the value of this script, if it is not immediately appearant from the variable name
- Use `Range` to use a slider in the inspector and define a value range if the bounds of the variable are known

Example:
<pre>
public class PlayerMovement : MonoBehaviour
{
    [Header("Config")]
    [SerializeField] private Transform playerTransform;

    [Header("Interactable")]
    [Range(0.0f, 25.0f)]
    [SerializeField] private float speed = 10.0f;
    [Tooltip("Gets used up when running and has to recharge when empty. Higher values allow the player to run longer.")]
    [Range(0.0f, 25.0f)]
    [SerializeField] private float stamina = 10.0f;
    
    private void Start()
    {
        // ...
    }
}
</pre>

The following best practices should be considered when serializing data;
- Aim to have Unity serialize the smallest possible set of data
- Don't have Unity serialize duplicate data or cached data
- Avoid nested, recursive structures where you reference other classes

Fields that are serialized and thus show in the editor should

#### 3.3.4 Comments

The following rules should always be followed when adding comments:
- Where ever possible, place comments above the code instead of beside it
- The // (two slashes) style of comment tags should be used in most situations
- Insert one space between the comment delimiter (//) and the comment text
- Begin comment text with an uppercase letter
- End comment text with a period

<a name="script-template"></a>
### 3.4 Script Template

In order to improve the scripting workflow, the base template for new C# scripts can be customized. To do this, navigate to:

> C:\Program Files\Unity\Hub\Editor\2021.3.13f1\Editor\Data\Resources\ScriptTemplates

There, edit the `C# Script-NewBehaviourScript.cs`. In accordance with the [Coding Style](#coding-style) described above, the following template could be used as a bare-bones script setup:
<pre>
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

#ROOTNAMESPACEBEGIN#
/// <summary>  
/// Brief summary of what the class does
/// </summary>
public class #SCRIPTNAME# : MonoBehaviour
{
    [Header("Config")]
    [SerializeField]
    
    private void Start()
    {
    }

    private void Update()
    {
    }
}
#ROOTNAMESPACEEND#
</pre>

**[Back to Top](#table-of-contents)**

<a name="asset-naming-conventions"></a>
## 4. Asset Naming Conventions

### Sections
> 4.1 [Rules](#rules)

> 4.2 [Asset Name Modifiers](#asset-name-modifiers)

**All asset names use PascalCase**

**All asset names should follow the standard of `Prefix_BaseAssetName_Variant_Suffix`.**

<a name="rules"></a>
### 4.1 Rules

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
### 4.2 Asset Name Modifiers

| Asset Type                    | Prefix    | Suffix    | Notes                            |
| ----------------------------- | --------- | --------- | -------------------------------- |
| Scene                         | *         |           | Should be in a folder called [Levels](#assets-folder-structure-preview), e.g. `Levels/A4_C17_Parking_Garage.unity` |
| > Persistent                  |           | _P        |                                  |
| > Audio                       |           | _Audio    |                                  |
| > Lighting                    |           | _Lighting |                                  |
| > Geometry                    |           | _Geo      |                                  |
| > Gameplay                    |           | _Gameplay |                                  |
| Script                        |           |           | Should be in a folder called [Scripts](#assets-folder-structure-preview), e.g. `Scripts/PlayerMovement.cs` |
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
