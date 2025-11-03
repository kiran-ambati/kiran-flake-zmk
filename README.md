# Kiran Flake (ZMK user config)

Single-piece 6x5 (29-key) keyboard using Seeed XIAO nRF52840 BLE.

- Controller: Seeed XIAO BLE (nRF52840)
- Matrix: 6 columns x 5 rows (col2row)
- Columns: D5, D4, D3, D2, D1, D0
- Rows:    D10, D9, D8, D7, D6 (pulldown)
- Bottom row has only 5 physical keys. The unused matrix position is Row 4, Col 0.

## Files

- `boards/shields/kiran_flake/kiran_flake.dtsi` — KScan and GPIO matrix wiring
- `boards/shields/kiran_flake/kiran_flake.overlay` — Includes base DTSI
- `boards/shields/kiran_flake/kiran_flake.keymap` — Keymap (base + fn)
- `boards/shields/kiran_flake/Kconfig.*` — Shield Kconfig glue
- `boards/shields/kiran_flake/kiran_flake.zmk.yml` — Shield metadata
- `config/west.yml` — Points to `zmkfirmware/zmk@main`
- `build.yaml` — Build matrix (board + shield)
- `.github/workflows/build.yml` — Reuses ZMK's build workflow

## Build locally (optional)

You can build via GitHub Actions (recommended) or locally with West + Zephyr toolchains installed.

### GitHub Actions

Push this folder as the root of a new GitHub repository, then:

- On each push to `main`, the "Build (Kiran Flake)" workflow runs.
- It uses ZMK's shared workflow and `build.yaml` to build the UF2 firmware artifact.
- Download the `kiran_flake.uf2` artifact from the workflow run and drag/drop it to the XIAO's USB mass storage after entering bootloader mode.

### Local build

If you have Zephyr + West set up, from the repo root:

```powershell
# Initialize west and fetch ZMK
west init -l config ; west update

# Build (Windows PowerShell)
west build -s zmk/app -b seeeduino_xiao_ble -- -DSHIELD=kiran_flake

# The UF2 will be in build/zephyr/zephyr.uf2 (rename as desired)
```

## Notes

- If your hardware routes the bottom-row empty position elsewhere, adjust the `&none` placeholder in `kiran_flake.keymap` accordingly.
- If your ZMK version uses a different board name (some releases use `seeed_xiao_nrf52840`), update `build.yaml` and the local build command to match.
