# Board Revisions

Module-01 is the reference anchor. Claim a revision only from a visible marking, measurement, trace, or repeatable behavior. Keep photo-confirmed facts separate from previous records and inference.

## Revision table

| Board ID | Identifying evidence | PCB / display | IC markings | Pads / connectors | Battery | Behavior | Status |
|---|---|---|---|---|---|---|---|
| Module-01 | Photo-confirmed vertical PCB marking `20250617` | Photo-confirmed elongated black PCB; display and controls on component side; rear insulating strip, display interconnect, battery pads, U3 area, and three lower contacts. Custom segmented display geometry is visible; technology, part number, and interface **unknown**. | PFS123 MCU and IP5305 PMIC were previously recorded in issue #9, but neither package marking is independently confirmed by these photos. Exact U2/U3 identities and assignment remain **unknown from this photo set**. | Photo-confirmed `J1`, `KEY`, `DATA`, `GND`, `VIN`, `B+`, `B-`, `TP-B+`, and `TP-B-`. Unlabeled contact functions remain **unknown**. | Photo-confirmed pouch cell and red/black wiring. Label, manufacturer, chemistry marking, voltage, and capacity remain **unknown from photos**; 850 mAh is a previous record only. | Working and USB-C charging were previously observed; other firmware behavior is **unknown / untested here**. | Reference anchor. Layout and listed silkscreen are photo-confirmed; other identities require their non-photo source or new bench evidence. |

## Photo evidence

Cleaned derivatives were added in [commit `43b4d00`](https://github.com/dronemaker-alt/vape-power-module-re/commit/43b4d00fdd2bff4815b02ac8cbb1b73a30469b80). Cleanup does not make an unreadable marking known.

| View | Photo | Photo-confirmed evidence | Unknown / not shown |
|---|---|---|---|
| Component/display side | [front](../photos/module-01-pcb-front-clean.jpg) | Display geometry; pushbutton and `KEY`; `U2` designator; USB-C `J1`; `DATA`, `GND`, `VIN`; `20250617`; surrounding designators | Complete U2 marking; display part number, technology, protocol |
| Rear/battery side | [rear](../photos/module-01-pcb-rear-clean.jpg) | Display interconnect; insulating strip; `TP-B+`, `TP-B-`, `B+`, `B-`; U3 area; three lower contacts; pouch cell and wiring | U3 marking; battery label/rating; contact functions |
| Rear U3/battery detail | [detail](../photos/module-01-pcb-rear-detail-clean.jpg) | U3 area/designator; `B-`; `TP-B-`; nearby passives; pouch cell; detached two-wire connector | Exact U3 marking; battery label/rating; connector destination |
| Assembled module | Not captured | — | Enclosure markings, orientation, external revision labels |
| IC macros | Not captured | — | Independent confirmation of remaining IC markings |
| Battery-label macro | Not captured | — | Manufacturer, chemistry marking, nominal voltage, capacity |

## Copy-ready comparison note

```markdown
### Module-XX compared with Module-01

| Item | Module-01 baseline | Module-XX evidence | Confirmed difference? | Source |
|---|---|---|---|---|
| PCB marking | `20250617` | unknown | unknown | photo/log link |
| Layout / display | See Module-01 photo index; display interface unknown | unknown | unknown | |
| Readable IC markings | unknown from current macro coverage | unknown | unknown | |
| Labeled pads / connectors | J1, KEY, DATA, GND, VIN, B+, B-, TP-B+, TP-B- | unknown | unknown | |
| Battery label / rating | unknown from photos | unknown | unknown | |
| Firmware behavior | Working and USB-C charging previously observed | unknown | unknown | |

**Revision decision:** unknown / same observable revision / confirmed new revision
**Confidence:** low / medium / high
**Notes:** Record facts first; keep inference separate.
```

Sources: [issue #3](https://github.com/dronemaker-alt/vape-power-module-re/issues/3), [issue #9](https://github.com/dronemaker-alt/vape-power-module-re/issues/9), and [Reference Board](reference-board.md).
