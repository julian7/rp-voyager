# Journal

The local supplier doesn't have everything in stock, so I ordered the main components from Mouser. I've ordered some of the components from Aliexpress.

I've made the first release, tagged as v1.0. I've ordered 5 prototype boards from JLCPCB, with stencils.  All the components arrived. The stencil made the PCB ordering way harder, as it was held back at customs for a week, as it was missing sanction declaration.

I've placed the bottom components of the left side, with some findings:

- The bulk cap (220 µF) has a 6.3V rating, which might be a bit problematic on the 5V rail. I've replaced that with a 10V-rated one, but I decided it will still do some good work on the LED circuit.
- Markings for the poly bulk cap is unipolar, but it is a polarized capacitor. It also caused a short, as it was placed anode side to GND.
- The crystal is taking a huge chunk of real estate, that could be smaller.
- Minor nuissance, ROW0-ROW3 are not connected to the MCU, leaving the majority of the keys unusable on the left side.
- There is a missing trace between CONN_TX test pad and the side USB recepticle's TX line in the design. For some reason, they are connected on the board I've received.

I now continue with some LEDs and making a right side, so that I can find more issues before placing a second order for PCBs.

---

Sep 30

I've built a right side, only bottom side. The board has some issues with the eFuse's EN signal. The board takes 0.037A if Q1 is off the board, that's a normal power consumption with no LEDs. Probably, Q1 gate needs a 1M pulldown resistor.

I want to test all three power scenarios on the right side: main only, side only, both. I'll use the PSU on main for the third scenario, I should measure 0A.

---

Oct 2

The right half started working well once I've installed a 1MΩ resistor between Q1's pin 1 and 2. The eFuse is disabled consistently when power also comes from UART USB.

I've installed a few LEDs, but they don't seem to be driven. The left side had a LED lighting bright blue for a moment, but it lasted only a second. I'll have to go back to the backlight once the more fundamental questions are solved.

I've updated the filler GPIO layouts, so that they are correctly connected. The keyboard matrix had some surprises too, as the right side's colums have been wired right to left. Apart from that, the right side is functioning well.

~~Apparently, sometimes the LEDs are working "somewhat", probably the first LEDs are broken but not completely dead.~~

Apparently, only one LED is burnt, the others had soldering issues.

---

Oct 3

Finished building the right side. All LEDs, all hotswap sockets, and the encoder works well through the UART connection from the left side.

At the same time, the first LED works on the left side, so we can conclude that only the left side PCB needs an update, the right one can be fixed with a 0603 resistor soldered on Q1's pins 1-2.

---

Oct 14

Left side PCB v1.1 arrived, components from faulty left side have been salvaged to the new version. Apart from the usual glitches during bring-up (there was a short under the MCU, but this time, D+ and D- were shorted under the main USB too), the system started working.

While testing the board, I noticed a key was not functioning (a diode has fallen off), and apparently, a Macbook Pro M1 doesn't deliver enough current for the LEDs in Swirl effect. Might need to set `CONFIG_ZMK_RGB_UNDERGLOW_BRT_MAX` to limit current taken, but at the same time, a port replicator has no such issue.

---

Oct 24

As per measurements, power consumption with Swirl effect is about 935 mA, which exceeds the available power of a USB-C port of a Macbook Pro.

Power consumption measurements:

| level | static red (mA) | Static peak (mA) | swirl (mA) |
| ----: | --------------: | ---------------: |  ---------: |
| 0 | 65 | 65 | 65 |
| 1 | 122 | 180 | 149 |
| 2 | 188 | 298 | 236 |
| 3 | 236 | 412 | 320 |
| 4 | 294 | 530 | 407 |
| 5 | 350 | 644 | 491 |
| 6 | 408 | 761 | 577 |
| 7 | 463 | 875 | 660 |
| 8 | 577 | 980 | 747 |
| 9 | 638 | 998 | 935 |

The best default brightness is 6, but I don't think the limit should be taken.
