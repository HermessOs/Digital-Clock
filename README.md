# Digital-Clock
A digital clock circuit i designed and simulated in Logisim Evolution. The design supports both 12-hour and 24-hour time formats, with the ability to toggle between modes during operation.

## Circuit Overview

![Full Clock](Full%20Clock.png)

### Seconds & Minutes
The seconds and minutes displays are each driven by two (T Flip Flop) cascaded BCD counters:
- **MOD-9 counter** — drives the units digit (0–9)
- **MOD-6 counter** — drives the tens digit (0–5), incrementing on each units rollover

Together, these produce a standard `00`–`59` count.

### Hours
The hours stage uses two separate counter pairs, one for each display mode, since the reset condition differs between them:
- **24-hour mode:** MOD-2 (tens) and MOD-9 (units), resetting to `00` upon reaching `24`
- **12-hour mode:** MOD-2 (tens) and MOD-9 (units), resetting to `00` upon reaching `12`

### Mode Switching
The tens and units digits of the hours display are each routed through a 2-to-1 multiplexer, selecting between the 12-hour and 24-hour counter outputs. Both multiplexers share a single select line, driven by a T flip-flop that toggles on each button press — switching the display format instantly without disrupting timekeeping.

![Zoomed Hour Controller](Zoomed%20Hour%20Controller.png)

### Output Display
Each counter's BCD output is fed into a hex (7-segment) display decoder, converting the count into a human-readable digit on the corresponding display.

### Manual Time Setting
Dedicated push buttons allow the hours and minutes to be set independently.
