# Multiplex PPM Format

This document is a specification of the Multiplex PPM format. It is used for RC radio transmitters to represent channel values in a pulse-width modulated form and to transmit it to the receiver.

This specification was derived from a PPM signal as generated by a Multiplex Profi mc3030 radio.

## Overview

A full PPM frame consists of a SYNC pause, followed by N pulses representing the channel values CHx.

```spec
SYNC|CH1|CH2|CH3|CH4|CH5|CH6|CH7|CH8|CH9
```

## PPM Signal

A PPM signal looks like this:

```spec
+      +-------+      +-----------+      +-- // --+      +---------+      +-----------------+
|      |       |      |           |      |   //   |      |         |      |                 |
+------+       +------+           +------+   //   +------+         +------+                 +
|<-TL->|       |<-TL->|           |          //   |<-TL->|         |<-TL->|                 |
|<----TP0----->|<-------TP1------>|          //   |<-----TPn------>|<--------TPsync-------->|
```

The frame starts with the first falling edge after the sync pulse TPsync. The channel values are represented by a series of low-pulses. All channel values have a fixed-width low-state which is TL=375µs long, followed by a variable-length high-state. The channel values are encoded by the width of the period TPx (i.e. the time between two falling edges), depicted as TP0, TP1, ..., TPn.

The width of the sync pulse TPsync is adjusted so that the total length of a PPM frame is 25ms. Common number of channels are seven (PPM7) and nine (PPM9).

## PPM timing (Multiplex-Uni Format)

The table below shows the PPM timing used by current Multiplex radios.

Value | TPx [µs]
------|---------
  MIN |  800
-110% |  895
-100% |  950
   0% | 1500
+100% | 2050
+110% | 2105
  MAX | 2200

## PPM timing (Old Multiplex Format)

The table below shows the old PPM timing used by older Multiplex radios, such as the Profi mc3030. It is identical to the Multiplex-Uni Format, except that TPx is offset by 100µs.

Value | TPx [µs]
------|---------
-110% |  995
-100% | 1050
   0% | 1600
+100% | 2150
+110% | 2205

## Disclaimer

All product and company names are trademarks or registered trademarks of their respective holders. Use of them does not imply any affiliation with or endorsement by them. The author is not affiliated with Multiplex.

## License

[GNU GPLv3](./LICENSE)

Copyright (C) 2018 Marius Greuel
