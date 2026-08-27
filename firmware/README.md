# Firmware

RMK (Rust) firmware for the Pico. Config is in [`keyboard.toml`](keyboard.toml).

Features wired in:
- **Rotary encoder** — volume on the base layer, page scroll on Fn.
- **OLED (SSD1306, 128×64, I2C1)** — configured in TOML.
- **Macro cluster** — M1/M2/M3 = copy / paste / cut.
- **Two layers** — base 65% and an Fn layer (F-keys + nav).
- **RGB (WS2812)** — the data line is on GP22, but addressable RGB isn't set up in
  `keyboard.toml`; RMK needs a small amount of Rust for it. Add it after the base build
  works: https://rmk.rs/docs/

## Build & flash

```bash
cargo install rmkit
rmkit init            # rp2040, keyboard.toml
# drop this keyboard.toml over the generated one
cargo build --release
```

Then hold BOOTSEL on the Pico, plug in USB, and copy the `.uf2` to the `RPI-RP2` drive.

The matrix, encoder, and I2C pins in `keyboard.toml` must match the KiCad schematic nets.
Default wiring is col2row (diode cathode → row); add `row2col = true` if it's reversed.
