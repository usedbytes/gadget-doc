[gadget-doc](/README.md)

# Gadget Documentation Project

Welcome to the Gadget documentation project. Though this is intended
to be used in conjunction with a board running Gadget, it may also be
useful as a generic resource for hackers working on linux.

This documentation is all available locally on Gadget, and can be
accessed via HTTP on port 80 of the ethernet interface.

If your Gadget is using the default setup, go here: http://192.168.3.142/

## Already have Gadget?

[Check out Getting Started](/getting-started/index.md)

## Want to get gadget?

[Visit the main project page](/dev/null)

## What's Gadget?

Gadget is an attempt to make a useful hacker's toolkit out of
commodity linux development boards (think
[Bus Pirate](http://dangerousprototypes.com/docs/Bus_Pirate), but
using linux instead of a PIC). It's a combination of software and
platform configuration aimed at making it fast and simple to access
all of the interfacing capabilities of your board.

Right now, it's only targeting the Raspberry Pi (specifically the
Zero), but as it's "just linux" it should be easily applicable to any
other linux platform. If you want to help out with adding support for
other platforms, then jump in!

## Why 'Gadget'?

The Raspberry Pi Zero has support for the [USB Gadget
subsystem](https://lwn.net/Articles/395712/) of the linux kernel. This
is how Gadget works - you plug the Pi into your computer, and it
presents an ethernet device, a serial port and a mass storage device.
You then use these 3 devices in tandem to access the functionality of
Gadget.

## Features

Gadget is a work-in-progress, but it will hopefully be able to support
a large variety of digital protocols and features.

The table below provides a quick overview of some of the
protocols/features which it would be good to support (inspired by the
Bus Pirate), as well as the status/plan for Gadget.

Follow the links from this table to learn more about any particular
feature. In general, a tick (✓) means support is available and
verified, a cross (✗) means support is not available, and is currently
unplanned, and a question mark (❓) means support should be available
but may not have been tested or may be missing some features/tools.

|  Protocol                         | Gadget                                         |
|:----------------------------------|:-----------------------------------------------|
| [1-wire](/1-wire/index.md)        | ❓ w1-gpio driver. Need userspace tools         |
| [UART](uart/index.md)             | ✓ Supported                                    |
| MIDI                              | ✗ Unsure                                       |
| [i2c](i2c/index.md) Master        | ✓ Supported                                    |
| [i2c](i2c/index.md) Address scan  | ✓ Supported                                    |
| [i2c](i2c/index.md) Sniffing      | ✗ Future. See [Logic Analyser](logic/index.md) |
| [SPI](spi/index.md) Master        | ✓ Supported                                    |
| [SPI](spi/index.md) Sniffing      | ✗ Future. See [Logic Analyser](logic/index.md) |
| raw 2-/3-wire                     | ❓ GPIO + Python                                |
| [JTAG](jtag/index.md)             | ❓ Supported (openOCD, untested)                |
| [AVR ISP](avrisp/index.md)        | ✓ Supported                                    |
| [flashrom](flashrom/index.md)     | ❓ Supported (untested)                         |
| [Oscilloscope](piscope/index.md)  | ❓ Digital only                                 |
| [Logic analyser](logic/index.md)  | ✗ Future. (sigrok)                             |

## Developers

For all matters related to the internals of Gadget, or how you can
help, check out the [Developers](/developers/index.md) page.
