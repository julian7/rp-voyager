# Journal

The local supplier doesn't have everything in stock, so I ordered the main components from Mouser. I've ordered some of the components from Aliexpress.

I've made the first release, tagged as v1.0. I've ordered 5 prototype boards from JLCPCB, with stencils.  All the components arrived. The stencil made the PCB ordering way harder, as it was held back at customs for a week, as it was missing sanction declaration.

I've placed the bottom components of the left side, with some findings:

- The bulk cap (220 µF) has a 6.3V rating, which might be a bit problematic on the 5V rail. I've replaced that with a 10V-rated one, but I decided it will still do some good work on the LED circuit.
- Markings for the poly bulk cap is unipolar, but it is a polarized capacitor. It also caused a short, as it was placed anode side to GND.
- The crystal is taking a huge chunk of real estate, that could be smaller.
- Minor nuissance, ROW0-ROW3 are not connected to the MCU, leaving the majority of the keys unusable on the left side.

I now continue with some LEDs and making a right side, so that I can find more issues before placing a second order for PCBs.
