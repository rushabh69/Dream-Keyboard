# PCB

KiCad project for the keyboard PCB. 65% layout with an encoder cluster, hotswap sockets,
RGB and an OLED. Raspberry Pi Pico as the controller, one 1N4148 diode per key.

Matrix: 5 rows × 15 cols. Pin mapping (matches `firmware/keyboard.toml`):

| Signal | Pico GPIO |
|---|---|
| ROW0–ROW4 | GP0–GP4 |
| COL0–COL14 | GP5–GP19 |
| Encoder A / B | GP20 / GP21 |
| RGB (WS2812 DIN) | GP22 |
| OLED SDA / SCL (I2C1) | GP26 / GP27 |

Parts / footprints to add (marbastlib for the keyboard parts):

- **Hotswap sockets** — Kailh MX hotswap footprint (marbastlib `SW_MX_1u` hotswap variant),
  not soldered switches.
- **Encoder** — EC11 rotary encoder footprint; A/B to GP20/GP21, encoder push wired into the
  matrix at (row0, col14).
- **RGB** — SK6812 MINI-E LEDs chained (DIN→DOUT), data from GP22, plus decoupling caps.
- **OLED** — 4-pin I2C header (GND/VCC/SCL/SDA) to GP27/GP26.

Switches on the 19.05 mm grid. Run DRC, then export Gerbers + drill files to `gerbers/`.
