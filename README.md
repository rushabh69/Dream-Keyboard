# My KEEB Keyboard

A 65% mechanical keyboard I'm building for [Hack Club KEEB](https://keeb.hackclub.com/), with
a rotary encoder, hotswap switches, RGB, and an OLED.

## Specs

- 65% layout with an encoder cluster (67 keys, 5×15 matrix)
- Rotary encoder (volume / page scroll), hotswap switches
- RGB lighting (SK6812) and a 128×64 OLED
- Raspberry Pi Pico (RP2040)
- RMK firmware (Rust)
- PCB designed in KiCad
- 3D-printed case, designed in Onshape

## Build

The PCB is in [`pcb/`](pcb/) (KiCad), the case in [`case/`](case/) (Onshape), and the
firmware config in [`firmware/keyboard.toml`](firmware/keyboard.toml). I'm keeping the
build log in [`JOURNAL.md`](JOURNAL.md) as I go.

## Files

- [`pcb/`](pcb/) — PCB and schematic files (KiCad), plus exported Gerbers and drill files
- [`case/`](case/) — case and plate CAD, exported as STEP/STL (mm)
- [`firmware/`](firmware/) — RMK firmware config
- [`photos/`](photos/) — build photos
- [`bom.csv`](bom.csv) — parts list
- [`JOURNAL.md`](JOURNAL.md) — build log
