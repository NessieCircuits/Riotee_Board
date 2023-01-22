# Riotee Board Hardware Design Files

[![Kibot ERC/DRC](https://github.com/NessieCircuits/Riotee_Board/actions/workflows/test.yml/badge.svg)](https://github.com/NessieCircuits/Riotee_Board/actions/workflows/test.yml)

The Riotee board is a development board for battery-free wireless devices. The on-board wireless microcontroller runs off energy harvested from, for example, a solar panel and uses only tiny capacitors as energy storage. For uploading new software, the board can be connected to a PC via USB. During sotware upload and debugging, the microcontroller is powered with a fixed supply voltage from USB. After programming, the board automatically switches over to untethered, battery-free operation.

Latest design files:
 - [Schematics](https://www.riotee.nessie-circuits.de/artifacts/board/latest/schematics.pdf)
 - [Layout](https://www.riotee.nessie-circuits.de/artifacts/board/latest/pcb.pdf)
 - [3D rendering](https://www.riotee.nessie-circuits.de/artifacts/board/latest/3drendering.png)

## Specification

![3D rendering](https://www.riotee.nessie-circuits.de/artifacts/board/latest/3drendering.png)

Essentially, the Riotee board combines a [Riotee probe](https://github.com/NessieCircuits/Riotee_ProbeHardware) and a Riotee module on a single board. The board has two 0.1" pin sockets that expose all relevant signals from the battery-free device, including 10 GPIOs that can be flexibly used for I2C, SPI or for reading analog sensors. These headers are also used to connect riotee shields to build fully featured devices without having to design custom PCBs. The board comes with a push button, an LED and a connector for a solar panel.

Specification:
 - 56mm x 23mm board with two expansion headers for shields
 - Boost converter with software-defined maximum power point tracking and energy measurement
 - 44uF on-board capacitance
 - 2V regulated output voltage
 - 64 MHz ARM Cortex-M4 MCU with integrated 2.4GHz radio
 - 128kB non-volatile FRAM to retain appliccation state across power outages
 - Ultra-low power RTC with power management functionality
 - Capacitor voltage sensing and ultra low power comparator with software-controlled thresholds
 - USB-C connector
 - CMSIS-DAP compatible: Supports programming via pyOCD and OpenOCD
 - Makes UART output from battery-free device available via USB
 - Push button and User LED

## Firmware

The board has a dedicated controller (Raspberry Pi RP2040) that manages the upload of new firmware and the communication with a PC. This controller is powered from USB whenever the board is connected to a PC. The software running on the controller is the same as on the [Riotee probe](https://github.com/NessieCircuits/Riotee_ProbeHardware) and can be found in [this repository](https://github.com/NessieCircuits/Riotee_ProbeFirmware). To upgrade the firmware on the controller, connect a wire from one of the ground pins to the test pad labelled 'USB_BOOT' on the bottom of the board, while plugging in the USB cable. A removable storage drive should appear on your PC. Drop a UF2 compatible binary into the drive.