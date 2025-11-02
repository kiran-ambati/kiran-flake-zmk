# Kiran Flake Firmware

This is a test configuration for the right half of the Flake keyboard only.

## About

This configuration allows you to test the right side of your split keyboard independently, without needing the left side connected. The keyboard will work as a standalone 30-key keyboard (6 columns x 5 rows).

## Hardware

- Board: Seeed Studio XIAO BLE (nRF52840)
- Right half of Flake keyboard

## Pin Configuration

**Rows (output):**
- Row 0: D10
- Row 1: D9
- Row 2: D8
- Row 3: D7
- Row 4: D6

**Columns (input):**
- Col 0: D5
- Col 1: D4
- Col 2: D3
- Col 3: D2
- Col 4: D1
- Col 5: D0

## Keymap

The default keymap includes:
- **Layer 0 (Base):** Right half of a standard QWERTY layout
- **Layer 1 (Num):** Number pad and symbols
- **Layer 2 (Fn):** Function keys, media controls, and Bluetooth controls

## Building

To build the firmware, use the included `build.yaml` configuration with ZMK's build system.

## Flashing

Flash the resulting UF2 file to your XIAO BLE by:
1. Double-press the reset button to enter bootloader mode
2. Copy the `kiran_flake-seeeduino_xiao_ble-zmk.uf2` file to the mounted drive
3. The board will automatically reboot with the new firmware

## Notes

- This is a **non-split** configuration for testing purposes only
- ZMK split features are disabled
- When you're ready to build the complete split keyboard, use the original `anywhy_flake` configuration
