# File Types and Data Structures

This catalog summarizes file types present in `package/` and the observable structure of text-like formats.
Binary formats are noted but not reverse-engineered here.

## Format overview
| Extension | Seen in | Purpose (observed) |
| --- | --- | --- |
| `.STC` | `STRUCTS/`, `ROADS/` | Structure and road definitions (text-like). |
| `.SST` | `STRUCTS/` | Structure definitions variant (text-like). |
| `.SUT` | `UNITS/` | Unit templates and weapons (text-like). |
| `.UNT` | `UNITS/` | Unit templates and weapons variant (text-like). |
| `.CM` | `CITIES/` | City/colony map layouts (text-like). |
| `.DAT` | `AI/` | AI configuration (text-like). |
| `.FDS` | `AI/` | AI dropship templates (text-like). |
| `.DES` | `ANMS/` | Animation descriptors (text-like). |
| `.LST` | `TERRAINS/` | Terrain list (text-like). |
| `.RTF` | `RTF/`, `INTF/` | In-game encyclopedia/help entries. |
| `.STI`, `.ICA`, `.ANM`, `.SHT`, `.PAM`, `.CMP`, `.COL` | multiple | Custom binary assets (not decoded). |

## Text-like formats (observable structure)
These files contain comments or INI-style sections and appear to drive gameplay data.

### `.STC` (structure/city/road definitions)
Text format with comment headers listing fields, followed by INI-style sections. Fields observed in `STRUCTS/HUMAN.STC`:
- `Hp`, `Cost`, `SizeX`, `SizeY`, `PictureID`
- `IsStarship`, `BuiltWhere`, `ProductionType`, `StorageType`
- `ProductionCash`, `ProductionResearch`, `ProductionEnergy`
- `ConsummationCash`, `ConsummationEnergy`, `StorageSize`
- `StructureCategory`, `EmbeddedUnitType`
- `EncyclopediaImg`, `EncyclopediaTxt`
- Optional gatekeeper flags like `CanBuild`

`BuiltWhere` uses explicit string tokens (`NOWHERE`, `B-ROAD`, `B-WALL`, `ANYWHERE`), and `ProductionType`/`StorageType` may include multiple tokens separated by spaces.

Observed in `STRUCTS/HUMAN.STC`, `STRUCTS/ALIEN.STC`, and `ROADS/ROAD.STC`.

### `.SST` (structure definitions variant)
Text format similar to `.STC`, with the same field list in comments, including category and embedded unit references.
Additional observed field:
- `UnitCanEnter` (e.g., in `STRUCTS/HUMAN.SST` for dropships)

Observed in `STRUCTS/HUMAN.SST`, `STRUCTS/ALIEN.SST`.

### `.SUT` (unit templates)
INI-like sections with headers such as `[DropShip]`, and key/value entries like `PictureID`, `LightWeapon`, `HeavyWeapon`, `Movement`, and `Cost`.
Comment headers describe fields for unit type name, movement type, production type, initiative, hit points, upkeep, and category.

Observed fields in `UNITS/HUMAN.SUT`:
- Core unit properties: `PictureID`, `Movement`, `Cost`, `ProductionType`, `TimeUnits`, `Initiative`, `Hp`, `Upkeep`
- Weapons: `LightWeapon`, `HeavyWeapon` (referencing weapon sections, or `NO WEAPON`)
- Metadata: `UnitCategory`, `MoveSound`, `Destructionanimation`

### `.SUT` weapon definitions
The same file contains weapon sections like `[WEAPON_MISWARHEAD]`, with fields such as:
- `Name`, `Type`, `Display`, `Turreted`, `Range`, `Precision`
- `DamageContact`, `DamageClose`, `DamageFar`, `PercentTimeUnits`

Observed in `UNITS/HUMAN.SUT`, `UNITS/ALIEN.SUT`.

### `.UNT` (unit templates variant)
INI-like sections with `PictureID`, weapon references, movement, production, action points, armor, and other metadata.
Comment headers note fields like category, move sound, embedded flags, and encyclopedia image.

Observed fields in `UNITS/HUMAN.UNT`:
- Core unit properties: `PictureID`, `Movement`, `Cost`, `ProductionType`, `TimeUnits`, `Initiative`, `Hp`, `Upkeep`
- Weapons: `LightWeapon`, `HeavyWeapon` (referencing weapon sections, or `NO WEAPON`)
- Metadata: `UnitCategory`, `MoveSound`, `Embedded`, `AcquireExperience`
- Encyclopedia references: `EncyclopediaImg`, `EncyclopediaTxt`
- Destruction animation: `DestructionAnimation`

### `.UNT` weapon definitions
Weapon sections mirror the `.SUT` fields, including `Name`, `Type`, `Display`, `Turreted`, `Range`, `Precision`, and damage fields.

Observed in `UNITS/HUMAN.UNT`, `UNITS/ALIEN.UNT`.

### `.CM` (city/colony maps)
INI-style configuration with labeled sections such as `[Tech]`, `[Landing]`, and territory-specific blocks.

Observed sections in `CITIES/DEMO001.CM`:
- `[Tech]`: `EnergyLevel`, `ResistanceLevel`, `DamageLevel`, `SpeedLevel`, `RateOfireLevel`, `RocketryLevel`
- `[Landing]`: numbered entries in `index=x,y` format (e.g., `1=08,09`)
- `[Neutral_Cash]`: `Structure=1`, `Unit=1`
- `[Neutral_City]`: numbered entries in `index=x,y,Type` format (e.g., `1=05,25,Road`, `152=04,23,Wall`)

The comments indicate some province ownership logic is embedded in these sections; the fields above are present in the demo map.

### `.DAT` (AI configuration)
INI-style configuration for AI behavior, including sections like `[Attack]` and `[Orbital]` with tunable timing parameters.

Observed sections and fields in `AI/AICONFIG.DAT`:
- `[Attack]`: `AvgTurnNeighbourAttackEasy`, `AvgTurnNeighbourAttackNormal`, `AvgTurnNeighbourAttackHard`, `AvgTurnRandomEffect`
- `[Orbital]`: `AvgTurnOrbitalAttackEasy/Normal/Hard`, `MinProvincesOrbitalEasy/Normal/Hard`
- `[QtyDShips]`: `ProximityClose`, `ProximityFar`, `TimeMiddleGame`, `TimeFinishGame`
- `[DShipContent]`: `YearDShipStep2`, `YearDShipStep3`, `YearDShipStep4`, `NumberOfTemplatePerStep`
- `[Nuke]`: `AvgTurnNukeEasy/Normal/Hard`, `PercentNukeBeforeAttackEasy/Normal/Hard`
- `[CityDevelopment]`: `UnitCashEasy/Normal/Hard`, `StructureCashEasy/Normal/Hard`
- `[AITech]`: `ResearchEasy/Normal/Hard`
- `[TechHuman]`, `[TechAlien]`: `EnergyPercent`, `ResistancePercent`, `DamagePercent`, `SpeedPercent`, `RateOfirePercent`, `RocketryPercent`
- `[TechStartLevel]`: `EnergyLevel`, `ResistanceLevel`, `DamageLevel`, `SpeedLevel`, `RateOfireLevel`, `RocketryLevel`
- `[PlayerCash]`: `Easy`, `Normal`, `Hard`

The file includes French developer comments with semicolon-prefixed lines.

### `.FDS` (AI dropship templates)
Structured with comments and descriptions of attack templates and difficulty-specific rules.
Observed in `AI/ALIEN.FDS`.

### `.DES` (animation descriptor)
INI-style with sections like `[LIGHTDAMAGE]` describing animation frames, speed, base filename, image size, and optional sound.

Observed fields in `ANMS/ANIMS.DES`:
- `Frames`, `Speed`, `FileName`, `Size_Height`, `Size_Width`, `Sound`

The file comments describe filename expansion rules:
- Single-sequence animations: `FileName(xx).anm` where `xx` is zero-based with a leading zero.
- Directional animations: `FileName(xy).anm` where `x` is a facing index and `y` is the frame index.

Observed in `ANMS/ANIMS.DES`, `ANMS/SHOTS.DES`.

### `.LST` (terrain list)
Simple list-format text file; present as `TERRAINS/TERRAINS.LST`.

### `.INI` / `.INS` / `.PKG`
Installer and configuration metadata (root-level installer files, plus `WINDOWS/WAVEMIX.INI`).

### `.RTF`
Rich text files likely used by the in-game encyclopedia/help.
Observed in `RTF/` and `INTF/`.

## Binary asset formats (not yet decoded)
These file types appear to be binary assets or custom data formats. They are referenced by the executable but the internal structure is still unknown.

- **Images**: `.BMP` (standard Windows bitmaps), plus `.STI`, `.ICA` (custom image formats), `.SHT`/`.ANM` (animation frames).
- **Audio**: `.WAV` (standard PCM/RIFF, likely), referenced by the executable and located in `SOUNDS/`.
- **Video**: `.AVI` (intro video in `VIDEO/`).
- **Maps/terrain**: `.PAM`, `.CMP`, `.COL` (map/colony-related binary assets).

### Open questions for binary formats
- `.STI`/`.ICA`/`.SHT`/`.ANM` container headers, palette format, and compression scheme.
- `.PAM` map header structure and tile encoding.
- `.CMP`/`.COL` colony data layout and coordinate encoding.

## Extension inventory summary
Extensions present in the demo include: `.ANM`, `.AVI`, `.BMP`, `.CM`, `.CMP`, `.CNT`, `.COL`, `.DAT`, `.DES`, `.DLL`, `.EXE`, `.EX_`, `.FDS`, `.HLP`, `.ICA`, `.INI`, `.INS`, `.LIB`, `.LST`, `.MD`, `.PAM`, `.PKG`, `.RTF`, `.SHT`, `.SST`, `.STC`, `.STI`, `.SUT`, `.TAB`, `.TXT`, `.UNT`, `.WAV`.
