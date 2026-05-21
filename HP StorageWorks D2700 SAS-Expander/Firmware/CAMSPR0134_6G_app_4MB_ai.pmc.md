
# Firmware für ein HP D2700 SAS Expander (v134)

* 0x00 - 0x4F: Header
* 0x50 - 0x11CF: binary image
* 0x11D0 - 0x145F: array data
* 0x1460 - 0x164F: repetitive data chunks
* 0x1650 - : less repetitive but still repetitive data
* zeroes
* 0x1EB496: 6 trailing non-zero bytes; probably checksum (CRC?)

## Vermutungen

* kombiniertes Image, das die Firmware mehrere Prozessoren enthält

Hinweise in den strings:

## HMP

Der Host Management Processor ist vermutlich der erste, der beim Einschalten läuft.

~~~
ps_twi.c
~~~

Er verteilt vermutlich die übrigen Images per SPI/TWI/I2C o.ä. an die anderen Controller und startet sie.

## PSoC

* Cypress PSoC
* oft für analoge Sensorik und GPIO-Steuerung verwendet

~~~
psoc.c
~~~

* könnte z.B. Temperaturen messen, Lüfter, LEDs und andere Anzeigen steuern (7-Segment-Anzeige?)

## PIC

~~~
hmpic.c
~~~

* evtl. Watchdog- oder Hot Plug-Controller

## SAS-Expander ASIC

~~~
sxp6g/src/sxp/sxp.c
MIPSRDY TIMER
SES
~~~

* MIPS-basierter Hauptprozessor
* verantwortlich für den SAS-Datenpfad, Link-Management, Routing, SES-Kommunikation etc.



