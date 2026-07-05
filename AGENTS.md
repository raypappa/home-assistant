# Home Assistant Configuration

This is a Home Assistant config directory, not a traditional software project. There are no build, test, or lint steps.

## Structure

- `configuration.yaml` — main config; includes all other YAML files
- `automations.yaml` — all automations (time-based, ZHA button triggers, state changes)
- `scripts.yaml` — reusable scripts (bathroom pre-heat, always-on device check)
- `scenes.yaml` — lighting scenes for bedroom and office (Hue, Signify)
- `climate.yaml` — climate group combining 4 Mysa thermostats
- `switch.yaml` — Broadlink IR blaster (living room light/fan)
- `device_tracker.yaml` — DD-WRT router tracking
- `zha.yaml` — Zigbee with custom quirks in `custom_zha_quirks/`
- `route53.yaml` — AWS Route53 DNS updates (daily at 05:00)
- `shell_command.yaml` — `git pull` command, triggered by GitHub commit sensor
- `esphome/` — ESPHome device configs
- `blueprints/` — reusable automation/script blueprints
- `themes/` — frontend themes (referenced by `configuration.yaml`)

## Tooling

- **Python 3.13+** managed by `uv` (`uv.lock`, `.python-version`)
- **ESPHome** is the only Python dependency — used to compile/flash ESPHome configs in `esphome/`
- **YAML formatting**: `.yamlfmt` with `indentless_arrays: true`

## Secrets & Ignored Files

- `secrets.yaml` is gitignored — use `!secret <key>` references in YAML
- Also ignored: `*.db*`, `.storage/`, `home-assistant.log`, `tts/`, `www/`, `zigbee.db`, `tags`
- Never commit `secrets.yaml` or any AWS credentials

## Conventions

- Temperature in **Fahrenheit**
- ZHA quirks enabled via `custom_zha_quirks/` directory
- Automations use `!include` pattern — edit the included files, not inline in `configuration.yaml`
- Git auto-pull automation watches `sensor.raypappa_home_assistant_latest_commit` and runs `shell_command.git_pull`
