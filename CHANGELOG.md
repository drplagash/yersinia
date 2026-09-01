# Changelog

All notable dataset updates are logged here, one entry per export.

## 2026-09-01

- Restructured `familias/` into per-sample folders (`<classification>/<sha256-short>/payload.txt` + optional `session.txt`).
- Dropped the generic `sesiones/` folder — replaced by real per-payload session linkage (only present when a sample was captured live off an actual attacker session).
- `comandos-frecuentes.txt`: 194 unique commands
- `familias/script_generic/`: 3 classified samples (none tied to a live session yet)
