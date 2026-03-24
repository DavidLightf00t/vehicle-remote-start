# Honda Remote Start

ESPHome-based vehicle remote start project that lets me trigger my Honda’s
remote start, lock, and unlock functions through Home Assistant.

This project is still evolving. The current setup works on my home network, and
I’m planning to extend it with cellular connectivity using an IoT SIM so it can
be used away from home as well.

## Overview

This project uses an ESP32-S3 running ESPHome to control a set of relays tied
to a physical key fob. Home Assistant provides the user interface, and the ESP
handles the timing and switching needed to simulate button presses.

In addition to the remote start function, the project is being developed to
support:

- Lock doors
- Unlock doors
- Start the engine remotely
- Vehicle telemetry / CAN bus experiments
- Secure remote access and time synchronization

## Current Status

- Home Assistant integration: working
- ESPHome firmware: working
- Relay / fob power control: working
- Remote start sequence: implemented
- CAN bus telemetry parsing: experimental
- IoT SIM integration: planned
- Cellular / off-network use: in progress

## Hardware

Current hardware includes:

- ESP32-S3 DevKitC-1
- Relay outputs for:
  - Key fob power
  - Lock
  - Unlock
  - Start
- Working Car Key
- Perf Board
- Pin Headers
- Dashcam Hardwire Kit
- Bipolar Transistors

Vehicle Telemetry (Optional):

- OBD-II Connector (With wires exposed)
- CAN Board (To read and write to CAN BUS)

Tools:

- Soldering Iron with Heat Station
- Soldering Wire
- Desoldering Wick
- Flux
- Electrical Wire
    - I used 30 gauge wire but I believe a thicker wire 
      like 22 gauge would have worked better here.


> Note: This project is custom-built around my own setup. Your vehicle, key
> fob, and wiring may require different timing or hardware.

## Software Stack

- ESPHome
- Home Assistant
- ESP-IDF framework
- SNTP for time synchronization
- Optional MQTT / secure remote connectivity planning
- C++ lambdas inside ESPHome for custom logic

## How It Works

The ESP32 exposes buttons in Home Assistant:

- **Start Engine**
- **Lock Doors**
- **Unlock Doors**

When a button is pressed, ESPHome runs a scripted sequence that:

1. Powers the key fob
2. Waits for the fob to initialize
3. Pulses the appropriate relay
4. Waits the required amount of time
5. Turns everything back off

This helps simulate the physical button presses on the fob in a controlled way and use less power.

## Project Goals

The goal of this project is to create a reliable, documented, and secure way
to control a vehicle remotely through a home assistant setup.

Longer term goals include:

- Adding an IoT SIM for connectivity outside the home
- Improving security around remote access
- Adding better telemetry from the vehicle
- Cleaning up the firmware and making the configuration easier to maintain
- Documenting the wiring and hardware more clearly

## Repository Layout

The current goal for this repository is:

```text
vehicle-remote-start/
  README.md
  .gitignore

  firmware/
    esphome/
      honda-remote-start.yaml
      secrets.example.yaml

  hardware/
    bom.md
    wiring.md
    pinout.md
    photos/

  docs/
    architecture.md
    troubleshooting.md
    notes.md
