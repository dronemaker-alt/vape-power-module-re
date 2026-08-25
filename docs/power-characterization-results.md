# Module-01 Power-System Characterization Results

This note holds conclusions from completed bench sessions. The blank sections are a reporting template, not evidence.

## Baseline evidence before characterization

### Confirmed

| Item | Status | Basis |
| --- | --- | --- |
| Power-management IC | Injoinic IP5305 | Identified device marking |
| Charge input | USB-C connector `J1`; charging observed | Module-01 observation |
| USB power nodes | `VBUS` charging input; USB-C `GND` board return | Recorded Module-01 node identification |
| Energy storage | 850 mAh single-cell Li-ion battery | Module-01 battery identification |
| Battery nodes | `B+` positive; `B-` negative / board return | Recorded Module-01 node identification |

### Provisional

| Observation | Why it remains provisional | Reproduction requirement |
| --- | --- | --- |
| Boost output approximately 4.5 V | Load, cell voltage, instrument setup, probe points, and output state were not recorded | Log all conditions and obtain an agreeing repeat reading |

### Unverified before the bench session

Charge current and termination; idle/sleep current; nominal boost regulation; minimum-load and timeout behavior; efficiency; continuous output capability; protection thresholds and recovery; battery-protection location; and the exact IP5305 board-level topology.

## Session reference

| Field | Result |
| --- | --- |
| Date / operator | |
| Module ID / PCB marking | Module-01 / `20250617` |
| Run sheet / raw-data location | |
| Photo location | |
| Starting battery condition / voltage | |
| Ambient temperature | |
| Test equipment | |
| Deviations from run sheet | |

## Results summary

Use **confirmed**, **provisional**, or **unverified** in the status column.

| Characteristic | Result | Conditions | Status | Evidence / notes |
| --- | --- | --- | --- | --- |
| Initial charge current | | | unverified | |
| Charge taper start | | | unverified | |
| Charge termination | | | unverified | |
| Output-off battery current | | | unverified | |
| Output-on battery current | | | unverified | |
| Sleep current | | | unverified | |
| Automatic-shutdown time | | | unverified | |
| No-load boost voltage | | | provisional | Earlier ~4.5 V observation awaits controlled reproduction |
| Loaded regulation band | | | unverified | |
| Minimum-load behavior | | | unverified | |
| Peak measured efficiency | | | unverified | |
| Maximum stable continuous load | | | unverified | |
| Low-voltage cutoff | | | unverified | |
| Low-voltage recovery | | | unverified | |
| Overcurrent trip / delay | | | unverified | |
| Overcurrent recovery | | | unverified | |
| Short-circuit response | | | unverified | |
| Short-circuit recovery | | | unverified | |
| Maximum observed temperature | | | unverified | |

## Boost-observation disposition

Earlier observation: approximately **4.5 V**, provisional.

Controlled reproduction:

- Cell voltage: `______ V`
- Output current/load: `______`
- Output state and elapsed time: `______`
- Instrument and probe points: `______`
- Trial 1: `______ V`
- Trial 2: `______ V`
- Disposition: confirmed / remains provisional / not reproduced
- Reason: `________________`

## Protection and anomaly notes

Record trip behavior, reset sequence, output droop, oscillation, audible noise, unexpected indications, and temperature behavior:

`________________________________________________________________`

`________________________________________________________________`

## Conclusions

### Newly confirmed

- None yet.

### Provisional findings

- Boost output approximately 4.5 V, pending a controlled repeat measurement.

### Remaining unknowns

- Charge profile and termination.
- Idle, active, and sleep current.
- Boost regulation, efficiency, and continuous-load capability.
- Low-voltage, overcurrent, and short-circuit thresholds and recovery.
- Battery-protection location and exact board-level power topology.

## Evidence review

A result can move to **confirmed** only when the measurement conditions are recorded and the observation is repeatable. A single reading, incomplete setup record, inferred topology, or datasheet-typical value remains provisional or unverified.

Related: [hardware overview](hardware-overview.md), [bench run sheet](power-characterization-run-sheet.md), and issue [#5](https://github.com/dronemaker-alt/vape-power-module-re/issues/5).
