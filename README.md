# Unity Style-Guide RU

Эта статья содержит конкретные правила разработки игр в Unity, касающиеся структуры проекта, имен ресурсов и сценариев.

#### Быстрый доступ
- [Структура папок с активами](#assets-folder-structure)
- [Структура сцены](#scene-structure)
- [Структура класса](#class-structure)
- [Модификаторы имени актива](#asset-name-modifiers)

<a name="toc"></a>
## Оглавление

> 1. [Введение](#introduction)
> 2. [Структура проекта](#project-structure)
> 3. [Скрипты](#scripts)
> 4. [Соглашения об именовании активов](#asset-naming-conventions)

<a name="introduction"></a>
## 1. Введение

#### Если вы работаете над проектом или с командой, у которой есть уже существующее руководство по стилю, его следует уважать. В случае несоответствия между существующим руководством по стилю и данным руководством следует отдать предпочтение существующему.

Однако руководства по стилю должны быть живыми документами, и вы должны предлагать изменения в существующем руководстве по стилю, а также в данном руководстве, если вы считаете, что изменения будут полезны для всех пользователей.

> ##### *Споры о стиле бессмысленны. Руководство по стилю должно быть, и вы должны ему следовать.*
> [_Ребекка Мерфи_](https://rmurphey.com) 

#### Вся структура, активы и код в любом проекте должны выглядеть так, как будто его создал один человек, независимо от того, сколько людей внесли свой вклад.
Переход от одного проекта к другому не должен приводить к повторному изучению стиля и структуры. Соблюдение руководства по стилю устраняет ненужные догадки и двусмысленности.

Это также позволяет более продуктивно создавать и поддерживать проект, поскольку не нужно думать о стиле, достаточно просто следовать инструкциям. Данное руководство по стилю составлено с учетом лучших практик, а это значит, что, следуя ему, вы также сведете к минимуму трудно отслеживаемые проблемы.

#### Друзья не позволяют друзьям иметь плохой стиль.
Если вы видите, что кто-то работает вразрез с руководством по стилю или вообще без него, постарайтесь его поправить.

При работе в команде или обсуждении в сообществе гораздо легче помогать и просить о помощи, когда люди последовательны. Никому не нравится помогать распутывать чей-то спагетти-код или работать с активами с непонятными названиями.

Если вы помогаете кому-то, чья работа соответствует другому, но последовательному и здравому руководству по стилю, вы должны быть в состоянии адаптироваться к нему. Если они не соответствуют никакому руководству по стилю, пожалуйста, направьте их сюда.

<a name="project-structure"></a>
## 2. Структура проекта

### Разделы
> 2.1 [Структура папок с активами](#assets-folder-structure)

> 2.2 [Структура сцены](#scene-structure)

<a name="assets-folder-structure"></a>
### 2.1 Структура папок с активами

Стиль структуры каталогов проекта следует считать законом. Соглашения об именовании активов и структура каталогов контента идут рука об руку, и нарушение любого из них приводит к ненужному хаосу.

В этом стиле мы будем использовать структуру, которая больше полагается на возможности фильтрации и поиска в окне проекта для тех, кто работает с активами, чтобы найти активы определенного типа, вместо другой распространенной структуры, которая группирует типы активов в папки.

> Поскольку мы используем [соглашения об именовании активов](#asset-name-modifiers), использование папок для содержания активов схожих типов, таких как `Meshes`, `Models`, `Textures` и `Materials`, является излишней практикой, поскольку типы активов уже отсортированы по префиксу, а также могут быть отфильтрованы в браузере контента.
<a name="assets-folder-structure-preview"></a>
<pre>
Assets
    <a name="structure-developers">_Developers</a>
        DeveloperName
            (Незавершенные активы)
    <a name="structure-project-specific">ProjectName</a>
            _Levels             // Сцены.
                Frontend
                Act1
                    Level1
            _Scripts             // C# Скрипты.
                AI
                Gameplay
                    Player
                Tools
            FX                  // Системы частиц, текстуры и т.д.
                Vehicles
            Gameplay            // Меши, текстуры, префабы, материалы и т.д.
                Characters
                Equipment
                Items
                Vehicles
            MaterialLibrary     // (Отладка) Материалы, шейдеры, общие текстуры шума и т.д.
                Debug
                Shaders
                Utility
            Objects             // Меши, текстуры, материалы и т.д.
                Architecture
                Props
            Settings            // Активы системы ввода, ресурсы конвейера рендеринга и т.д.
                Input
                    Controls
                RenderPipeline
            Sound               // Аудио файлы.
            UI                  // Активы и ресурсы, связанные с пользовательским интерфейсом.
                Art
                    Buttons
                Resources
                    Fonts
</pre>

#### 2.1.1 Имена папок

- Всегда используйте PascalCase
- Никогда не используйте пробелы
- Никогда не используйте символы Юникода и другие символы
- Начинайте имя папки с "_", чтобы переместить их на вершину иерархии

#### 2.1.2 Папка верхнего уровня для активов конкретного проекта

Все активы проекта должны существовать в папке, названной по имени проекта. Например, если ваш проект называется `Generic Shooter`, все его содержимое должно находиться в папке `Assets/GenericShooter`.

> Папка `_Developers` предоставляет разработчикам отдельные области для разработки активов и локального тестирования. Ваш проект не должен зависить от этих активов.

> `Third-party Assets` будут импортироваться непосредственно в папку Assets. Их перемещение может нарушить их функциональность, а папка верхнего уровня для специфических активов проекта гарантирует, что ничего не будет перезаписано, поэтому импорт сторонних активов можно оставить на месте.

#### 2.1.3 Все файлы сцен помещаются в папку Levels

Файлы уровней невероятно необычны, и обычно каждый проект имеет свою собственную систему именования сцен, особенно если он работает с подуровнями или потоковыми уровнями. Независимо от того, какая система организации карт используется в конкретном проекте, все уровни должны находиться в специальной папке Levels.

Возможность сказать кому-то открыть определенную сцену без необходимости объяснять, где она находится, значительно экономит время и улучшает общее "качество жизни". Обычно уровни находятся в подпапках, таких как `Levels/Campaign1/` или `Levels/Arenas`, но самое главное, чтобы все они существовали в папке `Assets/ProjectName/Levels`.

Это также упрощает работу по сборке проекта. Поиск уровней для процесса сборки может быть крайне утомительным, если приходится рыться в произвольных папках. Если все уровни находятся в одном месте, гораздо сложнее случайно не добавить сцену в сборку. Это упрощает сборку освещения, а также процессы QA.

#### 2.1.4 Очень большие наборы активов получают собственное расположение папок

Существуют определенные типы активов, которые имеют огромный объем связанных файлов, где каждый актив имеет уникальное назначение. Два наиболее распространенных типа активов - это анимация и аудио. Если у вас есть 15+ таких активов, которые должны быть вместе, они должны быть вместе.

Например, анимации, общие для нескольких персонажей, должны лежать в папке `Characters/Common/Animations` и могут иметь подпапки `Locomotion` или `Cinematic`.

#### 2.1.5 Библиотека материалов

Если в вашем проекте используются мастер-материалы, многослойные материалы или любые другие виды повторно используемых материалов или текстур, которые не принадлежат к какому-либо подмножеству активов, эти активы должны быть расположены в `Assets/ProjectName/MaterialLibrary`.

Таким образом, все "глобальные" материалы имеют свое место и легко находятся.

> Это также упрощает применение политики "использования только экземпляров материалов" в проекте. Если все художники и активы должны использовать экземпляры материалов, то единственные обычные материальные активы, которые должны существовать, находятся в этой папке. Вы можете легко убедиться в этом, поискав базовые материалы в любой папке, не входящей в `MaterialLibrary`.
Библиотека `MaterialLibrary` не обязательно должна состоять только из материалов. Общие полезные текстуры, функции материалов и другие вещи такого рода также должны храниться здесь в папках, обозначающих их назначение. Например, общие текстуры шума должны быть расположены в `MaterialLibrary/Utility`.

Любые тестовые или отладочные материалы должны находиться в папке `MaterialLibrary/Debug`. Это позволяет легко удалять отладочные материалы из проекта перед отправкой и делает невероятно очевидным использование их в производственных активах, если появляются ошибки в ссылках.

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

> 3.2 [Соглашения об именовании](#script-naming-conventions)

> 3.3 [Стиль кода](#code-style)

> 3.4 [Шаблон скрипта](#script-template)

<a name="class-structure"></a>
### 3.1 Структура класса

Члены класса должны быть расположены в алфавитном порядке и сгруппированы по разделам:
1. Константные поля
2. Статические поля
3. Поля
4. Конструкторы
5. Свойства
6. События / делегаты
7. Методы жизненного цикла (Awake, OnEnable, OnDisable, OnDestroy)
8. Публичные методы
9. Приватные методы
10. Вложенные типы

Внутри каждой из этих групп члены класса должны быть упорядочены по доступу:
1. публичный
2. внутренний
3. защищенный
4. приватный

<a name="script-naming-conventions"></a>
### 3.2 Соглашения об именовании

Именование членов класса должно соответствовать этим правилам:
- Константные поля: UPPERCASE_VARIABLE
- Поля:
    - Публичные: CamelCase
    - Приватные: _camelCase
- Конструкторы: PascalCase
- Свойства: PascalCase
- События / делегаты: PascalCase
- Методы: PascalCase
- Вложенные типы: PascalCase

<a name="code-style"></a>
### 3.3 Стиль кода

#### 3.3.1 Фигурные скобки

Следует придерживаться последовательного подхода к размещению фигурных/круглых скобок. Выбор в основном субъективен, но в данном Руководстве по стилю используется следующий формат:
<pre>
private void Update()
{
    // ...
}
</pre>

Несмотря на то, что сценарии становятся более компактными при размещении фигурных скобок на той же строке, а не на новой, есть и другие веские причины для использования приведенного выше формата:
1. Он соответствует [Соглашения Microsoft о написании кода C#](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions) и стандарту Unity.
2. Иначе пустые разрывы строк с фигурными скобками обеспечивают симметричное обрамление кода внутри, что - особенно для длинных скриптов - может дать лучший обзор структуры кода.
3. Для функций с большим количеством различных параметров размещение фигурных скобок на новой строке помогает отделить параметры функции от кода функции. Смотрите два примера ниже:

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

#### 3.3.2 Краткое описание

Все классы и функции, имеющие модификатор доступа `public`, должны иметь краткое описание.

```
/// <summary>  
/// Краткое описание того, что делает класс
/// </summary>
public class MyClass : MonoBehaviour
{
    private void Start()
    {
        // ...
    }

    /// <summary>  
    /// Краткое описание того, что делает функция
    /// </summary>
    public void MyFunction()
    {
        // ...
    }
}
```

#### 3.3.3 Сериализация

Предпочтительно использовать атрибут [SerializeField] вместо того, чтобы делать переменную публичной.

При сериализации полей используйте атрибуты, чтобы сделать взаимодействие с редактором в инспекторе более понятным:
- Всегда используйте `Header` для группировки различных полей - распространенными группами являются "Config" и "Interactable".
- Используйте `Tooltop` для добавления краткого описания того, как изменение этого значения влияет на значение этого скрипта, если это не видно сразу из имени переменной.
- Используйте `Range`, чтобы использовать ползунок в инспекторе и определить диапазон значений, если границы переменной известны.

Пример:
<pre>
public class PlayerMovement : MonoBehaviour
{
    [Header("Config")]
    [SerializeField] private Transform _playerTransform;

    [Header("Interactable")]
    [Range(0.0f, 25.0f)]
    [SerializeField] private float _speed = 10.0f;
    [Tooltip("Определяет выносливость игрока, которая расходуется при беге.")]
    [Range(0.0f, 25.0f)]
    [SerializeField] private float _stamina = 10.0f;
    
    private void Start()
    {
        // ...
    }
}
</pre>

При сериализации данных следует учитывать следующие передовые методы:
- Стремитесь к тому, чтобы Unity сериализовала минимально возможный набор данных.
- Не заставляйте Unity сериализовать дубликаты данных или кэшированные данные.
- Избегайте вложенных, рекурсивных структур, в которых вы ссылаетесь на другие классы.

#### 3.3.4 Комментарии

Комментирование должно соответствовать следующим правилам:
- Где это возможно, размещайте комментарии над кодом, а не рядом с ним.
- В большинстве ситуаций следует использовать теги комментариев в стиле // (две косые черты).
- Вставьте один пробел между разделителем комментариев (//) и текстом комментария
- Начинайте текст комментария с заглавной буквы
- Заканчивайте текст комментария точкой

<a name="script-template"></a>
### 3.4 Шаблон скрипта

Чтобы улучшить рабочий процесс создания сценариев, базовый шаблон для новых сценариев C# можно настроить. Для этого перейдите в:

`*\Unity\Hub\Editor\2021.3.13f1\Editor\Data\Resources\ScriptTemplates`.

Там отредактируйте `C# Script-NewBehaviourScript.cs`. В соответствии с описанным выше [стилем кодирования](#coding-style), [этот шаблон](ScriptTemplate.txt) может быть использован в качестве базовой установки скрипта.

**[Наверх](#table-of-contents)**

<a name="asset-naming-conventions"></a>
## 4. Соглашения об именовании активов

### Разделы
> 4.1 [Правила](#rules)

> 4.2 [Модификаторы имени актива](#asset-name-modifiers)

**Все имена активов используют PascalCase**.

**Все имена активов должны соответствовать стандарту `Prefix_BaseAssetName_Variant_Suffix`.**

<a name="rules"></a>
### 4.1 Правила

Все активы должны иметь _Base Asset Name_. Оно представляет собой логическую группировку связанных активов.

Ниже приведены подробные правила, касающиеся каждого элемента:
* `Prefix` и `Suffix` определяются типом актива с помощью следующей таблицы [Модификаторы имени актива](#asset-name-modifiers).
* `BaseAssetName` должно быть коротким и легко узнаваемым именем, связанным с контекстом данной группы активов. Например, если у вас есть персонаж по имени Боб, то все активы Боба будут иметь `BaseAssetName` - `Bob`.
* Для _уникальных и специфических вариаций_ активов, `Variant` - это короткое и легко узнаваемое имя, которое представляет логическую группу активов, являющихся подмножеством базового имени актива. Например, если у Боба есть несколько скинов, эти скины должны по-прежнему использовать `Bob` в качестве `BaseAssetName`, но включать узнаваемый `Variant`. Скин "Злой" будет называться `Bob_Evil`.
* Для _уникальных, но общих вариаций_ активов, `Variant` - это двузначный номер, начинающийся с `01`. Например, если у вас есть художник среды, создающий неописуемые камни, они будут называться `Rock_01`, `Rock_02`, `Rock_03` и т.д. За редким исключением, вам никогда не следует требовать трехзначный номер варианта. Если у вас более 100 активов, вам следует рассмотреть возможность организации их с разными базовыми именами или использования нескольких вариантов имен.
* В зависимости от того, как создаются варианты активов, вы можете объединять имена вариантов в цепочки. Например, если вы создаете активы напольных покрытий, вам следует использовать базовое имя `Flooring` с цепочкой вариантов, таких как `Flooring_Marble_01`, `Flooring_Maple_01`, `Flooring_Tile_Squares_01`.

Исключения:
* Сцены
    * Сцены должны быть названы в соответствии с конкретной [структурой уровней](#level-structure), выбранной для проекта. Таким образом, `Prefix` и `Suffix` не определяются типом актива, а следуют уникальному соглашению (пример можно найти в разделе [Модификаторы имени актива(#asset-name-modifiers)]).
* Скрипты
    * В отличие от других типов активов, скрипты хранятся в одной папке. Кроме того, содержащийся класс C# должен иметь то же имя, что и имя актива скрипта. Поэтому скрипты должны быть названы только с `BaseAssetName`.

<a name="asset-name-modifiers"></a>
### 4.2 Модификаторы имени актива

| Тип актива                    | Префикс   | Суффикс   | Примечание                       |
| ----------------------------- | --------- | --------- | -------------------------------- |
| Scene                         | *         |           | Должен находиться в папке с именем [Levels](#assets-folder-structure-preview), например `_Levels/A4_C17_Parking_Garage.unity` |
| > Persistent                  |           | _P        |                                  |
| > Audio                       |           | _Audio    |                                  |
| > Lighting                    |           | _Lighting |                                  |
| > Geometry                    |           | _Geo      |                                  |
| > Gameplay                    |           | _Gameplay |                                  |
| |  |  |  |
| Script                        |           |           | Должен находиться в папке с именем [Scripts](#assets-folder-structure-preview), например `_Scripts/PlayerMovement.cs` |
| |  |  |  |
| 3D-Model                      |           |           |                                  |
| > Character                   | CH_       |           |                                  |
| > Vehicle                     | VH_       |           |                                  |
| > Weapon                      | WP_       |           |                                  |
| > Static Mesh                 | SM_       |           |                                  |
| > Skeletal Mesh               | SK_       |           |                                  |
| |  |  |  |
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
| > UI Sprite                   |           | _GUI      |                                  |
| |  |  |  |
| Material                      | M_        |           |                                  |
| Shader                        | SH_       |           |                                  |
| Particle System               | PS_       |           |                                  |
| Audio Clip                    | A_        |           |                                  |
| Animation Controller	        | AC_       |           |                                  |
| Dialogue Voice                | DV_       |           |                                  |
| Render Pipeline               | BRP_/URP_/HDRP_ |     |                                  |

**[Наверх](#table-of-contents)**
