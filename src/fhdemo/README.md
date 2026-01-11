# FHDEMO.EXE Reverse Engineering Notes

## Target
- Path: `package/EXE/FHDEMO.EXE`
- Format: 32-bit Windows PE (pei-i386)
- Entry point: `0x00465520`

## Current map coverage
- Section layout: `maps/section-map.md`
- Imports (DLLs): `maps/import-map.md`
- Symbol map scaffolding: `maps/symbol-map.md`
- Structure map scaffolding: `maps/structure-map.md`

## Next steps
- Confirm entrypoint behavior via disassembly (Ghidra or other suitable tools).
- Identify the startup routine(s) leading into game initialization.
- Expand symbol and structure maps as routines and data layouts are identified.
