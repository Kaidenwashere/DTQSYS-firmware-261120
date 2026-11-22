# DTQSYS board variant for SlimeNRF 261120

This source tree adds `promicro_uf2/nrf52840/dtqsys` to the 261120 source, using the DTQSYS manufacturer's pin assignments. All 261120 upstream application changes are left intact, rather than backported piecemeal.

## Build

Install Nordic SDK/Zephyr dependencies and fetch the modules in `west.yml` (the repository targets the `jitingcn/sdk-nrf` `v3.4-branch`). Build for board `promicro_uf2/nrf52840/dtqsys` with `BOARD_ROOT` pointing to this repository, using the same sysbuild parameters as `.github/workflows/workflow.yml`.

The GitHub Actions tracker matrix now includes DTQSYS and will produce an artifact once built in a suitable GitHub repository with Actions enabled.

## Hardware pin mapping

- ICM45686 SPI3 MISO P1.09, MOSI P1.08, SCK P0.07, CS P0.04
- QMC6309 I2C0 SDA P0.24, SCL P0.22 (inherited)
- Power control P0.05; INT0 P0.02 (manufacturer raw flag 6); clock P0.12
- Battery VDDHDIV5, divider 1:5 (inherited)

## Cautions

- **Not compiled or tested**. Do not flash until Zephyr DTS/config validation, successful build, and a working bootloader recovery procedure are established.
- GPIO interrupt flags `6`, rotation `270`, external clock and power polarity follow available source defaults/manufacturer details; verify with physical hardware and logs.
- UF2 assumes Adafruit nRF52840 family ID; validate compatibility with the actual NICENANO bootloader. The prior non-rebooting UF2 issue is unresolved.
- Firmware receiver/protocol compatibility must be validated separately. Updating the receiver may be required.
- The upstream source ZIP may not contain git submodules; `west update` is required for a full build environment.
