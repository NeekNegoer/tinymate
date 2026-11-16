# TinyMate ♟️

**Eight Pin Gambit** — a smart chessboard that sees your pieces, powered by a single 8-pin ATtiny412.

> 🇧🇷 Um tabuleiro de xadrez inteligente que detecta as peças e joga online pelo Lichess, controlado por um microcontrolador de apenas 8 pinos.

Built for the [Hack Club 8-Pin Grant](https://8-pin-grant.hackclub.com/).

## How it works

```
[Phone/PC] ⇄ UART ⇄ [ATtiny412] ⇄ I2C ⇄ [MCP23017] ⇄ [8×8 reed switch matrix]
```

- Every piece has a small magnet in its base; every square has a reed switch (+ a 1N4148 diode to prevent ghosting).
- The ATtiny412 scans the 8×8 matrix through an MCP23017 I/O expander (8 rows out, 8 columns in) and reports occupied squares over UART.
- Software on the phone/PC compares board states to infer moves (from the starting position, including captures, castling and promotion) and plays them through the [Lichess Board API](https://lichess.org/api#tag/Board).

## ATtiny412 pinout

| Pin | Name | Use |
|---|---|---|
| 1 | VDD | 5 V |
| 2 | PA6 | UART TX |
| 3 | PA7 | UART RX |
| 4 | PA1 | I2C SDA |
| 5 | PA2 | I2C SCL |
| 6 | PA0 | UPDI (programming) |
| 7 | PA3 | Status LED |
| 8 | GND | Ground |

## Controller board parts (draft)

| Ref | Part | Notes |
|---|---|---|
| U1 | ATtiny412 (SOIC-8) | the brain |
| U2 | MCP23017 (SOIC-28) | A0–A2 → GND (addr 0x20), RESET → VCC |
| R1, R2 | 4.7 kΩ | I2C pull-ups |
| R3 + LED1 | 1 kΩ + LED | status |
| R4 | 10 kΩ | MCP23017 RESET pull-up |
| C1, C2 | 100 nF | decoupling, one per IC |
| C3 | 10 µF | bulk |
| J1 | 1×4 header | 5V / GND / TX / RX (also powers the board) |
| J2 | 1×3 header | UPDI: 5V / UPDI / GND |
| J3 | 2×8 header | matrix rows + columns |

## Status

- [x] Architecture, pinout and parts list
- [ ] Schematic (KiCad)
- [ ] PCB layout (KiCad, 2 layers)
- [ ] BOM with part numbers + cost check
- [ ] Submit to 8-Pin Grant
- [ ] Assemble, firmware, demo video
- [ ] Lichess bridge app

Progress log: [journal.md](journal.md)

## Author

Pietro Justino — [@NeekNegoer](https://github.com/NeekNegoer)
