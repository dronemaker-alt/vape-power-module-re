# Reference Board

Module-01 is the baseline for photographs, measurements, trace names, and revision comparisons.

| Property | Baseline | Evidence status |
|---|---|---|
| Module ID | Module-01 | Project-assigned anchor |
| PCB marking | `20250617` | Photo-confirmed |
| Display | Custom segmented display assembly | Geometry photo-confirmed; technology, part number, and interface **unknown** |
| MCU | Previously recorded as Padauk PFS123 | Current photos do not independently confirm the marking; remaining marking **unknown** |
| PMIC | Previously recorded as Injoinic IP5305 | Current photos do not independently confirm the marking; remaining marking **unknown** |
| Battery | Attached pouch cell with red/black wiring | Presence/wiring photo-confirmed; label, manufacturer, chemistry marking, voltage, and capacity **unknown from photos**. 850 mAh is previously recorded only |
| Status | Working; USB-C charging | Previously observed, not established by still photos |

## Photo evidence

The cleaned set was added by [commit `43b4d00`](https://github.com/dronemaker-alt/vape-power-module-re/commit/43b4d00fdd2bff4815b02ac8cbb1b73a30469b80).

- [Front](../photos/module-01-pcb-front-clean.jpg): confirms display geometry, pushbutton/`KEY`, `U2` designator, `J1`, `DATA`, `GND`, `VIN`, `20250617`, and nearby designators.
- [Rear](../photos/module-01-pcb-rear-clean.jpg): confirms display interconnect, insulating strip, `TP-B+`, `TP-B-`, `B+`, `B-`, U3 area, three lower contacts, pouch cell, and wiring.
- [Rear detail](../photos/module-01-pcb-rear-detail-clean.jpg): confirms U3 area/designator, `B-`, `TP-B-`, nearby passives, pouch cell, and detached two-wire connector.

The photos do **not** confirm the complete U2/U3 top markings, battery label or capacity, display protocol, connector destination, or lower-contact functions. Those remain **unknown** until supported by a legible macro, trace, measurement, or bench observation.

See [Board Revisions](board-revisions.md) for the full evidence table and reusable comparison template. Sources: [issue #9](https://github.com/dronemaker-alt/vape-power-module-re/issues/9) and [issue #3](https://github.com/dronemaker-alt/vape-power-module-re/issues/3).
