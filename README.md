# Voyager keyboard with RP2354A

This repository contains the necessary files for manufacturing of a split keyboard with on-board RP2354A microcontroller.

Features:

- On-board RP2354A MCU (2MB flash) for each side
- USB-C connection for power, firmware update, and a separate USB-C for UART connection between the halves
- RGB matrix under each key
- Gateron KS-33 / Kailh Choc v1 / Kailh Choc v2 low-profile keyswitches
- 1.2mm top plate (mainly planning for KS-33)

Non-features:

- Wireless functionality
- No tooling for mass production beyond common PCB houses and hobbyist CNC/3D print.

## What is Voyager?

Voyager is a minimal, split keyboard by [ZSA Technology Labs](https://www.zsa.io/), the same company who was behind the now discontinued Planck EZ.

The original Voyager is using an STM32 MCU, with RGB matrix. It has 52 keys, and 52 LEDs.

## Project status

Version v1.0 has been built, but the left side is not usable:

- ROW0-ROW3 are not connected to the MCU
- missing trace between CONN_TX test pad and the side USB recepticle's TX line

The right side can be put to work, with a single design flaw:

- The eFuse is always disabled. As a solution, put a 1 MΩ resistor (I've used a 0805 package, but probably a 0603 would be better) between pin 1 and pin 2 of Q1 MOSFET.

In general, LED silk screen markings were unreadable, and the ones I've purchased had different pin numbering. I've placed them by following the traces instead.

As a minor detail, SMD encoders' holes are a bit too tight, a 0.1mm clearance is added. Some silkscreen markings were adjusted for readability and visibility.

Version v1.1: only left side has been ordered, as there are no significant upgrades on the right side.

## Can I copy it?

I don't recommend any usage at this point. Copyright-wise I retain all rights for now, probably opening up later. You can watch, you can learn, and you can laugh at my failures though.

The original design is originated by ZSA Technology Labs, Inc. I can't stop being gratituous enough for all the things they've done.
