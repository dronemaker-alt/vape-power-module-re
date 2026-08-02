# vape-power-module-re

Reverse engineering of a USB-C rechargeable disposable vape power module built around an Injoinic IP5305 power-management IC, a Padauk PFS123 MCU, a single-cell Li-ion battery, and a small display.

## Documentation

- **[Hardware overview](docs/hardware-overview.md)** — stable module summary and entry point.
- **[Power system](../../issues/6)** — charging, regulation, load, efficiency, and protection test plan.
- **[Display](docs/display.md)** — interface identification and logic-analyzer checklist.
- **[Pinout](../../issues/8)** — battery, USB-C, display, MCU, and test-pad signal map.
- **[Board revisions](../../issues/3)** — revision comparison record.
- **[Reference board](../../issues/9)** — Module-01 baseline and comparison conventions.
- **[Reverse-engineering log](../../issues/4)** — chronological observations, measurements, and test results.
- **[Reuse concepts](docs/concepts/README.md)** — applications built around recovered modules.
  - **[MÍTILL avionics backpack](docs/concepts/mitill-backpack.md)** — self-powered GNSS, IMU, logging, and telemetry payload.

## Repository areas

- `photos/` — board and teardown images
- `hardware/` — schematics, layouts, and physical notes
- `firmware/` — MCU and protocol work
- `logic-analyzer/` — captures and decoder notes
- `datasheets/` — component references

Confirmed findings belong in the documentation; raw observations and evolving hypotheses belong in the reverse-engineering log.
