# Game File Structure (package/)

## Scope
This document maps the on-disk layout of the demo's `package/` directory and summarizes file groupings.
No files in `package/` should be edited; treat them as reference-only assets.

## Top-level layout
The `package/` folder contains 20 subdirectories and 12 files at its root.
Key root-level files include installer assets (`SETUP.EXE`, `_SETUP.DLL`, `_ISDEL.EXE`, `_INST32I.EX_`), setup metadata (`SETUP.INI`, `SETUP.INS`, `SETUP.PKG`), and documentation (`README.TXT`).

### Root files
- `COLORS.TAB`
- `README.TXT`
- `README.md`
- `SETUP.EXE`
- `SETUP.INI`
- `SETUP.INS`
- `SETUP.PKG`
- `SETUP.BMP`
- `_SETUP.DLL`
- `_SETUP.LIB`
- `_INST32I.EX_`
- `_ISDEL.EXE`

### Directory inventory
| Directory | Files | Notes |
| --- | ---: | --- |
| `AI/` | 2 | AI tuning/configuration data (`AICONFIG.DAT`, `ALIEN.FDS`). |
| `ANMS/` | 34 | Animation definitions (`.DES`) and frame data (`.ANM`, `.SHT`). |
| `CITIES/` | 4 | City map/config files (`.CM`). |
| `COLONIES/` | 2 | Colony data (`.CMP`, `.COL`). |
| `EXE/` | 1 | Main game executable (`FHDEMO.EXE`). |
| `HELP/` | 2 | Help system (`FALLEN.HLP`, `FALLEN.CNT`). |
| `IMGS/` | 7 | Interface images (`.BMP`). |
| `INTF/` | 21 | Interface assets (`.BMP`, `.RTF`, `.STI`). |
| `MAPS/` | 4 | Map files (`.PAM`). |
| `ROADS/` | 2 | Road definitions (`.ICA`, `.STC`). |
| `RTF/` | 20 | Rich text help/encyclopedia entries (`.RTF`). |
| `SIMG/` | 4 | Sprite image sets (`.ICA`). |
| `SOUNDS/` | 43 | Audio assets (`.WAV`). |
| `STRUCTS/` | 4 | Structure definitions (`.STC`, `.SST`). |
| `TERRAINS/` | 1 | Terrain list (`TERRAINS.LST`). |
| `TIMG/` | 3 | Terrain images (`.STI`). |
| `UIMG/` | 4 | Unit images (`.ICA`). |
| `UNITS/` | 4 | Unit definitions (`.SUT`, `.UNT`). |
| `VIDEO/` | 1 | Intro video (`FALLEN.AVI`). |
| `WINDOWS/` | 4 | Installer/runtime support files; includes `WINDOWS/SYSTEM/` DLLs. |

## Extension inventory
The demo data includes 179 files. The most common extensions are `.WAV` (43), `.BMP` (29), `.RTF` (20), `.SHT` (18), `.ANM` (14), and `.ICA` (10).
Other extensions appear to be configuration, binary asset, or installer-related formats.

## Observed structure patterns
- The game separates **data definitions** (text-like config files such as `.SUT`, `.UNT`, `.STC`, `.SST`, `.CM`, `.DAT`, `.FDS`) from **binary assets** (images, sounds, animations).
- Subsystems are grouped by directory name: e.g., `UNITS/` for unit definitions, `STRUCTS/` for buildings, `SOUNDS/` for audio, `RTF/` for in-game text.
- The `WINDOWS/` folder appears to include required runtime DLLs for Windows 95-era systems; installer tooling is stored at the root and uses InstallShield components.

## Text-like format locations
These directories contain the configuration-style formats described in `documents/file-types.md`:
- `AI/`: `.DAT` (AI tuning) and `.FDS` (dropship templates).
- `ANMS/`: `.DES` animation descriptor files.
- `CITIES/`: `.CM` city/province layout data.
- `ROADS/`: `.STC` road definitions.
- `STRUCTS/`: `.STC` and `.SST` structure definitions.
- `TERRAINS/`: `.LST` terrain list.
- `UNITS/`: `.SUT` and `.UNT` unit templates and weapon definitions.
- `RTF/`, `INTF/`: `.RTF` encyclopedia/help text.
