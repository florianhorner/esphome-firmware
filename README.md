# esphome-firmware

Compiled ESPHome firmware for BLE proxies, auto-deployed by CI.

## Structure

```
common/
  ble-proxy-base.yaml   # Shared BLE proxy configuration
ble-proxy-1.yaml        # Per-device config (name, board)
ble-proxy-2.yaml
ble-proxy-3.yaml
secrets.yaml.example    # Template for secrets
```

## Setup

1. Copy `secrets.yaml.example` to `secrets.yaml` and fill in your values.
2. Install [ESPHome](https://esphome.io/guides/installing_esphome).
3. Flash a device:
   ```bash
   esphome run ble-proxy-1.yaml
   ```

## Adding a new proxy

1. Copy any `ble-proxy-*.yaml` and update `name`, `friendly_name`, and `board`.
2. Add the new file to the matrix in `.github/workflows/build.yml`.
3. Push to `main` — CI will build and create a release with the firmware binaries.

## CI/CD

- **On push to `main`**: builds all proxy configs, then creates a GitHub Release with `.bin` files.
- **On pull requests**: builds all configs to validate changes.
- Firmware artifacts are also available as workflow artifacts on every build.
