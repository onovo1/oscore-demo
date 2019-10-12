# [WIP] oscore-demo

This will hopefully turn into a demonstration of protecting CoAP with OSCORE on
embedded devices some day.
At the moment, this is built specifically for the STM32F303VCT6 (server) and
STM32F407VGT6U (client).

## Dependencies

To build this you'll need (in your nightly toolchain):

- `rust-std` components (pre-compiled `core` crate) for the ARM Cortex-M
  target. Run:

```console
$ rustup target add thumbv7em-none-eabihf
```

## Hardware setup
This is the wiring:
```
ENC28J60    STM32F303/407
--------    -------------
VCC         3V
GND         GND
MISO        PB4
MOSI        PB5
SCK         PB3
CS          PA15
```

To use USART instead of Ethernet (pass `--features usart` to `cargo run`):
```
STM32F303   STM32F407
---------   ---------
PD5 (TX)    PD6 (RX)
PD6 (RX)    PD5 (TX)
GND         GND
```

And for getting serial debug output (using the SparkFun FTDI Basic Breakout as
USB to Serial IC):
```
FTDI        STM32F303/407
----        -------------
GND         GND
RXI         PB6
```

## Building
We're using minicom for serial output, so you need to create `.minirc.dfl` in
your home with this configuration:
```
pu baudrate 115200
pu bits 8
pu parity N
pu stopbits 1
pu rtscts No
pu xonxoff No
pu linewrap Yes
```
To exit minicom, use <kbd>CTRL</kbd>+<kbd>A</kbd>+<kbd>X</kbd>.

Use OpenOCD to connect to the board
```console
$ openocd -f interface/stlink-v2-1.cfg -f target/stm32f3x.cfg   # For the F303
$ openocd -f interface/stlink-v2-1.cfg -f target/stm32f4x.cfg   # For the F407
```
In a different terminal, open minicom to see serial output
```console
$ minicom -D /dev/ttyUSB0
```
In yet another terminal, build and enter GDB. We're using the release flag
since the debug build might be too large for the flash memory.
```console
$ cargo run --release
```
This will break at the main function, so you need to
```console
(gdb) continue
```

## License
Licensed under either of

 * [Apache License, Version 2.0](LICENSE-APACHE)
 * [MIT license](LICENSE-MIT)

at your option.

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the Apache-2.0 license, shall
be dual licensed as above, without any additional terms or conditions.
