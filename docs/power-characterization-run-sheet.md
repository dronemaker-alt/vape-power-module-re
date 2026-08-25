# Module-01 Power-System Bench Run Sheet

Use this sheet during one bench session. Enter measured values only; do not copy typical IP5305 values into result fields.

## Evidence status at session start

### Confirmed on Module-01

- Injoinic IP5305 power-management IC.
- USB-C connector `J1`; USB-C charging has been observed.
- USB-C `VBUS` is the charging input and USB-C `GND` is board return.
- 850 mAh single-cell Li-ion battery.
- `B+` is battery positive; `B-` is battery negative / board return.

### Provisional observation to reproduce

- Boost output was previously observed at approximately **4.5 V**.
- Load, cell voltage, instrument, probe points, and output state were not recorded. Treat this as provisional until reproduced with those conditions logged.

### Still unverified

- Charge-current profile and termination behavior.
- Idle, active, and sleep current.
- Nominal boost voltage, regulation, minimum-load behavior, and timeout.
- Efficiency and stable continuous output current.
- Low-voltage, overcurrent, and short-circuit thresholds and recovery.
- Battery protection location/behavior and exact IP5305 board-level connections.

## 1. Session record

| Field | Entry |
| --- | --- |
| Date / time | |
| Operator | |
| Module ID / PCB marking | Module-01 / `20250617` |
| Battery type / rating | Single-cell Li-ion / 850 mAh |
| Battery condition | |
| Starting cell voltage | |
| Ambient temperature | |
| USB source / current limit | |
| DMM(s) / ranges | |
| Battery ammeter or analyzer | |
| Electronic load | |
| Temperature probe | |
| Cell simulator, if used | |

- [ ] Photograph or label `GND`, `B+`, `B-`, USB-C input, boost output, and button/enable points.
- [ ] Verify source limits, meter polarity, common returns, and probe placement.
- [ ] Confirm the electronic load is disconnected or set to 0 A.
- [ ] Record the initial module state: USB disconnected; output off; display/indication noted.
- [ ] Use a known reset state before each protection test.

At every point record elapsed time, `Vcell`, `Ibat`, `Vusb`, `Iusb`, `Vout`, `Iout`, temperature, state/indication, and observations when applicable.

## 2. Charge characterization

**Start state:** boost output off; load disconnected.

| Point | Elapsed | Vusb | Iusb | Vcell | Ibat | Temp | Indication / notes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| Before USB | | — | — | | | | |
| 0–10 s after USB | | | | | | | |
| Steady charge | | | | | | | |
| Mid-charge | | | | | | | |
| Taper begins | | | | | | | |
| Termination | | | | | | | |
| Cell relaxed | | — | — | | | | |
| Recharge, if observed | | | | | | | |

- [ ] Record whether charge restarts after cell-voltage relaxation.
- [ ] Disconnect USB-C and allow the board to settle before idle-current tests.

## 3. Idle, sleep, and output control

**Start state:** battery only; no external load.

| State / action | Elapsed | Vcell | Ibat | Vout | Temp | Indication / notes |
| --- | ---: | ---: | ---: | ---: | ---: | --- |
| Output off after reset | | | | | | |
| Output enabled, no load | | | | | | |
| Output on, display active | | | | | | |
| Output on, display off | | | | | | |
| Automatic shutdown | | | | | | |
| Settled sleep | | | | | | |
| Repeat wake/sleep | | | | | | |

Trigger/button action: `________________`  
Enable behavior: momentary / latched / other: `________________`  
Exact restart sequence: `________________`

## 4. Boost baseline and provisional-observation check

**Start state:** battery only; output enabled; load at 0 A.

| Trial | Vcell | Ibat | Vout | Iout | Output state | Instrument / probe points | Notes |
| ---: | ---: | ---: | ---: | ---: | --- | --- | --- |
| 1 | | | | 0 | | | |
| 2 | | | | 0 | | | |

- [ ] State whether the earlier ~4.5 V observation was reproduced.
- [ ] Record output timeout or minimum-load behavior.
- [ ] Keep the result provisional unless the conditions above are complete and a repeat trial agrees.

## 5. Load sweep, regulation, and efficiency

Run at mid cell voltage first. Repeat at high and near-cutoff cell voltage if practical. Increase load in controlled steps and allow readings to settle.

`Pin = Vcell × Ibat`  
`Pout = Vout × Iout`  
`Efficiency = Pout / Pin × 100%`

| Run / step | Elapsed | Vcell | Ibat | Vout | Iout | Pin | Pout | Eff. | Temp | Stable / notes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| Mid / 0 | | | | | 0 | | | | | |
| Mid / 1 | | | | | | | | | | |
| Mid / 2 | | | | | | | | | | |
| Mid / 3 | | | | | | | | | | |
| Mid / 4 | | | | | | | | | | |
| Mid / 5 | | | | | | | | | | |
| High / | | | | | | | | | | |
| Near cutoff / | | | | | | | | | | |

Highest stable point held for: `______ min`  
Maximum stable continuous load: `______ A`  
Acceptance basis: `________________`

Record droop, oscillation, reset, audible noise, or shutdown. Do not report a brief pre-trip peak as a continuous rating.

## 6. Protection thresholds and recovery

Use a cell simulator for low-voltage testing and controlled current limiting for fault tests.

### Low-voltage cutoff

| Trial | Fixed load | Start Vcell | Cutoff Vcell | Recovery Vcell | Recovery action | Notes |
| ---: | ---: | ---: | ---: | ---: | --- | --- |
| 1 | | | | | | |
| 2 | | | | | | |

Recovery actions checked: automatic / button / USB input / battery reconnect.

### Overcurrent

| Trial | Last stable Iout | Trip Iout | Vout before trip | Trip delay | Recovery action | Notes |
| ---: | ---: | ---: | ---: | ---: | --- | --- |
| 1 | | | | | | |
| 2 | | | | | | |

### Controlled short-circuit response

| Trial | Source/load current limit | Response time | Residual Vout | Peak temp | Recovery action | Post-recovery Vout |
| ---: | ---: | ---: | ---: | ---: | --- | ---: |
| 1 | | | | | | |

- [ ] Remove the fault before testing recovery.
- [ ] Verify normal no-load boost output after recovery.

## 7. Closeout

- [ ] Save raw readings and photographs with Module-01 and the session date.
- [ ] Copy measured conclusions into [the results note](power-characterization-results.md).
- [ ] Mark single observations or incompletely recorded conditions as provisional.
- [ ] Leave untested items unverified; do not convert blanks into zeroes.
- [ ] Add the completed results to issue [#5](https://github.com/dronemaker-alt/vape-power-module-re/issues/5).
