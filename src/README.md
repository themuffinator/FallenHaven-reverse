# Reverse Engineering Scaffolding

This directory contains the initial scaffolding for the Fallen Haven demo reverse-engineering effort.
The goal is to keep information derived from analysis in a structured, incremental format so we can
expand and refine it over time.

## Scope
- Target binary: `package/EXE/FHDEMO.EXE`
- Analysis tools used so far: `objdump` (static inspection only)

## Work breakdown
The reverse-engineering workload is large, so the initial effort is broken into smaller, trackable
tasks:

1. **Binary entrypoint and section map**
   - Capture entrypoint address and basic PE section layout.
   - Update `src/fhdemo/README.md` and `src/fhdemo/maps/section-map.md`.
2. **Import/module inventory**
   - Record imported DLL names and leave room for per-function imports.
   - Update `src/fhdemo/maps/import-map.md`.
3. **Symbol map scaffolding**
   - Seed a symbol map with the entrypoint and placeholders for discovered routines.
   - Update `src/fhdemo/maps/symbol-map.md`.
4. **Structure map scaffolding**
   - Create a structure map template for future field/offset tracking.
   - Update `src/fhdemo/maps/structure-map.md`.

These files are intended to grow as deeper disassembly and runtime analysis are performed.
