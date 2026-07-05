# Home Assistant Configuration

Personal Home Assistant configuration for a smart home setup.

## Overview

Manages automations, lighting scenes, climate control, and device integrations for a home running Home Assistant.

## Key Integrations

- **Zigbee (ZHA)** — with custom quirks for device compatibility
- **Hue / Signify** — bedroom and office lighting with scenes
- **Mysa** — 4 thermostats grouped into a single climate entity (Fahrenheit)
- **Broadlink** — IR blaster for living room light and fan
- **ESPHome** — custom ESP device firmware
- **DD-WRT** — router-based device tracking
- **AWS Route53** — daily public DNS updates

## Structure

| File | Purpose |
|------|---------|
| `configuration.yaml` | Main config, includes all others |
| `automations.yaml` | Time-based and ZHA button-triggered automations |
| `scripts.yaml` | Reusable scripts (bathroom pre-heat, always-on check) |
| `scenes.yaml` | Lighting scenes for bedroom and office |
| `climate.yaml` | Mysa thermostat group |
| `switch.yaml` | Broadlink IR blaster config |
| `device_tracker.yaml` | DD-WRT router device tracking |
| `zha.yaml` | Zigbee config with custom quirks |
| `route53.yaml` | AWS Route53 DNS record updates |
| `esphome/` | ESPHome device configurations |
| `blueprints/` | Reusable automation and script blueprints |
| `themes/` | Frontend themes |

## Setup

Requires Python 3.13+ managed by `uv`:

```bash
uv sync
```

ESPHome configs in `esphome/` can be compiled and flashed using the `esphome` CLI.

## Secrets

`secrets.yaml` is gitignored. Use `!secret <key>` references in YAML files. Never commit `secrets.yaml` or AWS credentials.

## Git Auto-Pull

An automation watches `sensor.raypappa_home_assistant_latest_commit` and runs `git pull` on new commits, keeping the config in sync with this repo.
