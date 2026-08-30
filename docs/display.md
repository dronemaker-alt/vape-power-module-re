# Module-01 Display Connector and Protocol Capture

## Objective

Number the photographed Module-01 display interconnect, separate likely supply and communication conductors from unresolved pins, and obtain the smallest capture that can distinguish a serial protocol from direct segment drive.

## Current Knowledge

| Item | Status | Notes |
| --- | --- | --- |
| Display present | Confirmed | Small display attached to the main PCB |
| Display interconnect | Confirmed | Eight soldered conductors are visible in the rear photograph |
| Display technology | Unknown | The photographs show a custom segmented display assembly, but not its electrical technology |
| MCU controlled | Suspected | Verify by correlating display activity with MCU-side signals |
| Orientation and segment map | Unknown | Photograph before removal or continuity testing |
| Controller location | Unknown | May be on the panel/flex or implemented by the main MCU |

The photographs confirm the conductor count and location only. They do not establish pin functions, supply voltage, protocol, controller location, or even that every conductor is digital. A bare segmented display may expose common/segment drive lines rather than a conventional data bus.

## Connector Reference and Evidence Boundary

Use the rear/battery-side photograph with the PCB upright (`TP-B+` toward the top and the three spring contacts toward the bottom). Number the eight display solder joints from top to bottom as **DISP-1** through **DISP-8**. This is a project measurement reference, not a claim about the display manufacturer's pin numbering.

| Project pin | Photo-backed identification | Likely class before measurement | Status / confirming test |
| ---: | --- | --- | --- |
| DISP-1 | Top solder joint in the eight-conductor row | Power, data, control, or direct drive | Unknown; continuity and powered waveform required |
| DISP-2 | Second joint from top | Power, data, control, or direct drive | Unknown; continuity and powered waveform required |
| DISP-3 | Third joint from top | Power, data, control, or direct drive | Unknown; continuity and powered waveform required |
| DISP-4 | Fourth joint from top | Power, data, control, or direct drive | Unknown; continuity and powered waveform required |
| DISP-5 | Fifth joint from top | Power, data, control, or direct drive | Unknown; continuity and powered waveform required |
| DISP-6 | Sixth joint from top | Power, data, control, or direct drive | Unknown; continuity and powered waveform required |
| DISP-7 | Seventh joint from top | Power, data, control, or direct drive | Unknown; continuity and powered waveform required |
| DISP-8 | Bottom solder joint in the eight-conductor row | Power, data, control, or direct drive | Unknown; continuity and powered waveform required |

Do not identify any DISP pin with the separately labeled `DATA`, `GND`, or `VIN` pads near USB-C. The photographs show those labels but do not show electrical continuity between those pads and the display connector.

### Sorting power from signals

1. With battery and USB disconnected, continuity to confirmed `B-`/USB-C ground makes a pin the **ground candidate**. Record resistance rather than promoting it from a photograph.
2. Power normally and measure all eight pins with a DMM or scope. A stable DC level that appears whenever the display is enabled is a **supply candidate**; verify against a nearby decoupling capacitor or regulator output. Any voltage above the analyzer input rating remains scope-only.
3. Pins that toggle in bursts at wake are **serial data/control candidates**. Two idle-high, open-drain-looking lines suggest I²C; clock plus data plus a framing line suggests SPI or custom synchronous serial.
4. Pins with continuous periodic, multi-level, alternating, or phase-related waveforms are **direct COM/SEG candidates**, not ordinary logic-analyzer inputs until their voltage range is known.
5. A static pin that changes only at wake may be reset, enable, data/command, chip-select, or a bias node. Leave it unknown until timing or continuity distinguishes it.

## Bus-Type Priority

Investigate in this order:

1. **SPI-like serial** — most likely when four or more active digital lines are present: clock, data, chip-select, and possibly data/command or reset.
2. **I²C-like serial** — likely when exactly two pulled-up digital lines toggle together, normally with idle-high clock and data.
3. **Three-wire or custom synchronous serial** — likely when clock and data are visible but chip-select, framing, or direction does not match standard SPI.
4. **Direct segment/common drive** — likely when many lines carry continuous, repeated, multi-level, or bipolar waveforms and no command burst is evident.
5. **Parallel interface** — lowest initial priority; consider only if several data lines change simultaneously around a separate strobe.

## Equipment and Setup

- [ ] Assign the module ID and hardware revision.
- [ ] Use the reference board/module selected for baseline measurements.
- [ ] Photograph the display, flex, connector, and PCB routing before attaching probes.
- [ ] Mark display orientation: top, bottom, pin 1, battery side, and USB-C side.
- [ ] Record the logic-analyzer model, probe arrangement, software, and decoder version.
- [ ] Establish a short, reliable ground connection at a confirmed PCB ground.
- [ ] Verify probe voltage compatibility before connecting.
- [ ] Power the module in its normal configuration for the first capture.
- [ ] If available, record supply voltage and current alongside each operating state.

## Phase 1 — Unpowered Inspection

- [ ] Count the flex conductors and number them consistently from one photographed end.
- [ ] Record connector pitch, flex markings, panel markings, and any visible controller IC.
- [ ] Trace obvious conductors to ground, battery/rail, MCU pins, resistors, capacitors, or test pads.
- [ ] Measure resistance to ground on every display pin.
- [ ] Check continuity from display pins to nearby test pads and MCU pins.
- [ ] Identify likely power and ground pins from copper width, decoupling, and continuity.
- [ ] Look for pull-up resistors shared by two signal lines; this increases the likelihood of I²C.
- [ ] Look for a cluster of series resistors or direct MCU connections; this may indicate SPI or direct drive.
- [ ] Do not use diode/ohms measurements on a powered module.

### Pin Survey

| Project pin | PCB/test point | Resistance to GND | Unpowered trace destination | Initial hypothesis | Confidence |
| ---: | --- | ---: | --- | --- | --- |
| DISP-1 |  |  |  |  | Unknown |
| DISP-2 |  |  |  |  | Unknown |
| DISP-3 |  |  |  |  | Unknown |
| DISP-4 |  |  |  |  | Unknown |
| DISP-5 |  |  |  |  | Unknown |
| DISP-6 |  |  |  |  | Unknown |
| DISP-7 |  |  |  |  | Unknown |
| DISP-8 |  |  |  |  | Unknown |

## Phase 2 — First Powered Probes

Begin with an oscilloscope or logic analyzer in analog-capable mode. Observe first; do not inject signals.

- [ ] Measure the DC voltage on every flex pin with the display idle.
- [ ] Observe every non-power pin during power-up and one complete animation cycle.
- [ ] Separate constant rails from active signals.
- [ ] Note idle level, minimum/maximum voltage, pulse shape, repetition rate, and whether activity is bursty or continuous.
- [ ] Check for a boosted OLED rail; do not attach a digital-only analyzer input until its voltage is known.
- [ ] Compare these states:
  - [ ] Battery connected / module asleep
  - [ ] Wake or activation
  - [ ] Normal animation
  - [ ] User-input transition, if available
  - [ ] Low-battery or charging indication, if safely reproducible
  - [ ] Return to sleep

### Fast Classification

| Observation | Likely interpretation | Next action |
| --- | --- | --- |
| Two idle-high lines with pull-ups; one clocked, one data | I²C | Capture both and try 7-bit I²C decode |
| Clock, data, and a framing/chip-select line | SPI or custom synchronous serial | Capture all candidates; test SPI modes 0–3 |
| Clock and data with unusual framing | Three-wire/custom serial | Measure frame boundaries and bit order manually |
| Many continuously active periodic lines | Direct segment/common drive | Capture several lines simultaneously with analog voltage detail |
| Several data lines change around a strobe | Parallel bus | Capture strobe, control lines, and all suspected data lines |
| High-voltage or bipolar waveform | OLED segment/common or charge-pump node | Use a suitable scope probe; do not connect a low-voltage analyzer directly |

## Phase 3 — Logic-Analyzer Captures

### Minimum decisive capture

After the voltage survey proves every candidate is safe for the analyzer, connect all non-power DISP pins simultaneously, plus the analyzer ground at confirmed `B-`/USB-C ground. Capture one normal wake from a fully dark display:

- **Channels:** every voltage-safe, non-power DISP pin; retain physical names `DISP-n`.
- **Rate:** 10 MS/s minimum; use 24 MS/s if available.
- **Window:** about 100 ms before the wake stimulus through at least 2 s after the first visible update.
- **Trigger:** the first edge on any active DISP pin; if the analyzer cannot OR-trigger, arm it first and wake the module manually.
- **Save:** raw undecoded data first, plus a short video showing the display during the same event.
- **Repeat:** perform the identical wake once more only if the first trace is usable.

That single capture confirms the protocol class when it shows one of these signatures:

| Captured signature | Conclusion |
| --- | --- |
| Two idle-high lines with START/STOP, ACKs, and eight-bit transfers | I²C confirmed; record address and clock rate |
| Clocked data with a framing/chip-select line and consistent words | SPI-like/custom synchronous serial confirmed; test SPI modes 0–3 |
| Clock and data but non-SPI framing | Custom synchronous serial; record edge, word length, and gaps |
| Several phase-related lines active continuously, without command bursts | Direct segment/common drive; repeat with an oscilloscope for voltage and phase |
| No connector activity despite a visible change | Capture setup/pin access is incomplete, or the display/controller interconnect is not being observed at the correct point |

This is the smallest proof needed to classify the interface. Cold-start initialization, sleep, charging, segment mapping, and decoder refinement are follow-on captures, not prerequisites for the first protocol decision.

### Capture Settings

- [ ] Label analyzer channels with physical flex-pin and test-pad names, not guessed functions.
- [ ] Capture raw signals before enabling protocol decoders.
- [ ] Use at least 10× the measured clock frequency; 20× or more is preferred for uncertain edges.
- [ ] If the clock is unknown, begin at the analyzer's highest practical rate for a short capture.
- [ ] Set the digital threshold from measured logic-high and logic-low voltages.
- [ ] Trigger on power-on, wake input, suspected chip-select, or the first clock edge after idle.
- [ ] Preserve pre-trigger data so reset and initialization are included.
- [ ] Capture long enough to contain initialization plus at least one complete animation cycle.
- [ ] Repeat the same stimulus at least twice to distinguish fixed initialization from changing display data.

### Required Capture Set

- [ ] **CAP-01 — Cold power-up:** battery disconnected, then connected; include initialization.
- [ ] **CAP-02 — Wake from idle:** trigger on the user action or sensor event that wakes the display.
- [ ] **CAP-03 — Full animation:** record one complete loop from a known starting frame.
- [ ] **CAP-04 — State transition:** capture a visible change such as counter, icon, charging, or battery indication.
- [ ] **CAP-05 — Repeatability:** repeat CAP-02 or CAP-03 without changing the setup.
- [ ] **CAP-06 — Idle/sleep:** capture the final update and bus behavior as the display turns off.

### Decoder Attempts

For each decoder attempt, preserve the raw capture and record settings separately.

- [ ] I²C: list detected 7-bit addresses, read/write direction, ACK/NACK behavior, bus speed, and repeated starts.
- [ ] SPI: test modes 0–3 and record clock polarity, clock phase, bit order, word length, and chip-select polarity.
- [ ] Custom serial: record idle polarity, edge used for sampling, bits per frame, inter-frame gap, and any repeating header.
- [ ] Direct drive: measure common/segment frequency, phase relationship, duty cycle, voltage levels, and waveform symmetry.
- [ ] Parallel: identify data width, read/write or data/command controls, strobe polarity, and setup/hold relationship.

Do not rename a channel to SDA, SCLK, CS, COM, or SEG until the waveform supports that identification. Keep the physical name beside any functional alias.

## Phase 4 — Correlate Data With Visible Segments

- [ ] Record video or frame-by-frame photographs synchronized with a capture.
- [ ] Change only one visible condition at a time where possible.
- [ ] Compare captures to locate bytes, bits, or waveforms that change with that segment.
- [ ] Build a segment map using stable names such as DIG1_A, ICON_BATTERY, or BAR_03.
- [ ] Note whether the controller receives character values, a segment bitmap, or higher-level commands.
- [ ] Identify initialization commands separately from recurring display data.
- [ ] Estimate display refresh/update rate from repeated transactions or drive cycles.
- [ ] Verify each proposed mapping in at least two captures before marking it confirmed.

### Segment Map

| Visible element | Capture/event | Candidate byte/bit or drive pair | Evidence | Status |
| --- | --- | --- | --- | --- |
|  |  |  |  | Unknown |

## Exact Notes to Record for Every Session

### Module and Physical Context

- Date/time:
- Investigator:
- Module ID:
- PCB revision/markings:
- Display/flex markings:
- Flex-pin numbering reference:
- Display orientation:
- Photos:
- Any disassembly, damage, or rework since the previous session:

### Power and State

- Battery voltage:
- External supply voltage/current limit, if used:
- Idle current:
- Active/display-on current:
- Module state at trigger:
- Exact stimulus performed:
- Visible display result:
- Ambient or board temperature if relevant:

### Probe and Instrument Setup

- Scope/analyzer model:
- Software/firmware version:
- Probe type and attenuation:
- Ground point:
- Channel-to-flex-pin/test-pad mapping:
- Sample rate:
- Analog bandwidth, if applicable:
- Digital threshold:
- Trigger source and level:
- Pre-trigger percentage:
- Capture duration:
- Decoder and all decoder settings:

### Signal Results

For each channel, record:

- Physical pin/test point:
- Measured idle, low, and high voltages:
- Direction, if known:
- Pull-up/pull-down evidence:
- Frequency or clock rate:
- Active-high/active-low behavior:
- Activity state: initialization, animation, idle, or continuous:
- Proposed function:
- Confidence: Confirmed / Probable / Tentative / Unknown:
- Evidence and alternate interpretation:

### Capture Record

| Capture ID | File name | Module/revision | State and stimulus | Channels | Sample rate/threshold | Decoder/settings | Visible result | Key finding |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CAP-01 |  |  | Cold power-up |  |  | Raw |  |  |

Use filenames that sort and compare cleanly:

`YYYY-MM-DD_<module-id>_<pcb-rev>_<capture-id>_<event>_<sample-rate>.<ext>`

Example:
