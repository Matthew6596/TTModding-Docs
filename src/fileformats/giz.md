# GIZ Files

**GIZ** files are a proprietary format used in TTGames LEGO video games to store interactable elements of a level such as levers, studs, and more.

This format is not officially documented by TTGames. The current understanding comes from community research.

## 📦 Overview

- **File extension:** `.giz`
- **Category:** Level
- **Used for:** Non-AI interactable elements in levels
- **Official name:** Gizmo

## 🎮 Usage in games

The file format was introduced in _.

## 🛠️ Working with GIZ files

Some sections of the GIZ file can be edited in BrickBench, but you can always use a Hex Editor as well.

### Common workflow:
1. ...

## 🔧 Known tools

The following tools are commonly used with GIZ files:
- [TTGames Explorer Rebirth](../tools/ttgamesexplorerrebirth.md)

## ⚠️ Notes & limitations

- GIZ is a proprietary format
- The internal structure is not fully documented for all games
- Some variations may exist between different games or engine versions

## 🧩 Structure

The structure may vary between engine versions:

- [LEGO Star Wars: The Complete Saga GIZ Structure](#tcs-giz-structure)

### TCS GIZ Structure

*Type Legend*

| Type       | Description              |
|------------|--------------------------|
| `int`      | 32-bit signed integer    |
| `float`    | 32-bit float             |
| `str8`     | 8-bit length-prefixed string  |
| `str16`    | 16-bit length-prefixed string |
| `str32`    | 32-bit length-prefixed string |
| `🔒strn`    | Fixed-length string (n = byte length) |
| `short`    | 16-bit signed integer    |
| `ushort`   | 16-bit unsigned integer  |
| `byte`     | 8-bit unsigned integer   |
| `bool`     | Boolean                  |
| `vec3`     | 3-component float vector |
| `enum`     | Enumerated value         |
| `array`    | Array of objects         |
| `_[]`  | Array of _          |
| `?`        | Special/Other type       |

---

*Overall*

```
/
├── [int]    Magic               — Always 1 (0x01 00 00 00).
├── [array]  Sections            — Section types listed below.
│       ├── [str32]  Section Name
│       └── [int]    Section Length  — Length of the section in bytes.
└── [int]    End of File         — Always 0 (0x00 00 00 00).
```

---

*Special Objects*

Special objects are used in multiple gizmo sections and are loaded through the same function.
Linking to special objects or other parts can be done without the special objects loading function,
but the function is usually used when linking to multiple special objects.

Throughout the rest of the gizmo section documentation, the special object loading will be written
out completely for each section despite the repetition.

```
/
├── [byte]   Special Object Version
├── [byte]   Special Object Count
└── [array]  Special Objects
        ├── [str8]   Special Object Name
        ├── [float]  Unknown
        ├── [float]  Animation Time
        ├── [int]    Unknown              (Special Object Version >= 2)
        └── [?]      Additional Loading  — When loading special objects, code for loading additional
                                           data can be passed and thus for some special objects
                                           loading there may be an extra property.
```

---

*GizObstacle Section*

GizObstacles are primarily invisible triggers of sorts. For example, in 1-2 when you jump on top
of the stone pillars, you enter a GizObstacle trigger that causes the pillar to fall.

```
/
├── [byte]   Version              — This is always at least 10 in Vanilla.
├── [short]  GizObstacle Count
└── [array]  GizObstacles
        ├── [🔒str16]  Name
        ├── [vec3]   Position
        ├── [vec3]   Unknown              (Version >= 2)
        ├── [float]  Unknown
        ├── [float]  Unknown
        ├── [vec3]   Unknown              (Version >= 3)
        ├── [short]  Unknown              (Version >= 3)
        ├── [int]    Unknown
        ├── [int]    Unknown              (Version >= 12)
        ├── [short]  Unknown              (Version == 6)
        ├── [byte]   Unknown              (Version == 6)
        ├── [byte]   Unknown
        ├── [byte]   Unknown
        ├── [byte]   Unknown              (Version >= 7)
        ├── [byte]   Special Object Version
        ├── [byte]   Special Object Count
        ├── [array]  Special Objects
        │       ├── [str8]   Special Object Name
        │       ├── [float]  Unknown
        │       ├── [float]  Animation Time
        │       ├── [int]    Unknown      (Special Object Version >= 2)
        │       └── [short]  Unknown      (Version >= 8)
        ├── [float]  Unknown              (Version >= 4)
        ├── [float]  Unknown              (Version >= 5)
        ├── [float]  Unknown              (Version >= 8)
        ├── [short]  Unknown              (Version == 9)
        ├── [str8]   Unknown              (Version >= 10)
        ├── [short]  Unknown              (Version >= 9)
        ├── [short]  Unknown              (Version >= 9)
        ├── [short]  Unknown              (Version >= 9)
        ├── [vec3]   Unknown              (Version >= 9)
        ├── [float]  Unknown              (Version >= 11)
        ├── [str8]   Unknown              (Version >= 13)
        └── [str8]   Unknown              (Version >= 14)
```

---

*GizBuildit Section*

GizBuildit is the buildable attribute applied to special objects.

```
/
├── [byte]   Version
├── [short]  Buildit Count
└── [array]  Buildits
        ├── [🔒str16]  Name
        ├── [vec3]   Position
        ├── [byte]   Special Object Version
        ├── [byte]   Special Object Count
        ├── [array]  Special Objects
        │       ├── [str8]   Special Object Name
        │       ├── [float]  Unknown 1
        │       ├── [float]  Animation Time
        │       └── [int]    Unknown 2            (Special Object Version >= 2)
        ├── [float]  Jump Intensity
        ├── [float]  Unknown 1                    (Version <= 6)
        ├── [ushort] Minimum Studs Value?
        ├── [ushort] Maximum Studs Value?         — Or random variance?
        ├── [byte]   Unknown 2
        ├── [byte]   Unknown 3
        ├── [float]  Unknown 4                    (Version >= 6)
        ├── [short]  Unknown 5                    (Version == 7)
        ├── [str8]   Unknown 6                    (Version >= 8)
        ├── [short]  Studs Pitch                  (Version >= 7)
        ├── [short]  Studs Yaw                    (Version >= 7)
        ├── [vec3]   Studs Spawn Position          (Version >= 7)
        ├── [float]  Studs Speed                  (Version >= 9)
        ├── [short]  Unknown 7                    (Version >= 4)
        ├── [short]  Unknown 8                    (Version >= 5)
        └── [str8]   Unknown 9                    (Version >= 5)
```

---

*GizForce Section*

GizForce is the forceable attribute applied to special objects.

```
/
├── [byte]   Version              — This is always at least 8 in Vanilla, but mostly 16.
├── [short]  Force Count
└── [array]  Forces
        ├── [🔒str16]  Name
        ├── [vec3]   Position
        ├── [vec3]   Unknown              (Version == 1)
        ├── [float]  Reset Time
        ├── [float]  Shake Time           (Version >= 8)
        ├── [float]  Range
        ├── [vec3]   Unknown              (Version == 1)
        ├── [short]  Unknown              (Version == 1)
        ├── [int]    Interaction Options  — Needs further research/experimentation.
        │       ├── Dark Side
        │       └── Reset
        ├── [bool]   Togglable
        ├── [byte]   Unknown              (Version >= 11)
        ├── [byte]   Unknown
        ├── [byte]   Unknown              (Version == 1)
        ├── [byte]   Special Object Version
        ├── [byte]   Special Object Count
        ├── [array]  Special Objects
        │       ├── [str8]   Special Object Name
        │       ├── [float]  Unknown
        │       ├── [float]  Animation Time
        │       ├── [int]    Unknown      (Special Object Version >= 2)
        │       └── [short]  Unknown      (Version >= 9)
        ├── [float]  Force Speed
        ├── [float]  Reset Speed
        ├── [float]  Auto Force?          (Version >= 6)
        ├── [float]  Effect Scale         (Version >= 7)
        ├── [float]  Unknown              (Version >= 3)  — Related to animation?
        ├── [short]  Unknown              (Version == 4)
        ├── [str8]   blowup               (Version >= 5)
        ├── [ushort] Minimum Studs Value? (Version >= 4)
        ├── [ushort] Maximum Studs Value? (Version >= 4)
        ├── [short]  Studs Angle          (Version >= 4)
        ├── [vec3]   Studs Position       (Version >= 4)
        ├── [float]  Studs Speed          (Version >= 10)
        ├── [str8]   Process Sound        (Version >= 15)
        ├── [str8]   Complete Sound       (Version >= 15)
        └── [str8]   Reset Sound          (Version >= 15)
```

---

*blowup Section*

```
/
├── [int]    Version                      — This is always at least 21 in Vanilla.
├── [int]    blowup (Effect) Count        (Version >= 2)
├── [int]    blowup (Property) Count
├── [array]  blowups (Effects)            (Version >= 2)
│       ├── [str8]   Special Object?
│       ├── [str8]   Name?
│       ├── [str8]   .par Reference?      (Version >= 17)
│       ├── [str8]   .par Reference?      (Version >= 17)
│       ├── [str8]   .ptl Reference?      (Version >= 4)
│       ├── [str8]   .ptl Reference?      (Version >= 4)
│       ├── [str8]   .ptl Reference?      (Version >= 4)
│       ├── [str8]   _ Reference          (Version >= 26)
│       ├── [str8]   _ Reference          (Version >= 26)
│       ├── [str8]   _ Reference          (Version >= 27)
│       ├── [str8]   _ Reference          (Version >= 27)
│       ├── [int]    Unknown
│       ├── [int]    Unknown              (Version >= 7)  — Potentially stud related.
│       ├── [byte]   Unknown              (Version >= 7)
│       ├── [float]  Unknown              (Version >= 8)
│       ├── [str8]   Blowup Decal         (Version >= 9)
│       ├── [float]  Unknown              (Version >= 14)
│       ├── [float]  Unknown              (Version >= 14)
│       ├── [byte]   Unknown              (Version >= 15)
│       ├── [byte]   Unknown              (Version >= 15)
│       ├── [bool]   Next Data?           (Version >= 16)
│       ├── [vec3]   Unknown              (Next Data != 0)
│       ├── [float]  Unknown              (Next Data != 0)
│       ├── [float]  Unknown              (Next Data != 0)
│       ├── [float]  Unknown              (Next Data != 0)
│       ├── [float]  Unknown              (Next Data != 0)
│       ├── [float]  Unknown              (Next Data != 0)
│       ├── [short]  Unknown              (Next Data != 0)
│       ├── [byte]   Unknown              (Next Data != 0)
│       ├── [byte]   Unknown              (Next Data != 0)
│       ├── [str8]   Blouwp Emit Object   (Version >= 18)
│       ├── [str8]   Blouwp Emit Object   (Version >= 22)
│       ├── [str8]   Blouwp Emit Object   (Version >= 22)
│       ├── [str8]   Blouwp Emit Object   (Version >= 22)
│       ├── [byte]   Unknown              (Version >= 18)
│       ├── [float]  Unknown              (Version >= 18)
│       ├── [float]  Unknown              (Version >= 18)
│       ├── [str8]   Blowup Shadow        (Version >= 19)
│       ├── [str8]   Blowup Swap          (Version >= 20)
│       ├── [float]  Unknown              (Version >= 23)
│       └── [float]  Unknown              (Version >= 24)
└── [array]  blowups (Properties)
        ├── [str8]   blowup (Effect)?
        ├── [str8]   Name?                (Version >= 2)
        ├── [vec3]   Position
        ├── [short]  Unknown
        ├── [short]  Unknown
        ├── [short]  Unknown
        ├── [short]  Unknown 1a           (Version >= 2 && Version <= 19)
        ├── [int]    Unknown 1a           (Version >= 20)
        ├── [int]    Unknown 1b           (Version == 28)
        ├── [int]    Unknown              (Version >= 30)
        ├── [int]    Unknown              (Version >= 2)
        ├── [byte]   Unknown              (Version >= 2)
        ├── [byte]   Unknown              (Version >= 2)
        ├── [byte]   Unknown              (Version >= 4)
        ├── [float]  Unknown              (Version >= 6)
        ├── [float]  Unknown              (Version >= 8)
        ├── [float]  Unknown              (Version >= 8)
        ├── [short]  Unknown              (Version >= 9)
        ├── [short]  Unknown              (Version >= 9)
        ├── [short]  Unknown              (Version >= 9)
        ├── [float]  Unknown              (Version >= 9)
        ├── [float]  Unknown              (Version >= 9)
        ├── [float]  Unknown              (Version >= 9)
        ├── [float]  Unknown              (Version >= 10)
        ├── [float]  Unknown              (Version >= 11)
        ├── [float]  Unknown              (Version >= 11)
        ├── [float]  Unknown              (Version >= 11)
        ├── [byte]   Unknown              (Version >= 12)
        ├── [short]  Unknown              (Version >= 13)
        ├── [short]  Unknown              (Version >= 13)
        ├── [short]  Unknown              (Version >= 19)
        ├── [short]  Unknown              (Version >= 19)
        ├── [short]  Unknown              (Version >= 19)
        ├── [float]  Unknown              (Version >= 19)
        ├── [float]  Unknown              (Version >= 19)
        ├── [float]  Unknown              (Version >= 19)
        ├── [float]  Unknown              (Version >= 19)
        ├── [float]  Unknown              (Version >= 21)
        ├── [float]  Unknown              (Version >= 23)
        └── [float]  Unknown              (Version >= 31)
```

---

*GizmoPickup Section*

```
/
├── [int]    Version
├── [int]    Pickup Count          — Length of the Pickups array.
├── [int]    Pickup Version?       (Version >= 3)  — Not entirely understood.
├── [float]  Draw Distance         (Version >= 5)  — Distance from camera pickups must be in to load.
├── [float]  Scale                 (Version >= 5)  — Scale of the pickups. Applies consistently
│                                                    through the whole area despite being per-file.
└── [array]  Pickups
        ├── [🔒str8]   Pickup Name
        ├── [vec3]   Pickup Position
        ├── [enum]   Pickup Type
        │       ├── default,s  — Silver Stud
        │       ├── g          — Gold Stud
        │       ├── b          — Blue Stud
        │       ├── p          — Purple Stud
        │       ├── m          — Minikit
        │       ├── u          — Powerup
        │       ├── h          — Heart
        │       ├── r          — Red Brick
        │       ├── c          — Challenge Minikit
        │       └── t          — Torpedo
        ├── [enum]   Spawn Type    (Version >= 2)  — Not entirely researched/experimented with.
        │       ├── default,0  — Normal
        │       ├── 2          — Triggered
        │       └── 6          — Auto-Collect
        └── [byte]   Spawn Group   (Version >= 4)  — Pickups of the same spawn group all spawn when
                                                     one is triggered. Never utilized in Vanilla.
```

---

*Lever Section*

```
/
├── [int]    Version               — This is always 6 in Vanilla.
├── [int]    Lever Count
└── [array]  Levers
        ├── [🔒str16]  Name
        ├── [vec3]   Position
        ├── [short]  Angle
        ├── [enum]   Handle Color
        │       ├── default  — None
        │       ├── r        — Red
        │       ├── o        — Orange
        │       ├── y        — Yellow
        │       ├── l        — Lime
        │       ├── g        — Green
        │       ├── u        — Light Blue
        │       ├── b        — Blue
        │       ├── p        — Purple
        │       └── w        — Brown
        ├── [bool]   Multiple Pulls    (Version >= 2)
        ├── [float]  Pull Time         (Version >= 3)
        ├── [bool]   Invisible         (Version >= 4)
        ├── [vec3]   Target Position   (Version >= 5)
        ├── [float]  Target Size       (Version >= 5)
        └── [bool]   Target Invisible  (Version >= 6)
```

---

*Spinner Section*

Spinner is the green and red gizmo that you push to spin.

```
/
├── [int]    Version               — This is essentially always 9 in Vanilla.
├── [int]    Spinner Count
└── [array]  Spinners
        ├── [str8]   Name
        ├── [vec3]   Position
        ├── [short]  Angle
        ├── [str8]   Spinner Special Object
        ├── [byte]   Unknown Count?
        ├── [byte]   Flap Count            (Version >= 2)
        ├── [int]    Unknown               (Flap Count != 0 && Version >= 3)
        ├── [float]  Unknown               (Flap Count != 0 && Version >= 3)
        ├── [float]  Unknown 1             (Flap Count != 0 && Version >= 4)
        ├── [byte]   Unknown               (Unknown 1 != 0 && Version >= 6)
        ├── *Format for Version <= 4 excluded here
        ├── [byte]   Special Object Version
        ├── [byte]   Special Object Count
        ├── [array]  Special Objects
        │       ├── [str8]   Special Object Name
        │       ├── [float]  Unknown 1
        │       ├── [float]  Animation Time
        │       └── [int]    Unknown 2     (Special Object Version >= 2)
        ├── *Format for Version <= 6 excluded here
        ├── [float[]] Unknown              (Version >= 7)  — Length of Unknown Count.
        ├── [float]  Unknown               (Version >= 8)
        └── [float]  Unknown               (Version >= 8)
```

---

*MiniCut Section*

MiniCuts are short cutscenes that occur in the middle of levels.

```
/
├── [int]    Version               — This is always 1 in Vanilla. Changing this value in TCS does nothing.
├── [int]    MiniCut Count
└── [array]  MiniCuts
        ├── [str8]   Name
        ├── [float]  Unknown
        ├── [float]  Unknown
        ├── [float]  Unknown
        ├── [float]  Unknown
        ├── [float]  Unknown
        ├── [byte]   MiniCuts Parts Count
        └── [array]  MiniCuts Parts
                ├── [str8]   MiniCuts Part Name
                ├── [float]  Unknown
                ├── [float]  Unknown
                ├── [float]  Unknown
                ├── [float]  Unknown
                ├── [short]  Unknown
                ├── [short]  Unknown
                ├── [short]  Unknown
                ├── [float]  Unknown
                └── [float]  Unknown
```

---

*Tube Section*

Tubes are the areas that blow/fan/float your character upwards. They are also used in the podsprint level.

```
/
├── [int]    Version               — This is always 2 in Vanilla.
├── [int]    Tube Count
└── [array]  Tubes
        ├── [🔒str16]  Name
        ├── [vec3]   Position      — This is at the bottom of the tube.
        ├── [float]  Height
        ├── [float]  Radius
        ├── [bool]   Magnetic      (Version >= 2)
        └── [str8]   Special Object (Version >= 3)  — Not present in TCS.
```

---

*ZipUp Section*

ZipUps are the red targets and grapples that blaster characters can swing and zip between.

```
/
├── [int]    Version               — This is always at least 2 in Vanilla, but mostly 4.
├── [int]    ZipUp Count
└── [array]  ZipUps
        ├── [🔒str16]  Name
        ├── [vec3]   Start
        ├── [vec3]   Axis
        ├── [vec3]   End
        ├── [short]  Unknown 1
        ├── [short]  Unknown 2
        ├── [bool]   Swing
        ├── [bool]   Unknown 3
        ├── [bool]   Two Way
        ├── [bool]   Invisible         (Version >= 2)
        ├── [bool]   Unknown 4         (Version >= 3)
        └── [bool]   Target(s) Invisible? (Version >= 4)
```

---

*GizTurret Section*

GizTurrets are the turrets that don't move but shoot at the player, such as in vehicle levels or on Kamino.

```
/
├── [byte]   Version
├── [short]  GizTurret Count
└── [array]  GizTurrets
        ├── [🔒str16]  Name
        ├── [byte]   Special Object Version
        ├── [byte]   Special Object Count
        ├── [array]  Special Objects
        │       ├── [str8]   Special Object Name
        │       ├── [float]  Unknown
        │       ├── [float]  Animation Time
        │       ├── [int]    Unknown      (Special Object Version >= 2)
        │       └── [short]  Unknown      (Version >= 3)  — TCS loading code for this is a bit odd.
        ├── [vec3]   Unknown
        ├── [vec3]   Unknown
        ├── [vec3]   Unknown
        ├── [vec3]   Unknown
        ├── [int]    Unknown
        ├── [int]    Unknown
        ├── [int]    Unknown
        ├── [int]    Unknown
        ├── [int]    Unknown
        ├── [int]    Unknown
        ├── [int]    Unknown              (Version >= 2)
        ├── [byte]   Unknown Count
        ├── [vec3[]] Unknown              — Length of Unknown Count.
        ├── [float]  Unknown
        ├── [float]  Unknown
        ├── [float]  Unknown              — This is always 0 in Vanilla.
        ├── [float]  Unknown
        ├── [float]  Unknown
        ├── [float]  Unknown
        ├── [short]  Unknown
        ├── [short]  Unknown
        ├── [short]  Unknown
        ├── [vec3]   Unknown
        ├── [float]  Unknown              (Version >= 6)
        ├── [byte]   Unknown
        ├── [byte]   Unknown              (Version >= 4)
        ├── [short]  Unknown              (Version >= 4)
        ├── [str8]   Blaster Material?
        ├── [str8]   Part?
        ├── [str8]   Part?
        ├── [str8]   Part?                (Version >= 7)
        ├── [str8]   Blowup?
        └── [short]  Unknown
```

---

*BombGenerator Section*

BombGenerators are the generators that spawn bombs for the player in vehicle levels.

```
/
├── [byte]   Version               — This is always 1 in Vanilla.
├── [short]  BombGenerator Count
└── [array]  BombGenerators
        ├── [🔒str16]  Name
        ├── [vec3]   Position
        ├── [int]    Unknown
        ├── [byte]   Special Object Version
        ├── [byte]   Special Object Count
        └── [array]  Special Objects
                ├── [str8]   Special Object Name
                ├── [float]  Unknown
                ├── [float]  Animation Time?
                └── [int]    Unknown      (Special Object Version >= 2)
```

---

*Panel Section*

```
/
├── [int]    Version               — This is always at least 5 in Vanilla, but mostly 8.
├── [int]    Panel Count
└── [array]  Panels
        ├── [str32]  Name
        ├── [vec3]   Position
        ├── [short]  Angle
        ├── [enum]   Type
        │       ├── default,0  — Astromech Droid
        │       ├── 1          — Protocol Droid
        │       ├── 2          — Bounty Hunter
        │       └── 3          — Stormtrooper
        ├── [bool]   Invisible             (Version >= 3)
        ├── [vec3]   Target Offset         (Version >= 4)
        ├── [float]  Target Size           (Version >= 4)
        ├── [bool]   Target Invisible      (Version >= 5)
        ├── [bool]   Alternative Face      (Version >= 6)  — Only applies to Astromech and Protocol Droid types.
        ├── [bool]   Alternative Body      (Version >= 6)  — Only applies to Astromech and Protocol Droid types.
        │                                                    Protocol Droid uses the same alternative body as
        │                                                    Astromech, and thus looks incorrect.
        ├── [bool]   Unknown 2             (Version >= 7)
        └── [bool]   Unknown 3             (Version >= 8)  — Almost always false, except for panel3
                                                             in deathstarrescue_a.
```

---

*HatMachine Section*

HatMachines are the machines that give your character a hat when the lever is pulled.

```
/
├── [int]    Version               — This is always 5 in Vanilla.
├── [int]    HatMachine Count
└── [array]  HatMachines
        ├── [str32]  Name
        ├── [vec3]   Position
        ├── [short]  Angle
        ├── [enum]   Type
        │       ├── 0          — Random
        │       ├── 1          — Leia
        │       ├── 2          — Fedora
        │       ├── 3          — Top Hat
        │       ├── 4          — Baseball Cap
        │       ├── default,5  — Stormtrooper
        │       ├── 6          — Bounty Hunter
        │       └── 7          — Droid Panel
        ├── [enum]   Lever Handle Color    (Version >= 3)
        │       ├── default  — None
        │       ├── r        — Red
        │       ├── o        — Orange
        │       ├── y        — Yellow
        │       ├── l        — Lime
        │       ├── g        — Green
        │       ├── u        — Light Blue
        │       ├── b        — Blue
        │       ├── p        — Purple
        │       └── w        — Brown
        ├── [vec3]   Target Position       (Version >= 4)
        ├── [float]  Target Size           (Version >= 4)
        └── [bool]   Target Invisible      (Version >= 5)
```

---

*PushBlocks Section*

PushBlocks are the blocks that can be pushed and slid across the tiled floors.
Some unknown values may be related to allowing the PushBlock to be pushed after being pushed to a target location.

```
/
├── [int]    Version
├── [int]    PushBlocks Count
└── [array]  PushBlocks
        ├── [str8]   Name                  — This (likely) links to a special object.
        ├── [float]  Snap Range
        ├── [bool]   Push Location?        — Whether this is where you are meant to push an object to/on.
        ├── [bool]   Unknown 1             — This is always 0 in Vanilla.
        ├── [bool]   Lock Z                — Prevents the PushBlock from being pushed on the Z axis.
        ├── [bool]   Lock X                — Prevents the PushBlock from being pushed on the X axis.
        ├── [bool]   Unknown 2             (Version >= 4)
        ├── [bool]   Unknown 3             (Version >= 4)
        ├── [bool]   Unknown 4             (Version >= 5)  — This is always 0 in Vanilla.
        ├── [bool]   No Slipperiness       (Version >= 5)  — Prevents the PushBlock from slipping entirely.
        ├── [byte]   PushBlock Link Object Count (Version >= 3)
        └── [str8[]] PushBlock Link Objects (Version >= 3)  — These may be special objects.
```

---

*Torp Machine Section*

Torp Machines are the machines that you collect torpedoes from by flying over in vehicle levels.

```
/
├── [int]    Version               — This is essentially always 3 in Vanilla.
├── [int]    Torp Machine Count
├── [float]  Scale                 (Version >= 3)
└── [array]  Torp Machines
        ├── [str32]  Name
        ├── [vec3]   Position
        ├── [short]  Angle
        └── [byte]   Red Outline   (Version >= 2)  — Normal black color when 0, red color otherwise.
```

---

*ShadowEditor Section*

Unknown.

```
/
├── [byte]   Version
├── [byte]   ShadowEdit Count
└── [array]  ShadowEdits
        ├── [vec3]   Position?
        ├── [float]  Unknown
        ├── [float]  Unknown              (Version >= 2)
        ├── [float]  Unknown              (Version >= 2)
        ├── [float]  Unknown              (Version >= 3)
        ├── [float]  Unknown              (Version >= 3)
        ├── [float]  Unknown              (Version >= 4)
        ├── [float]  Unknown              (Version >= 5)  — This is always 0 in Vanilla.
        ├── [float]  Unknown              (Version >= 5)  — This is always 0 in Vanilla.
        ├── [float]  Unknown              (Version >= 6)
        ├── [float]  Unknown              (Version >= 6)
        ├── [float]  Unknown              (Version >= 6)
        ├── [float]  Unknown              (Version >= 7)
        └── [int]    Unknown              (Version >= 8)  — This is always 0, 1, or 2 in Vanilla.
```
