# Bus Interface (V1 → V2)

<img src="BusInterfaceV2_2/S3-BusInterface%20Large.png" width="480" alt="Bus Interface V2.1 – assembled">

**Context:** Ecogenium student team (hydrogen vehicle, Shell Eco-marathon) · **Tools:** KiCad 7 (V1), Altium Designer (V2)
**Timeline:** V1.0 12/2022 → V1.2 03/2023 → V2.1 12/2023 → V2.2 10/2024
<!-- TODO: confirm/adjust your role -->
**My role:** Concept, schematic, layout and bring-up of both generations
**Documentation:** [V1 schematic (PDF)](BusInterfaceV1/Schematic.pdf) · [V2.2 schematic & layout (PDF)](BusInterfaceV2_2/BusInterface.pdf)

## What it does

The Bus Interface is the standard controller node of the vehicle's electronics. Every subsystem
board (power distribution, DC/DC, fuel cell controller, main controller, …) carries a Bus Interface
on a common pin header. The Bus Interface provides the microcontroller, the power rails, the CAN
connection and the measurement of the 12 V supply, so each application board only has to implement
its own function.

## V1 – Raspberry Pi Pico carrier (KiCad)

<img src="BusInterfaceV1/S2-BusInterface%20Large.png" width="480" alt="Bus Interface V1.2 – assembled">

- **MCU:** Raspberry Pi Pico (RP2040) as a plug-in module
- **CAN:** MCP2515 controller + MCP2562 transceiver, switchable 120 Ω termination, CAN in/out connectors for daisy-chaining
- **Analog:** MCP3208 12-bit / 8-channel SPI ADC with an LM4040 3 V reference
- **Power:** MP1584 buck converter (12 V → 5 V, 3 A), 12 V pass-through outputs
- **Current measurement:** shunt + INA281 current-sense amplifier on the 12 V output
- **Bus connector:** 2×12 pin header carrying SPI, UART, I²C, 8 ADC channels and 12 V / 5 V / 3.3 V

## V2 – Chip-down RP2040 redesign (Altium)

The second generation replaces the plug-in Pico with a discrete RP2040 design and moves from KiCad
to Altium. This reduced the size drastically, so the Bus Interface now plugs onto any other board
without taking up much space. For this, the pinout of the bus connector was redesigned (2×14) and
new features were added: **CAN FD** (MCP2518FD), Würth MagI³C power modules, a digital current
monitor (INA219), a temperature sensor and USB-C.
