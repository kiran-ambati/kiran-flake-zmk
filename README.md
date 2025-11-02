# Kiran Flake – Right Half Test Firmware

This is a minimal ZMK config to flash and test ONLY the right half of the Anywhy Flake keyboard (Seeeduino XIAO BLE).

- Shield: `anywhy_flake_right` (provided by the sibling `flake-zmk-module`)
- Board: `seeeduino_xiao_ble`
- Keymap: Single layer (`test`) with simple QWERTY-style bindings

## Prereqs
- Zephyr SDK toolchain + Python installed per ZMK docs
- West initialized from this folder
- This repo lives next to `flake-zmk-module/` in the same parent directory, as in:

```
<parent>
  ├─ flake-zmk-module/
  └─ kiran-flake/
```

## One-time setup
From PowerShell in `kiran-flake/`:

```powershell
# Initialize a west workspace using this config
west init -l .

# Fetch ZMK + the flake shield module
west update
```

If you re-run `west update` later and it says `flake-zmk-module` already exists, that's fine.

## Build (right half only)
```powershell
# Clean old build (optional when iterating)
west build -t pristine

# Build right half UF2
west build -b seeeduino_xiao_ble -- -DSHIELD=anywhy_flake_right
```

The UF2 will be at:
```
build\zephyr\zmk.uf2
```

## Flash
1. Plug the XIAO BLE into USB on your PC.
2. Enter the bootloader (double-tap the reset pads/button on the XIAO BLE).
3. A new USB drive appears. Drag and drop `build\zephyr\zmk.uf2` onto it.

## Notes
- This config only has one layer to keep testing simple. The left side isn’t required for this test build.
- If keys don’t send anything: ensure you built `anywhy_flake_right` and that the XIAO BLE is in bootloader when flashing.
- To tweak the keymap, edit `config/anywhy_flake.keymap` and rebuild.
