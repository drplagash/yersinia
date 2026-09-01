# Rival-miner eviction script (inter-botnet competition)

# Rival-miner eviction script

## What it does

This session's command sequence does not deploy a cryptominer - it **removes one**. It systematically kills known XMRig process names across three architectures (`xmrig-aarch64`, `xmrig-armv7`, `xmrig-x86_64`), tears down a persistence mechanism named `wannamine`/`watchdog` across essentially every autostart location a Linux/Android system could use (systemd, init.d, rc.local, cron, crontab, anacrontab, supervisor, udev rules, shell profile files, an Android `post-fs-data.d`/`service.d` Magisk module path), reverts `sysctl` memory-overcommit settings, and finally deletes its own marker file (`.wannamine_processed`) and several backup/hidden directories before fingerprinting the device (`getprop ro.product.cpu.abi`, `uname -m`, `arch`).

## Why it's notable

This is not defensive cleanup by a device owner - a device owner does not know to hunt for a specific rival botnet's process names and persistence paths across six+ competing autostart mechanisms with `su -c` on every line. This is one cryptomining/IoT botnet operator's **takeover script for a device already compromised by a competitor** ("WannaMine"-branded miner infrastructure). It evicts the previous occupant's miner and persistence before (presumably, in a later stage not captured in this session) installing its own - a direct, hands-on-keyboard illustration of the resource competition between rival cryptojacking campaigns for the same pool of compromised Android/IoT devices.

## Classification note

Flagged as `cryptominer` because it is unambiguously part of a cryptomining campaign's operational tooling, even though it contains no pool URL or wallet address itself (nothing to extract - its job is removal, not deployment).
