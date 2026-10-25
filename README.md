# 5-LED-Knight-Rider-Circuit-Tutorial-555-Timer-CD4017-Step-by-Step
Reviewed of Your Knight Rider 555 + CD4017 Wiring

5-LED Knight Rider – Corrected Full Wiring (No Transistors)
TIMESTAMPS / CHAPTERS
0:00 – Intro
0:20 – Parts you need
0:45 – 555 timer wiring (the clock)
1:35 – Potentiometer wiring (speed control)
2:10 – CD4017 wiring (the counter)
2:50 – LED wiring
3:20 – Power up & test
3:45 – Troubleshooting tips
4:10 – Outro
PARTS LIST
1× NE555 timer IC

1× CD4017 decade counter IC

1× 10 kΩ resistor

1× 10 kΩ potentiometer (linear)

1× 1 kΩ resistor (series protection for pot — recommended)

1× 10 µF electrolytic capacitor (timing)

1× 0.01 µF ceramic capacitor (555 pin 5)

1× 0.1 µF ceramic capacitor (4017 decoupling — recommended)

5× LEDs

5× 220 Ω resistors

5 V–9 V power supply

Breadboard + jumper wires

1) 555 TIMER (ASTABLE CLOCK)
text
• Pin 1  → GND
• Pin 2  → tied to Pin 6
• Pin 3  → CD4017 Pin 14 (clock)
• Pin 4  → VCC
• Pin 5  → 0.01 µF → GND
• Pin 6  → tied to Pin 2 → 10 µF capacitor (+) → GND
• Pin 7  → junction of 10 kΩ resistor (to VCC) and pot Pin 1
• Pin 8  → VCC
Timing / speed control network
text
VCC ── 10 kΩ ──┬── 555 Pin 7
               │
               └── 1 kΩ ── POT Pin 1
                            POT Pin 2 (wiper) ── 555 Pins 2 & 6
                            POT Pin 3 ── NOT CONNECTED 
555 Pins 2 & 6 ── 10 µF (+) ── GND
The 10 kΩ sets the minimum charge resistance.

The 1 kΩ protects the 555 discharge transistor when the pot is at zero.

The pot varies the scan speed — turning it changes how fast the LEDs chase.

The 10 µF sets the timing range; swap to 4.7 µF for faster, 47 µF for slower.

Note: This arrangement does not give a 50 % duty cycle (charge path = 10 k + 1 k + R_pot, discharge path = 1 k + R_pot). That's normal and fine for driving a CD4017 — the counter only needs clean clock pulses.

2) CD4017 CONNECTIONS
text
• Pin 16 → VCC
• Pin 8  → GND
• Pin 13 → GND          (clock enable — active low)
• Pin 14 ← 555 Pin 3    (clock input)
• Pin 15 ← Q5 (Pin 1)   (reset after 5 LEDs)
• 0.1 µF ceramic across Pin 16 → GND (decoupling, recommended)
3) LED WIRING
Output	4017 Pin	LED	Resistor
Q0	Pin 3	LED1	220 Ω
Q1	Pin 2	LED2	220 Ω
Q2	Pin 4	LED3	220 Ω
Q3	Pin 7	LED4	220 Ω
Q4	Pin 10	LED5	220 Ω
text
4017 output ── 220 Ω ── LED anode (long leg)
LED cathode (short leg) ── GND
4) POTENTIOMETER — CORRECT WIRING
A potentiometer has 3 pins:

• Pin 1 (left leg)
• Pin 2 (center wiper)
• Pin 3 (right leg)
Variable Resistor Mode (correct for speed control):

POT Pin 1 (left)   → 1 kΩ → 555 Pin 7
POT Pin 2 (wiper)  → 555 Pins 2 & 6 (tied together)
POT Pin 3 (right)  → NOT CONNECTED (leave empty)
Complete speed-control network:

VCC ── 10 kΩ ──┬── 555 Pin 7
               │
               └── 1 kΩ ── POT Pin 1
                            POT Pin 2 (wiper) ── 555 Pins 2 & 6
                            POT Pin 3 ── (open)

555 Pins 2 & 6 ── 10 µF (+) ── GND
5) COMPLETE SCHEMATIC (ASCII)

                    VCC
                     │
              ┌──────┴──────┐
              │             │
            10 kΩ          Pin 4 ── 555
              │             Pin 8 ── 555
              │             │
    ┌─────────┴─────────┐   │
    │                   │   │
  Pin 7 ── 555      1 kΩ   │
    │                   │   │
    │                 POT 1 │
    │                 POT 2 ──┬── Pins 2 & 6 ── 555
    │                 POT 3   │        │
    │                (open)   │      10 µF
    │                         │        │
    │                        GND      GND
    │
  Pin 3 ── 555 ── Pin 14 ── CD4017
                              │
                    ┌─────────┼─────────┐
                    │         │         │
                  Pin 16    Pin 8     Pin 13
                   VCC      GND       GND
                    │
                  0.1 µF
                    │
                   GND

  CD4017 Outputs:
  Q0 (Pin 3)  ── 220Ω ── LED1 ── GND
  Q1 (Pin 2)  ── 220Ω ── LED2 ── GND
  Q2 (Pin 4)  ── 220Ω ── LED3 ── GND
  Q3 (Pin 7)  ── 220Ω ── LED4 ── GND
  Q4 (Pin 10) ── 220Ω ── LED5 ── GND
  Q5 (Pin 1)  ── Pin 15 (reset)
6) POWER UP & TEST
Double-check all VCC and GND connections before applying power.

Verify the 10 µF capacitor polarity — + to Pins 2 & 6, – to GND.

Apply 5 V–9 V. LED1 should light first, then the sequence should chase LED1 → LED5 and repeat.

Turn the pot — the chase speed should change smoothly.

If nothing happens, check the 555 output (Pin 3) with a multimeter or LED+resistor — it should toggle.

7) TROUBLESHOOTING TIPS
Symptom	Likely cause
No LEDs light	Power not connected, or 555 not oscillating (check Pin 3)
Only one LED stays on	555 not clocking — check pot/10 k/10 µF network
LEDs chase but don't reset	Pin 15 not connected to Q5 (Pin 1)
All LEDs on at once	Pin 13 not grounded, or missing GND on 4017 Pin 8
Speed doesn't change	Pot wiper not connected to Pins 2 & 6, or pot Pin 3 accidentally tied to something
Erratic / flickering	Missing 0.01 µF on Pin 5 or 0.1 µF decoupling on 4017; check breadboard contacts
555 gets hot	Pin 4 or Pin 8 reversed, or output shorted
