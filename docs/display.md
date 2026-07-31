# Display Investigation Checklist

## Objective

Identify the display electrical interface, capture a repeatable power-up and animation transaction, and preserve enough physical and timing detail to compare later module revisions.

## Current Knowledge

| Item | Status | Notes |
| --- | --- | --- |
| Display present | Confirmed | Small display attached to the main PCB |
| Flex connection | Confirmed | Treat exposed flex contacts as fragile probe points |
| Display technology | Likely segmented OLED | Confirm by inspecting the unpowered panel and flex routing |
| MCU controlled | Suspected | Verify by correlating display activity with MCU-side signals |
| Orientation and segment map | Unknown | Photograph before removal or continuity testing |
| Controller location | Unknown | May be on the panel/flex or implemented by the main MCU |

Do not assume that every flex conductor is digital. A bare segmented OLED may expose common/segment drive lines with alternating waveforms rather than a conventional data bus.

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

| Flex pin | PCB/test point | Resistance to GND | Unpowered trace destination | Initial hypothesis | Confidence |
| ---: | --- | ---: | --- | --- | --- |
| 1 |  |  |  |  | Unknown |
| 2 |  |  |  |  | Unknown |
| 3 |  |  |  |  | Unknown |
| 4 |  |  |  |  | Unknown |

Add rows until every conductor is represented.

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

`2026-07-31_Module-01_Rev-A_CAP-01_cold-boot_24MHz.sal`

## Comparison Rules

- Use the same module orientation, flex-pin numbering, ground point, stimulus, channel order, and capture IDs for every revision.
- Keep raw captures immutable; save decoder experiments as copies or session metadata.
- Record unknowns explicitly rather than carrying an old guess forward.
- Mark a signal **Confirmed** only when supported by continuity/trace evidence plus a matching waveform or repeatable functional correlation.
- Mark a signal **Probable** when the protocol decode and electrical behavior agree but the trace destination is not confirmed.
- Mark a signal **Tentative** when based on waveform resemblance alone.
- When comparing revisions, list changed pinout, voltage, timing, initialization, address/command, and segment-mapping behavior.

## Completion Criteria

The display investigation is ready for a driver or emulator attempt when:

- [ ] Every flex conductor has a physical pin number.
- [ ] Power, ground, and any elevated-voltage pins are identified.
- [ ] The interface type and logic levels are confirmed or narrowed to one testable hypothesis.
- [ ] Cold-start initialization and a full animation cycle have repeatable raw captures.
- [ ] Timing, framing, bit order, and control-line polarity are documented.
- [ ] At least one visible segment or icon is correlated with captured data or drive lines.
- [ ] Capture files, photographs, channel maps, decoder settings, and confidence levels are recorded.
- [ ] Remaining unknowns are listed as specific next experiments.
