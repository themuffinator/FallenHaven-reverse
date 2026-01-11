# Supporting Binary Analysis

## Install/Setup components
The demo includes several installer-related binaries at the root of `package/`:

- `SETUP.EXE`
- `_ISDEL.EXE`
- `_SETUP.DLL`
- `_SETUP.LIB`
- `_INST32I.EX_`

### Format identification (static)
- `SETUP.EXE`, `_ISDEL.EXE`, and `_SETUP.DLL` contain an MZ header with an **NE** signature at the New Executable offset, indicating 16-bit Windows New Executable format.
- `_INST32I.EX_` does **not** begin with an MZ signature; it appears to be a compressed or packed payload associated with InstallShield.

### String evidence
Static strings point to InstallShield tooling and resources:

- `HInstallShield Launcher SE v2.1 (C) Stirling Technologies, Inc. 1990-1995`
- `InstallShieldSetup30`
- `Setup Launcher ( SETUP.EXE)`
- `InstallSHIELD Delete`
- `InstallShield Deleter.`
- `DInstallSHIELD Resource DLL (c) Stirling Technologies Inc., 1990-1995`

### Role summary
These components appear to implement the Windows 95-era InstallShield installer and uninstaller workflow for the demo:

- `SETUP.EXE` is the launcher/driver.
- `_SETUP.DLL` supplies InstallShield UI resources and setup script support.
- `_ISDEL.EXE` acts as the uninstall/deletion helper.
- `_INST32I.EX_` is likely a compressed payload used by the installer.

Further analysis of these binaries would require NE-format parsing tools or unpacking the compressed payload.
