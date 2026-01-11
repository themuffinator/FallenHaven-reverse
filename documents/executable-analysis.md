# Main Executable Analysis: `package/EXE/FHDEMO.EXE`

## Header summary
Static inspection shows the executable is a 32-bit Windows PE file (MZ header, PE signature) targeting the 0x14c machine type (x86). The PE header indicates 6 sections with the following layout:

| Section | VA | Virtual Size | Raw Offset | Raw Size |
| --- | --- | --- | --- | --- |
| `.text` | 0x00001000 | 0x0006791e | 0x00000400 | 0x00067a00 |
| `.rdata` | 0x00069000 | 0x00012438 | 0x00067e00 | 0x00012600 |
| `.data` | 0x0007c000 | 0x00003bdb | 0x0007a400 | 0x00003200 |
| `.idata` | 0x00080000 | 0x00001b80 | 0x0007d600 | 0x00001c00 |
| `.rsrc` | 0x00082000 | 0x0008a978 | 0x0007f200 | 0x0008aa00 |
| `.reloc` | 0x0010d000 | 0x0000c4e4 | 0x00109c00 | 0x0000c600 |

## Imported modules (from embedded strings)
String inspection reveals references to the following Windows DLLs:

- `ADVAPI32.dll`
- `GDI32.dll`
- `KERNEL32.dll`
- `MFC42.DLL`
- `MSVCRT.dll`
- `MSVFW32.dll`
- `USER32.dll`
- `WINMM.dll`
- `WMIX32.dll`

These suggest usage of Win32 APIs, MFC runtime, multimedia (WINMM/MSVFW32), and a custom audio mixer (`WMIX32.dll`).

## Asset and data references (from embedded strings)
The executable includes literal references to many asset files and data types. Notable examples:

- Video: `FALLEN.AVI`
- Audio: `.WAV` entries (extension references)
- Images: `.BMP` entries (menu images, win/lose screens, etc.)
- Text/help: `.RTF` entries such as `AITURN.RTF`, `STRAT.RTF`, `VICNATT.RTF`
- Game data: `AICONFIG.DAT`, `ROAD.STC`, `TERRAINS.LST`, `.SUT`/`.UNT`/`.SST`/`.STC` references
- Animation assets: `.ANM`, `.SHT`
- Map files: `.PAM`
- Terrain tiles: `.STI`
- Sprite image collections: `.ICA`

The presence of file-type extensions in strings indicates the game loads these assets by name at runtime rather than relying solely on embedded resources.

## High-level mapping (static)
Given the imports and data references, the executable appears to orchestrate these subsystems:

- **Rendering/UI**: Image and UI bitmap references (`.BMP`), and `GDI32`/`USER32` usage.
- **Audio playback**: `.WAV` files, `WINMM.dll`, and `WMIX32.dll` strings.
- **Video playback**: `FALLEN.AVI` and `MSVFW32.dll` references.
- **Data-driven gameplay**: Numerous references to text-like `.SUT`, `.UNT`, `.STC`, `.SST`, `.CM`, `.DAT`, `.FDS` files indicate runtime parsing of definition files for units, structures, cities, and AI.
- **Help/encyclopedia**: `.RTF` references across tactical/strategic topics.

This mapping is based on static string inspection and the observed asset names; deeper behavior analysis would require disassembly or debugging.
