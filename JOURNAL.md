# Build Journal

Logging what I do as I go, with hours and photos (KEEB checks these). Newest first.

Total so far: ~30h

---

### 2026-08-27 — Design, repo, layout, and full PCB
**Hours: ~30h (cumulative, approximate)**

What I did:
- Chose the build: 65% layout with an encoder cluster, hotswap switches, RGB, and an OLED.
  Controller: Raspberry Pi Pico (RP2040). Firmware: RMK.
- Set up the GitHub repo and the project structure (pcb / case / firmware / photos).
- Wrote the firmware config (`firmware/keyboard.toml`): 5×15 matrix, base + Fn layers,
  rotary encoder, and OLED.
- Designed the physical layout in Keyboard Layout Editor; fixed the arrow cluster so the
  up arrow sits above the down arrow.
- Generated the switch-matrix netlist from the layout and imported it into KiCad.
- Placed the 67 switches + diodes and routed the matrix (kbplacer + autorouter).
- Wired the Pico to the matrix (ROW0–4 → GP0–4, COL0–14 → GP5–19).
- Added and wired the extras: rotary encoder (GP20/21), OLED header + I2C pull-ups
  (GP26/27), a 5-zone SK6812 RGB chain (GP22) with a 74AHCT125 level shifter, and the
  +5V / +3V3 / GND power network.
- Verified connectivity net-by-net, ran DRC (0 unconnected), and exported Gerbers.

Board size ended up 320×152mm. Next: case design in Onshape (OLED window, encoder-knob
hole, RGB), then flash the firmware and order the PCB.

<!-- Add photos of the KiCad board / first PCB when available -->

---
