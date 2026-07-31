# Hardware Overview

## Purpose

This document is the stable entry point for the recovered vape power module. It summarizes the known hardware, identifies the reference unit used for comparison, and routes detailed measurements and findings to the supporting documents.

> [!IMPORTANT]
> This is a reverse-engineering record, not a finished schematic. Statements marked **confirmed** are based on direct observation or measurement. Items marked **unconfirmed** remain working hypotheses until traced or tested.

## Reference module

**Module-01** is the baseline reference board for this project. Preserve it as the least-modified sample and use its board orientation, connector names, test-point labels, photographs, and measurements when comparing later modules or revisions.

Unless another module is named explicitly, measurements and signal names in this repository refer to Module-01.

See [Reference board lab map](reference-board.md) for the baseline measurement set and comparison conventions.

## Module summary

| Area | Current understanding | Status |
| --- | --- | --- |
| Input power | USB-C connector supplies external power for charging and board operation. | Connector confirmed; USB-C configuration and supported input modes unconfirmed |
| Battery | Rechargeable single-cell lithium pouch cell connected directly to the module by two leads. | Cell type and polarity confirmed by inspection; capacity, condition, and protection arrangement require measurement |
| Power path | USB-C input feeds the charge/power-management section. The battery feeds the controller/display electronics and the high-current output stage. | Functional path inferred from construction; rail voltages and component-level routing unconfirmed |
| Display | Small color display driven from the main PCB and used for status/animation output. | Presence confirmed; controller, pinout, voltage, and bus type unconfirmed |
| MCU | Main logic device controls the user interface, display, sensing, and power-stage behavior. A visible package marking has been recorded for identification work. | Device present; exact manufacturer, part number, architecture, and programmability unconfirmed |
| External/test access | USB-C, battery leads, display connection, output wiring, and PCB test pads are the primary investigation points. | Physical features confirmed; signal assignments remain under investigation |

## Functional power path

```text
USB-C input
    |
    +--> charge / power-management circuitry --> single-cell battery
                                                |
                                                +--> regulated logic rails --> MCU --> display
                                                |
                                                +--> switched high-current output stage
```

The diagram is intentionally functional. It must not be treated as proof of rail topology, power sharing, boost/buck conversion, or protection placement until those paths are traced and measured.

## Display

The display is a salvage target as well as a diagnostic window into the original firmware. Investigation should establish:

- connector/pad pin count and supply voltage;
- ground and power pins;
- likely SPI, parallel, I2C, or custom signaling;
- reset, chip-select, command/data, clock, and backlight behavior;
- logic-analyzer captures during boot and animation changes;
- controller or flex-cable markings.

Record probes and captures in [Display investigation](display.md). Add confirmed connections to the [Signal map](hardware/pinout.md).

## Battery and power electronics

Treat the battery, charger, protection behavior, logic supply, and high-current output as separate subsystems until measurements prove how they interact. The baseline characterization should cover charge current, idle current, boost or conversion efficiency, maximum continuous load, and shutdown/protection behavior.

Use the [Power-system bench test](power-system-bench-test.md) for the ordered test sequence and pass/fail criteria. Record measured connections and rails in the [Signal map](hardware/pinout.md).

## MCU

The MCU identity is not yet confirmed. Do not equate a package marking with a public part number without a matching datasheet or pinout. The investigation should determine:

- complete top marking and package dimensions;
- power and ground pins;
- oscillator or crystal connections;
- reset, boot, SWD/JTAG/UART, or other debug candidates;
- connections to the display, sensors, buttons, and power-stage control;
- whether firmware readout or reprogramming is practical.

Preserve raw markings, photos, continuity results, and failed identification attempts in the [Reverse-engineering log](reverse-engineering-log.md).

## Related documentation

- [Reference board lab map](reference-board.md) — Module-01 baseline, photo orientation, labels, and comparison rules.
- [Signal map](hardware/pinout.md) — battery, USB-C, display, output, and test-pad connections with confidence levels.
- [Display investigation](display.md) — probe order, likely interfaces, logic-analyzer captures, and observation checklist.
- [Power-system bench test](power-system-bench-test.md) — charge, idle, efficiency, load, and protection tests.
- [Reverse-engineering log](reverse-engineering-log.md) — dated procedures, observations, measurements, conclusions, and next actions.

## Update rule

Keep this page concise and stable. Promote a finding here only after it is supported by a trace, measurement, repeatable behavior, legible component identification, or a cited datasheet. Put raw evidence and evolving hypotheses in the related investigation documents.
