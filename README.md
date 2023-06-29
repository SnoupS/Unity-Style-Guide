# Unity Style-Guide RU

Эта статья содержит конкретные правила разработки игр в Unity, касающиеся структуры проекта, имен ресурсов и сценариев.

#### Ярлыки
- [Структура папки активов](#assets-folder-structure)
- [Структура сцены](#scene-structure)
- [Структура класса С#](#class-structure)
- [Модификаторы имени актива](#asset-name-modifiers)

<a name="toc"></a>
## Оглавление

> 1. [Введение](#introduction)
> 2. [Структура проекта](#project-structure)
> 3. [Скрипты](#scripts)
> 4. [Соглашения об именах активов](#asset-naming-conventions)

<a name="introduction"></a>
## 1. Введение

#### Если в вашем проекте уже есть руководство по стилю, вы должны следовать ему.
Если вы работаете над проектом или с командой, у которой уже есть руководство по стилю, его следует уважать. Любое несоответствие между существующим руководством по стилю и этим руководством должно относиться к существующему.

Однако руководства по стилю должны быть живыми документами, и вам следует предлагать изменения руководства по стилю в существующем руководстве по стилю, а также в этом руководстве, если вы чувствуете, что изменение принесет пользу всем пользователям.

> ##### *Споры о стиле бессмысленны. Должно быть руководство по стилю, и вы должны ему следовать.*
> [_Ребекка Мерфи_] (https://rmurphey.com)

#### Вся структура, активы и код в любом проекте должны выглядеть так, как будто их создал один человек, независимо от того, сколько людей внесли свой вклад.
Переход от одного проекта к другому не должен вызывать повторного изучения стиля и структуры. Соответствие руководству по стилю устраняет ненужные догадки и двусмысленности.

Это также позволяет более продуктивно создавать и поддерживать, поскольку не нужно думать о стиле, просто следуйте инструкциям. Это руководство по стилю написано с учетом лучших практик, а это означает, что, следуя этому руководству по стилю, вы также сведете к минимуму проблемы, которые трудно отследить.

#### Друзья не позволяйте друзьям иметь плохой стиль.
Если вы видите, что кто-то работает либо против руководства по стилю, либо без руководства по стилю, постарайтесь исправить его.

При работе в команде или обсуждении в сообществе гораздо легче помогать и просить о помощи, когда люди последовательны. Никто не любит помогать распутывать чей-то спагетти-код или иметь дело с активами с именами, которые они не могут понять.

Если вы помогаете кому-то, чья работа соответствует другому, но последовательному и разумному руководству по стилю, вы должны быть в состоянии адаптироваться к нему. Если они не соответствуют какому-либо руководству по стилю, направьте их сюда.

<a name="project-structure"></a>
## 2. Структура проекта

### Разделы
> 2.1 [Структура папки активов](#assets-folder-structure)

> 2.2 [Структура сцены](#scene-structure)

<a name="assets-folder-structure"></a>
### 2.1 Структура папки активов

Стиль структуры каталогов проекта следует считать законом. Соглашения об именовании активов и структура каталогов содержимого идут рука об руку, и нарушение любого из них приводит к ненужному хаосу.

В этом стиле мы будем использовать структуру, которая больше полагается на возможности фильтрации и поиска в окне проекта для тех, кто работает с активами, чтобы найти активы определенного типа, вместо другой общей структуры, которая группирует типы активов с папками.

> Поскольку мы используем префикс [соглашение об именах](#asset-name-modifiers), использование папок для хранения ресурсов похожих типов, таких как `Сети`, `Текстуры` и `Материалы`, является избыточной практикой, поскольку типы активов уже отсортированы по префиксу, а также могут быть отфильтрованы в браузере контента.
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

#### 2.1.1 Имена папок

- Всегда используйте PascalCase
- Никогда не используйте пробелы
- Никогда не используйте символы Юникода и другие символы
- Начинайте имя папки с «_», чтобы переместить их на вершину иерархии.

#### 2.1.2 Папка верхнего уровня для конкретных активов проекта

Все активы проекта должны находиться в папке с именем проекта. Например, если ваш проект называется `Generic Shooter`, _все_ его содержимое должно существовать в `Assets/GenericShooter`.

> Папка `Sandbox` предоставляет разработчикам отдельные области для ресурсов WIP и локального тестирования. Ваш проект не использует эти активы, поэтому они не зависят от конкретного проекта.

> `Third-party Assets` будут импортированы непосредственно в папку «Активы». Их перемещение может нарушить их функциональность, а папка верхнего уровня для конкретных ресурсов проекта гарантирует, что ничего не будет перезаписано, поэтому импорт сторонних ресурсов можно оставить там, где они есть.

#### 2.1.3 Все файлы сцены помещаются в папку с названием Levels

Файлы уровней невероятно особенные, и каждый проект обычно имеет свою собственную систему именования карт, особенно если они работают с подуровнями или потоковыми уровнями. Независимо от того, какая система организации карты используется для конкретного проекта, все уровни должны находиться в отдельной папке уровней.

Возможность сказать кому-то открыть конкретную карту, не объясняя, где она находится, — это отличная экономия времени и общее улучшение «качества жизни». Обычно уровни находятся в подпапках, таких как `Levels/Campaign1/` или `Levels/Arenas`, но самое главное здесь то, что все они существуют в `Assets/ProjectNameName/Levels`.

Это также упрощает работу инженеров по приготовлению пищи. Борьба с уровнями для процесса сборки может быть чрезвычайно неприятной, если им приходится копаться в произвольных папках для них. Если уровни команды находятся в одном месте, то случайно не сварить карту в билде гораздо сложнее. Это также упрощает сценарии сборки освещения, а также процессы контроля качества.

#### 2.1.4 Очень большие наборы ресурсов получают собственный макет папки

Существуют определенные типы активов, которые имеют огромный объем связанных файлов, где каждый ресурс имеет уникальное назначение. Двумя наиболее распространенными являются анимация и аудио активы. Если вы обнаружите, что у вас есть более 15 таких активов, которые принадлежат друг другу, они должны быть вместе.

Например, анимация, которая используется несколькими персонажами, должна лежать в `Characters/Common/Animations` и может иметь подпапки, такие как `Locomotion` или `Cinematic`.

#### 2.1.5 Библиотека материалов

Если в вашем проекте используются мастер-материалы, многослойные материалы или любые формы повторно используемых материалов или текстур, которые не принадлежат ни к какому подмножеству ресурсов, эти ресурсы должны быть расположены в `Assets/ProjectName/MaterialLibrary`.

Таким образом, все «глобальные» материалы имеют место для жизни и легко обнаруживаются.

> Это также позволяет невероятно легко применять политику «использовать только экземпляры материала» в рамках проекта. Если все исполнители и активы должны использовать экземпляры материалов, то в этой папке должны существовать только обычные материальные активы. Вы можете легко убедиться в этом, выполнив поиск базовых материалов в любой папке, кроме `MaterialLibrary`.
`MaterialLibrary` не обязательно должна состоять только из материалов. Общие служебные текстуры, функции материалов и другие подобные вещи также должны храниться здесь, а также в папках, обозначающих их предназначение. Например, общие текстуры шума должны находиться в `MaterialLibrary/Utility`.

Любые материалы для тестирования или отладки должны находиться в `MaterialLibrary/Debug`. Это позволяет легко удалять отладочные материалы из проекта перед отправкой и делает невероятно очевидным, используются ли они в производственных активах, если отображаются справочные ошибки.

<a name="scene-structure"></a>
### 2.2 Структура сцены
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

**[Наверх](#table-of-contents)**

<a name="scripts"></a>
## 3. Скрипты

### Разделы
> 3.1 [Структура класса](#class-structure)

> 3.2 [Соглашения об именах](#script-naming-conventions)

> 3.3 [Стиль кода](#code-style)

> 3.4 [Шаблон скрипта](#script-template)

<a name="class-structure"></a>
### 3.1 Структура класса

Члены класса должны быть упорядочены в алфавитном порядке и сгруппированы в разделы:
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

Внутри каждой из этих групп члены класса должны быть упорядочены по доступу:
1. public
2. internal
3. protected
4. private

<a name="script-naming-conventions"></a>
### 3.2 Соглашения об именах

Именование членов класса должно соответствовать следующим правилам:
- Константные поля: UPPERCASE_VARIABLE
- Статические поля: camelCase
- Поля: верблюжий регистр
- Конструкторы: PascalCase
- Свойства: PascalCase
- События/Делегаты: PascalCase
- Методы: PascalCase
- Вложенные типы: PascalCase

<a name="code-style"></a>
### 3.3 Стиль кода

#### 3.3.1 Фигурные скобки

Следует применять последовательный подход к размещению фигурных скобок/скобок. Выбор в основном субъективен, но в этом Руководстве по стилю используется следующий формат:
<pre>
private void Update()
{
    // ...
}
</pre>

Несмотря на то, что скрипты становятся более компактными при размещении фигурных скобок на той же строке, а не на новой, есть и другие веские причины для использования вышеуказанного формата:
1. Это соответствует [Соглашениям о кодировании C# Microsoft] (https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions) и стандарту Unity.
2. В противном случае пустые разрывы строк с фигурными скобками обеспечивают симметричное обрамление кода внутри, что — особенно для более длинных скриптов — может обеспечить лучший обзор структуры кода.
3. Для функций с большим количеством различных параметров размещение фигурных скобок на новой строке помогает отличить параметры функции от кода функции. См. два примера ниже:
Плохой пример:
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
Хороший пример:
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

#### 3.3.2 Краткое содержание

Все классы и функции, имеющие модификатор доступа public, должны иметь краткое содержание.

```
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
```

#### 3.3.3 Сериализация

Лучше использовать атрибут [SerializeField] вместо того, чтобы делать переменную общедоступной.

При сериализации полей используйте атрибуты, чтобы облегчить понимание взаимодействия с редактором в инспекторе:
- Всегда используйте `Заголовок` для группировки различных полей — распространенными группами являются `Конфигурация` и `Взаимодействующие`.
- Используйте `Tooltop`, чтобы добавить краткое описание того, как изменение этого значения влияет на значение этого скрипта, если оно сразу не появляется из имени переменной.
- Используйте `Диапазон`, чтобы использовать ползунок в инспекторе и определить диапазон значений, если известны границы переменной.
Пример:
<pre>
public class PlayerMovement : MonoBehaviour
{
    [Header("Config")]
    [SerializeField] private Transform playerTransform;

    [Header("Interactable")]
    [Range(0.0f, 25.0f)]
    [SerializeField] private float speed = 10.0f;
    [Tooltip("Determines the Player's stamina, which gets used up when running.")]
    [Range(0.0f, 25.0f)]
    [SerializeField] private float stamina = 10.0f;
    
    private void Start()
    {
        // ...
    }
}
</pre>

При сериализации данных следует учитывать следующие рекомендации:
- Стремитесь к тому, чтобы Unity сериализовала наименьший возможный набор данных.
- Unity не сериализует повторяющиеся данные или кэшированные данные.
- Избегайте вложенных рекурсивных структур, в которых вы ссылаетесь на другие классы.

#### 3.3.4 Комментарии

Комментирование должно соответствовать следующим правилам:
- По возможности размещайте комментарии над кодом, а не рядом с ним.
- В большинстве ситуаций следует использовать стиль тегов комментариев // (две косые черты).
- Вставьте один пробел между разделителем комментария (//) и текстом комментария
- Начинайте текст комментария с заглавной буквы
- Конец текста комментария точкой

<a name="script-template"></a>
### 3.4 Шаблон скрипта

Чтобы улучшить рабочий процесс программирования, можно настроить базовый шаблон для новых скриптов C#. Для этого перейдите к:

`*\Unity\Hub\Editor\2021.3.13f1\Editor\Data\Resources\ScriptTemplates`

Там отредактируйте файл `C# Script-NewBehaviourScript.cs`. В соответствии со [Стилем кода](#code-style) описано выше, [этот шаблон](Unity_ScriptTemplate.txt) можно использовать в качестве базового скрипта.

**[Наверх](#table-of-contents)**

<a name="asset-naming-conventions"></a>
## 4. Соглашения об именовании активов

### Разделы
> 4.1 [Правила](#rules)

> 4.2 [Модификаторы имени актива](#asset-name-modifiers)

**Все имена активов используют PascalCase**

**Все имена активов должны соответствовать стандарту `Prefix_BaseAssetName_Variant_Suffix`.**

<a name="rules"></a>
### 4.1 Правила

Все активы должны иметь _BaseAssetName_. Оно представляет собой логическую группу связанных активов.

Вот несколько подробных правил относительно каждого элемента:
* `Prefix` and `Suffix` are to be determined by the asset type through the following [Asset Name Modifier](#asset-name-modifiers) table.
* `BaseAssetName` should be a short and easily recognizable name related to the context of this group of assets. For example, if you had a character named Bob, all of Bob's assets would have the `BaseAssetName` of `Bob`.
* For _unique and specific variations_ of assets, `Variant` is a short and easily recognizable name that represents logical grouping of assets that are a subset of an asset's base name. For example, if Bob had multiple skins these skins should still use `Bob` as the `BaseAssetName` but include a recognizable `Variant`. An 'Evil' skin would be referred to as `Bob_Evil`.
* For _unique but generic variations_ of assets, `Variant` is a two digit number starting at `01`. For example, if you have an environment artist generating nondescript rocks, they would be named `Rock_01`, `Rock_02`, `Rock_03`, etc. Except for rare exceptions, you should never require a three digit variant number. If you have more than 100 assets, you should consider organizing them with different base names or using multiple variant names.
* Depending on how your asset variants are made, you can chain together variant names. For example, if you are creating flooring assets for an Arch Viz project you should use the base name `Flooring` with chained variants such as `Flooring_Marble_01`, `Flooring_Maple_01`, `Flooring_Tile_Squares_01`.

Исключения:
* Сцены
    * Scenes should be named in accordance with the specific [Level Structure](#level-structure) chosen for the project. Thus, `Prefix` and `Suffix` are not determined by asset type, but follow a unique convention (example found under [Asset Name Modifiers(#asset-name-modifiers)]).
* Скрипты
    * Unlike other asset types, scripts are all stored in the same folder. Additionally, the contained C# Class must have the same name as the script's asset name. Therefore, scripts should only be named with a `BaseAssetName`.

<a name="asset-name-modifiers"></a>
### 4.2 Модификаторы имени актива

| Тип актива                    | Префикс   | Суффикс   | Примечание                       |
| ----------------------------- | --------- | --------- | -------------------------------- |
| Scene                         | *         |           | Должен находиться в папке с именем [Levels](#assets-folder-structure-preview), например `Levels/A4_C17_Parking_Garage.unity` |
| > Persistent                  |           | _P        |                                  |
| > Audio                       |           | _Audio    |                                  |
| > Lighting                    |           | _Lighting |                                  |
| > Geometry                    |           | _Geo      |                                  |
| > Gameplay                    |           | _Gameplay |                                  |
| Script                        |           |           | Должен находиться в папке с именем [Scripts](#assets-folder-structure-preview), например `Scripts/PlayerMovement.cs` |
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

**[Наверх](#table-of-contents)**
