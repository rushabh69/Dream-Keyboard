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

## Start from the layout (auto-place the matrix)

`layout.kle.json` is the full 65% layout with each key labelled by its `row,col` matrix
position. Instead of placing 67 keys by hand:

`dream-keyboard.net` is a pre-generated KiCad netlist for the whole matrix — all 67
switches + 67 diodes, wired to nets ROW0–ROW4 and COL0–COL14. It was generated from
`layout.kle.json` with `kle2netlist` (switch = `PCM_marbastlib-mx:SW_MX_1u`,
diode = `Diode_THT:D_DO-35_SOD27_P7.62mm_Horizontal`).

Bring the matrix into a PCB:

1. Install the **marbastlib** library so the switch footprint resolves.
2. New KiCad project in this folder → open the **PCB Editor**.
3. **File → Import → Netlist** → pick `dream-keyboard.net` → **Update PCB**. All 67
   switch+diode pairs load with the matrix already connected (you'll see the ratsnest).
4. Install the **kbplacer** plugin (Plugin and Content Manager) and run it with
   `layout.kle.json` to auto-arrange the switches on the 19.05 mm grid.
   - kbplacer: https://github.com/adamws/kbplacer
5. Hand-add the Pico, encoder, OLED header, and SK6812 chain, and wire them to the GPIO in
   the pin table above.
6. Draw the outline, route, DRC, export Gerbers.

The netlist covers only the key matrix — the Pico/encoder/OLED/RGB are added by hand.
