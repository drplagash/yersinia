# yersinia

![yersinia](banner.jpg)

Real attacker commands and classified payloads, captured live from a controlled honeypot environment ([Oráculo SOC](https://github.com/drplagash)). Plain text, no synthetic data — every file here is something an attacker actually typed or served against a real (emulated) service.

The companion credential dictionaries (usernames/passwords/combos) live in [pandemia](https://github.com/drplagash/pandemia). Real malware binaries recovered from these samples live in a separate repo, cross-referenced here by SHA256 once available.

Updated automatically, every 12 hours.

## What's in here

### `comandos-frecuentes.txt` — always the latest snapshot

Unique shell commands attackers actually ran, most-repeated first. Full regenerate every run.

### `familias/` — captured payloads, classified, one folder per sample

```
familias/
└── <classification>/
    └── <sha256-short>/
        ├── payload.txt    (always)
        └── session.txt    (only when a real attacker session produced it)
```

`payload.txt` has a header with the sample's metadata (SHA256, kind, size, first seen, times seen, YARA rule matches) followed by its plain-text content.

`session.txt` only shows up when the payload was captured *live*, mid-session, off a real attacker's keyboard (Cowrie/ADBHoney `file_download` events) — in that case it's the actual command sequence that led to it, redacted to the /24. Payloads recovered instead through automated follow-up investigation of attacker infrastructure (not something anyone typed) don't get a fabricated session — no file, rather than a fake one.

Right now the only classification with real samples is `script_generic` — benign login/default pages picked up while investigating attacker infrastructure, none of them tied to a live session. No actual malware has been captured yet; as soon as it is, it gets its own classification folder here (`downloader/`, `backdoor/`, `cryptominer/`, `c2_client/`, etc.) and the corresponding binary goes into the malware repo, cross-referenced by SHA256.

## Source

Captured via [Cowrie](https://github.com/cowrie/cowrie)/[ADBHoney](https://github.com/adbhoney/adbhoney) honeypots (part of a [T-Pot](https://github.com/telekom-security/tpotce) deployment) plus follow-up automated investigation of attacker infrastructure. Classification and YARA matching run against the community [Yara-Rules](https://github.com/Yara-Rules/rules) ruleset. No source IPs, internal topology, or infrastructure details beyond the redacted /24 are published here.

## Updates

`comandos-frecuentes.txt` regenerates fully every run. `familias/` is incremental — new samples get added as they're captured and classified, existing ones are refreshed in place (a `session.txt` can appear later if one gets linked after the fact).

## Disclaimer

For security research and authorized testing only. These are real attacker-supplied commands and payloads collected in a controlled, isolated lab. Text content is published as-is for research purposes — do not execute anything from `familias/` outside an isolated, disposable environment.

## License

MIT — see [LICENSE](LICENSE).
