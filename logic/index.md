[gadget-doc](/README.md) / [logic](/logic/index.md)

Logic Analyser
==============

This page is a placeholder, containing details of the planned logic analyser
implementation on Gadget. A cheap, high-speed logic analyser was initially the
primary goal of the project, however it seemed foolish to focus on this when a
much more useful tool could be built more quickly by focussing on other areas.

The basic plan is to combine some form of data acquisition driver for the
Raspbery Pi GPIOs, and to couple this with [sigrok](http://sigrok.org/) for
processing.

sigrok
------

From the project page: "*The sigrok project aims at creating a portable,
cross-platform, Free/Libre/Open-Source signal analysis software suite that
supports various device types (e.g. logic analyzers, oscilloscopes, and many
more).*"

Effectively, sigrok provides a powerful front-end for logic analysers and other
data acquisition equipment. Importantly, the data acquisition is completely
decoupled from the data analysis.

sigrok has support for decoding and viewing different data streams - for
instance it understands i2c, SPI, UART, JTAG, SPDIF and so on (for more
information see [Protocol Decoders](http://sigrok.org/wiki/Protocol_decoders)).
What this means, is if there is a way to capture data in a format that sigrok
understands, then Gadget automatically gets support for protocol sniffing of all
of the protocols detailed on that page (61 protocols at the time of writing!).

The intention would be to provide [`sigrok-cli`](http://sigrok.org/wiki/Sigrok-cli)
on-board, and some form of network interface for running more rich applications
such as [PulseView](http://sigrok.org/wiki/PulseView) on the host.

Linux iio
---------

The [Linux Industrial IO subsystem](https://wiki.analog.com/software/linux/docs/iio/iio)
is intended for all input (or output) devices which don't fit in the `input`
subsystem (which is intended for human interface devices, such as keyboards,
mice and the like). Whilst there is currently no precedent for a "logic
analyser"-style device in `iio` I think it's a good fit.
`iio` provides DMA buffer handling and a well-defined userspace interface for
handling data acquisition. There is a userspace library -
[`libiio`](https://wiki.analog.com/resources/tools-software/linux-software/libiio)
which can be used to interact with `iio` devices, and it also has a daemon for
communicating with `iio` devices over the network (perfect for Gadget).

There is currently no merged generic `iio` driver for sigrok, however there are
murmurs on the [mailing list](https://sourceforge.net/p/sigrok/mailman/message/34728951/),
which indicates there is at-least interest, and some code to start with.

Raspberry Pi GPIO + DMA
-----------------------

The other part of the puzzle is actually getting the data from the pins into
RAM. Of course the GPIO pins can be mapped into userspace, and polled. This is
already used by a number of libraries/tools and seems to give a max sample rate
of around 1 MHz.

The DMA engine on the Pi can read from the GPIOs, but there is no simple way to
control the sample rate, and also jitter may be an issue.
Without further investigation, it's hard to determine how feasible this is. It's
been discussed before in the Raspberry Pi forums amongst other places, but
no-one seems to have made any significant progress.

Some cursory tests involving reading the timer using DMA gave a sample rate of
around 17 MHz, which is respectable but not lightning fast.
