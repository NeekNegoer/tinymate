# TinyMate — Journal

Format: date · time spent · what I did · decisions · problems · screenshots.
(Write each entry in your own words.)

---

## 2026-11-16 · 17:15–18:15 · 1h

**Research:** I spent the first part of this session researching Hack Club programs
and the 8-Pin Grant rules, and exploring project ideas that would fit them.
I landed on a smart chessboard that detects the pieces and plays online.

**Decision:** the ATtiny412 only has 8 pins (5 usable, after power and programming),
and with my mental sketch I needed 16 to read all 64 squares as an 8×8 matrix,
plus 2 for communication. So I added an MCP23017, which gives me 16 extra pins
over I2C using just 2 of the ATtiny's.

**Learned:**
- A tiny MCU like the ATtiny412 runs out of pins fast: after power, ground and the
  UPDI programming pin, only 5 are left for the actual project.
- You can get around that with I/O expanders like the MCP23017, which talks over
  I2C and adds 16 pins while using only 2 of the MCU's. The 8-Pin Grant allows one
  expander per board, so it fits the rules.
- How the journal works and how it compares to commits: commits show *what* changed
  in the files, the journal shows *why*, what I tried and how long it took.

**Next step:** build the parts list on DigiKey and start the schematic in KiCad.

---

## 2026-11-16 · 18:15–20:45 · ~2h20 (7 min break)

**What I did:** built the parts list on DigiKey (~$9 total, all in stock), then my
first ever KiCad project: full schematic (ATtiny412, MCP23017, pull-ups, status LED,
decoupling caps, 3 connectors), passed ERC with 0 errors / 0 warnings, assigned
footprints, placed everything on the PCB and drew a 42.5 × 33 mm board outline.

![Schematic](images/2026-11-16-schematic.png)

**Liked:** that KiCad has generic symbols for everything, and that you only pick the
physical footprint later. The 3D view is awesome, and shoutout to the PCB editor's
dark mode: it has a great style and makes long sessions way easier on the eyes. I only
wish the schematic editor came with a dark theme by default too (turns out you can
install one through the Plugin and Content Manager).

**Problems:**
- The 10µF capacitor I picked was out of stock, so I had to find a substitute.
- The LED was placed backwards, and R3 was wired so the current skipped it.
- I chose the wrong footprint for J1/J2 (a fan connector instead of a plain pin
  header). Footprints come in many variants and it's easy to pick the wrong one.
- I got completely lost placing the components on the PCB, with everything stacked
  on top of each other. I fixed it by separating everything first and then grouping
  parts by function (ATtiny side, MCP23017 in the middle, chess matrix connector on the right).

![PCB 3D view](images/2026-11-16-pcb-3d-top.png)

**Learned:** basically everything, since I had never used KiCad before: schematic →
footprints → PCB, net labels, PWR_FLAG for ERC, reading the ratsnest, and keeping
courtyards at least 1 mm from the board edge.

**Next step:** route the traces, add a ground plane and run DRC.
