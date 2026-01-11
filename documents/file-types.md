# File Types and Data Structures

This catalog summarizes file types present in `package/` and the observable structure of text-like formats.
Binary formats are noted but not reverse-engineered here.

## Text-like formats (observable structure)
These files contain comments or INI-style sections and appear to drive gameplay data.

### `.STC` (structure/city/road definitions)
Text format with comment headers listing fields such as:
- Name, Hit points, Cost, Size, Picture ID
- Build constraints (e.g., where it can be built)
- Production and storage types
- Resource production/consumption
- Category identifiers (HQ, FACTORY, ENERGY, LAB, etc.)

Observed in `STRUCTS/HUMAN.STC`, `STRUCTS/ALIEN.STC`, and `ROADS/ROAD.STC`.

### `.SST` (structure definitions variant)
Text format similar to `.STC`, with the same field list in comments, including category and embedded unit references.
Observed in `STRUCTS/HUMAN.SST`, `STRUCTS/ALIEN.SST`.

### `.SUT` (unit templates)
INI-like sections with headers such as `[DropShip]`, and key/value entries like `PictureID`, `LightWeapon`, `Movement`, and `Cost`.
Comment headers describe fields for unit type name, movement type, production type, initiative, hit points, upkeep, and category.
Observed in `UNITS/HUMAN.SUT`, `UNITS/ALIEN.SUT`.

### `.UNT` (unit templates variant)
INI-like sections with `PictureID`, weapon references, movement, production, action points, armor, and other metadata.
Comment headers note fields like category, move sound, embedded flags, and encyclopedia image.
Observed in `UNITS/HUMAN.UNT`, `UNITS/ALIEN.UNT`.

### `.CM` (city/colony maps)
INI-style configuration with labeled sections such as `[Tech]` and `[Landing]`.
Keys describe tech levels and positions (e.g., `EnergyLevel`, `DamageLevel`, `1=08,09`).
Observed in `CITIES/DEMO001.CM` (and similar).

### `.DAT` (AI configuration)
INI-style configuration for AI behavior, including sections like `[Attack]` and `[Orbital]` with tunable timing parameters.
Observed in `AI/AICONFIG.DAT`.

### `.FDS` (AI dropship templates)
Structured with comments and descriptions of attack templates and difficulty-specific rules.
Observed in `AI/ALIEN.FDS`.

### `.DES` (animation descriptor)
INI-style with sections like `[LIGHTDAMAGE]` describing animation frames, speed, base filename, image size, and optional sound.
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

## Extension inventory summary
Extensions present in the demo include: `.ANM`, `.AVI`, `.BMP`, `.CM`, `.CMP`, `.CNT`, `.COL`, `.DAT`, `.DES`, `.DLL`, `.EXE`, `.EX_`, `.FDS`, `.HLP`, `.ICA`, `.INI`, `.INS`, `.LIB`, `.LST`, `.MD`, `.PAM`, `.PKG`, `.RTF`, `.SHT`, `.SST`, `.STC`, `.STI`, `.SUT`, `.TAB`, `.TXT`, `.UNT`, `.WAV`.
