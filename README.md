# OSC2Midi

ESP8266 based OSC <-> Midi wireless bridge.

It is mostly meant to be used with [TouchOSC][1] but it will work with
any [OSC message source][2].

## Library dependencies

Project uses:
  * https://github.com/FortySevenEffects/arduino_midi_library/
  * https://github.com/CNMAT/OSC

## Hardware

Based on a generic ESP8266-12f board and the following guides to hook
up ESP8266 and do MIDI i/o:

  * [MIDI Input][4]
  * [MIDI Output][3]

Midi I/O uses [SoftwareSerial][5] mostly to allow debug logging via
primary serial port.

## Schematic

Note! Do checkout the KiCad project instead. Image below is for quick preview only.

![ESP8266 OSC to MIDI](esp8266-osc-to-midi.png)

## Flashing firmware

To flash the firmware I'm using FTDI cable with [flash+reset circuit][8].

## Hardware ideas / roadmap / TODO

  * Find a reasonable enclosure and adapt layout to it.
  * [MCP73833][7] based battery charging circuit + microusb input for power.
  * Maaaaybe i2c screen.

## OSC message formats

All messages are expected to have payload of 1 or 2 floats with range
from 0 to 127.

### /midi/cc/{cc} + 1 float

Will send control change message for `{cc}` number.

### /midi/cc/{ccA}/{ccB}/.../{index} + 1 float

Will send control change message for CC specified by `{index}`. For
example:

  * /midi/cc/10/12/15/1 -> CC to 10
  * /midi/cc/10/12/15/3 -> CC to 15

This is meant to be used with TouchOSC groups of faders. For example,
my [MicroKORG][6] preset includes a fader group of 4 to control
amp ADSR: `/midi/cc/73/75/70/72`

### /midi/cc/{ccA}/{ccB} + 2 floats

This sends two control change messages to `{ccA}` and `{ccB}`. This is
meant to be used with TouchOSC XY pads.

## Current prototype

Rather crude build, but it works:

![ESP8266 OSC to MIDI](1.jpg)

![ESP8266 OSC to MIDI](2.jpg)

![ESP8266 OSC to MIDI](3.jpg)

## Hello people of the future

So it seems GitHub is about to take a snapshot of active open source repositories
and put it into cold storage that should last 1000 years. Hence this section:
a change for the sake of it. Exact criteria is not clear, but hope this
repository makes it to the archive.

[1]: http://hexler.net/software/touchosc
[2]: https://en.wikipedia.org/wiki/Open_Sound_Control
[3]: https://www.arduino.cc/en/Tutorial/Midi
[4]: http://libremusicproduction.com/tutorials/arduino-and-midi-in
[5]: https://www.arduino.cc/en/Reference/SoftwareSerial
[6]: http://www.korg.com/us/products/synthesizers/microkorg/
[7]: https://www.microchip.com/wwwproducts/en/en027785
[8]: https://github.com/tadas-s/esp8266-autoreset
