# Module-01 Hardware Overview

Module-01 is the working reference board for this reverse-engineering project. Unless another module is named, hardware names and measurements in this repository refer to Module-01.

This page records only confirmed or previously observed facts from issues [#8](https://github.com/dronemaker-alt/vape-power-module-re/issues/8) and [#9](https://github.com/dronemaker-alt/vape-power-module-re/issues/9). It is not a schematic.

## Confirmed hardware

| Area | Confirmed fact |
| --- | --- |
| USB-C | USB-C connector `J1` is fitted. USB-C charging has been observed. `VBUS` is the charging input and USB-C `GND` is board return. |
| Battery | Module-01 uses an 850 mAh single-cell Li-ion battery. `B+` is battery positive and `B-` is battery negative / board return. |
| Power management | The power-management IC has been identified as an Injoinic IP5305. |
| Controller | The MCU has been identified as a Padauk PFS123. |
| Display | A custom segmented display assembly is fitted. Its physical layout has been photographed. |
| Test access | Visible PCB labels include `TP-B+`, `TP-B-`, `KEY`, `DATA`, `GND`, and `VIN`. The board also has a test point provisionally named `TP1` in the signal-map work. |

The component-side PCB marking `20250617` is visible in the reference photographs.

## Reference photographs

- [PCB front — display and component side](../photos/module-01-pcb-front-clean.jpg)
- [PCB rear — battery side](../photos/module-01-pcb-rear-clean.jpg)
- [PCB rear — U3 and battery detail](../photos/module-01-pcb-rear-detail-clean.jpg)

## Unknowns

- USB-C CC1/CC2 resistor values, destinations, and supported input modes.
- Exact IP5305 package orientation, physical pin numbering, rail voltages, and board-level connections.
- Exact PFS123 package orientation, physical pin numbering, supply pins, programming/debug access, and GPIO assignments.
- Battery condition and whether protection is on the cell, PCB, or both.
- Display technology, pin order, supply voltage, interface/protocol, signal direction, and whether the PFS123 drives it directly.
- Electrical functions of `KEY`, `DATA`, `VIN`, `TP1`, and the three lower spring/contact pins.
- Connections between the USB-C input, IP5305, battery, PFS123, display, and other loads beyond the confirmed nodes listed above.
- Differences between Module-01 and any other board revision.

## Evidence rule

Promote an unknown to a confirmed fact only when supported on Module-01 by a recorded trace, measurement, repeatable observation, legible marking, or matching component documentation. Keep inferred topology and probe plans in the signal-map and subsystem documents.

## Related documentation

- [Reference board](reference-board.md)
- [Board revisions](board-revisions.md)
- [Display investigation](display.md)
