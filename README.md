
## Summary

This project is an SOC (System on a Chip) coded in VHDL and implemented for the Lattice iCE40-hx8k dev board. The SOC contains the following components: 65(c)02 CPU + UART + Timer + I/O Ports

## Required Hardware

* Lattice iCE40-hx8k dev board (can be ordered online at www.latticesemi.com)
* USB-to-Serial 3.3V adapter (can be ordered from eBay)
* misc USB cables and wires for connecting the USB-to-Serial adapter

NOTE: Make sure the USB-to-serial adapter is a 3.3V version. Some adapters have 5V interface signals which could damage your iCE40-hx8k dev board.

## Tools

* IceCube2 (from Lattice Semiconductor) was used for synthesis and FPGA Routing.
* Icestorm (https:/github.com/cliffordwolf/icestorm) was used for programming.


## Build Flow

I used the Lattice IceCube2 software to generate the SOC_bitmap.bin programming file and then I used this command line "iceprog SOC_bitmap.bin" the program the iCE40-hx8k dev board over the USB cable (iceprog is part of the icestorm tool suite).

## Console Interface

I used the minicom program (on Ubuntu Linux) as a console to communicate with the 6502 SOC over the USB-to-Serial connection. Configure minicom using the command line "minicom -s" to configure the serial port for ttyUSB0 and turn of the hardware handshaking. There are probably other alternatives to minicom. Any ANSI terminal-emulator program should work for this application.

## Pinout

The iCE40 pins are defined as follows:
```
UART_RXD   G1 -pullup yes
UART_TXD   G2
PORTA[0]   B5
PORTA[1]   B4
PORTA[2]   A2
PORTA[3]   A1
PORTA[4]   C5
PORTA[5]   C4
PORTA[6]   B3
PORTA[7]   C3
RESET      N3 -pullup yes
CLK        J3 -pullup yes
```

## Memory Map

The memory map of this SOC is as follows:
```
$0000 -> $00FF  Zero Page RAM (256-bytes)
$0100 -> $01FF  Stack RAM (256-bytes)
$0200 -> $0207  UART registers
$0208 -> $020B  Timer registers
$020C           Output port register
$020D           Interrupt mask register
$020E -> $020F  Random number registers
$0210           Interrupt source register
$F000 -> $FFFF  Boot RAM (4k-bytes)
```

## 6502 CPU Background Info

The 6502 was a highly successful 8-bit microprocessor design first introduced in 1975 by MOS Technology. The 6502 has ties to the Motorola 6800 as key members of the 6800 design team formed the core of the 6502 design team. The strength of the 6502 architecture lies in its small size and simple instruction set, coupled with flexible addressing modes. When it was introduced, the 6502 was much cheaper than its competitors and as a result the 6502 was designed into many early computers and game consoles including the first Apple computers.

NOTE: This SOC implements the 65C02 intruction set, but I generically I refer to it here as 6502.


## Contributors

* Scott L Baker - SOC design

## License

See the **LICENSE** file in this repository
