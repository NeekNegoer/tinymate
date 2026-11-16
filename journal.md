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

**Next step:**
