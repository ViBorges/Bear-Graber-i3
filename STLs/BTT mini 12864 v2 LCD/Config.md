This post helped to adopt screen to board quickly and painless, huge thanks!



I was a bit confused by pins naming, so decided to post pins mappings as they called in official diagrams of boards (and not adapter diagram).



\- SKR Mini E3 v3 diagram: https://github.com/bigtreetech/BIGTREETECH-SKR-mini-E3/blob/master/hardware/BTT%20SKR%20MINI%20E3%20V3.0/Hardware/BTT%20E3%20SKR%20MINI%20V3.0\_PIN.pdf

\- Mini 12864 diagram: https://github.com/bigtreetech/MINI-12864/blob/master/mini12864\_v2.0/Hardware/MINI12864%20V2.0-Pin.png



Pins mapping:



| SKR Mini E3 v3 pin (PORT: pin)  | Mini 12864 pin (PORT: pin) |

| ------------- | ------------- |

| EX1: PB5  | EXP1: BTN  |

| EX1: TX1  | EXP2: ENCB  |

| EX1: RX1 | EXP2: ENCA  |

| EX1: PB8 | EXP1: LCD-EN  |

| EX1: GND | EXP1: GND  |

| EX1: PA15 | EXP1: D5 |

| EX1: RST | EXP2: RST |

| EX1: PD6 | EXP1: LCD-CS |

| EX1: 5v | EXP1: 5v |

| SPI1: MOSI | EXP2: SD-MOSI  |

| SPI1: CLK | EXP2: SD-SCK  |

| SPI1: MISO | EXP2: SD-MISO |



My printer based on Ender 3v2 with Klipper software so I didn't need to do pin swap, I did it but then default config from Voron made my wheel direction opposite, so I had to adjust config, instead just do not swap PA9 and PA10 for Klipper setup:



> Change PA9 ---- PA9 PA10 ---- PA10 to PA10 ---- PA9 PA9 ---- PA10 to get correct encoder direction, otherwise you'll have to uncomment this in configuration.h //#define REVERSE\_ENCODER\_DIRECTION



In case you did swap PA9 and PA10, change order of those pins:

```

\[display]

encoder\_pins: ^PA10, ^PA9

```



Klipper config was taken as is from adapter page: \[SKR-Mini\_Screen\_Adaptor/SRK Mini E3 V3.0/ScreenBreakout.cfg](https://github.com/VoronDesign/Voron-Hardware/blob/master/SKR-Mini\_Screen\_Adaptor/SRK%20Mini%20E3%20V3.0/ScreenBreakout.cfg)



```

\[display]

\#    MKS Mini 12864 V3.0 Your display might have to haver connectors flipped. If the neopixels doesnt light up and you are 100% sure you have EXP1 connected to EXP1, try flipping the connector.

lcd\_type: uc1701

cs\_pin: PB8

a0\_pin: PD6

rst\_pin: PB9

encoder\_pins: ^PA9,^PA10

click\_pin: ^!PB5

contrast: 63

spi\_software\_sclk\_pin: PA5

spi\_software\_mosi\_pin: PA7

spi\_software\_miso\_pin: PA6



\[neopixel SKR\_screen]

pin: PA15

chain\_count: 3

initial\_RED: 0.4

initial\_GREEN: 0.05

initial\_BLUE: 0.0

color\_order: RGB



\[delayed\_gcode welcome]

initial\_duration: .1

gcode:

&#x09;SET\_LED LED=SKR\_screen RED=0.5 GREEN=0.0 BLUE=0.0 TRANSMIT=0

&#x09;SET\_LED LED=SKR\_screen RED=0.0 GREEN=0.0 BLUE=0.5 INDEX=1 TRANSMIT=1

```





Good luck people!





