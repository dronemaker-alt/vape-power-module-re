# MÍTILL Modular Avionics Backpack

> **Pronunciation:** approximately **MEE-till**  
> **Working expansion:** **Modular Independent Telemetry, Intelligence, Location, and Logging**

## Concept

MÍTILL is a detachable, self-powered avionics backpack that attaches to a TinyWhoop or other small unmanned aircraft without consuming power from the host. Like the tick or mite that inspired its name, it latches onto a host, travels with it, and operates as an independent attached system.

The concept grew from a conversation with **Rob**, a coworker who regularly shares drone ideas and material with the project.

## Purpose

Reuse the recovered rechargeable vape PowerPac as a removable energy cartridge for an avionics package that can move between aircraft. The backpack should provide useful navigation, sensing, telemetry, and logging even when the host flight controller exposes no data interface.

## Proposed subsystem stack

| Subsystem | Initial role |
| --- | --- |
| Recovered PowerPac | Independent rechargeable power source |
| Companion MCU | Sensor fusion, logging, communications, and host-interface management |
| GNSS receiver | Position, ground speed, time, and independent flight-track recording |
| IMU | Independent motion, attitude-change, vibration, and event data |
| Storage | Local flight and diagnostic logs |
| Radio or host link | Telemetry and optional exchange with the aircraft flight controller |
| Remote ID | Possible future function where appropriate for the aircraft and mission |
| Status interface | Minimal LED, display, button, or wireless configuration path |

## Operating modes

1. **Independent logger** — no electrical connection to the host; records GNSS and IMU data locally.
2. **Telemetry parasite** — listens to a host UART or other exposed bus without controlling the aircraft.
3. **Companion mode** — exchanges commands and data with a compatible flight controller.
4. **Transferable payload** — moves between aircraft using a standardized mechanical mount and connector.

## Design principles

- Do not depend on the host battery for normal operation.
- Keep the PowerPac removable and rechargeable through its existing USB-C path where practical.
- Make the minimum configuration useful even with no host data connection.
- Use a repeatable mount, connector, pinout, and center-of-gravity reference.
- Separate confirmed PowerPac capabilities from proposed backpack functions.
- Preserve raw sensor data so later firmware can reprocess early flights.

## First design questions

- What useful capacity, mass, discharge rate, and protection behavior does each candidate PowerPac provide?
- Which companion MCU gives the best capability-to-mass ratio?
- Can one compact sensor package provide both a suitable IMU and barometer?
- What GNSS module and antenna geometry work on a TinyWhoop-scale airframe?
- How much endurance remains after accounting for MCU, GNSS, sensors, storage, and radio loads?
- Which host interfaces should be standardized first: passive UART, MSP, MAVLink, I2C, or standalone only?
- What mounting position minimizes GNSS interference, vibration error, and center-of-gravity shift?
- Should Remote ID be a base feature, optional daughterboard, or separate MÍTILL variant?

## Proposed first prototype

Build **MÍTILL-01** as a standalone logger before attempting flight-controller integration:

- one characterized PowerPac;
- low-power ESP32-class companion MCU;
- GNSS receiver;
- IMU;
- local storage;
- USB-C charge/configuration access;
- removable TinyWhoop mounting cradle.

Success means the backpack can power independently, acquire a GNSS fix, timestamp and record synchronized GNSS/IMU data, survive a short flight, and export a readable log.

## Related work

- [Hardware overview](../hardware-overview.md)
- [Power-system bench test](../power-system-bench-test.md)
- [Signal map](../hardware/pinout.md)
