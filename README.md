# Security Home Lab (lab-as-code)

Starter repository to build a reproducible **security home lab** aligned with the career roadmap in `ruta_ciberseguridad.md`.

> **Purpose:** Practice network detection, hardening, SIEM and automation — and produce real portfolio evidence (GitHub + writeups).

## Disclaimer
Use only **your own lab**. Never scan, attack or test systems you do not own or have written authorization for.

## Lab topology (planned)

```
Internet ──► pfSense/OPNsense ──► VLAN MGMT
                     │
                     ├── VLAN USERS   (Win10/11 + Sysmon + Wazuh agent)
                     ├── VLAN SERVERS (Ubuntu + DVWA + Suricata sensor)
                     ├── VLAN ATTACK  (Kali) ── isolated, lab-only
                     └── VLAN MON     (Elastic/Wazuh manager + Grafana)
```

See `docs/architecture.md` for more detail.

## 7-day quick start
1. Day 1: Fork/clone this repo, create `backlog.md` with 20+ security gaps you want to close.
2. Day 2: Install VirtualBox/VMware + Docker Desktop. Run `docker compose config`.
3. Day 3: Build 4 VMs (pfSense, Kali, Ubuntu, Windows 10) + snapshots.
4. Day 4: Add Suricata sensor + enable `custom.rules`. Replay a test PCAP and verify alerts.
5. Day 5: Install Wazuh agent on Windows; confirm telemetry shows up.
6. Day 6: Bring up a SIEM (Wazuh manager or Elastic) and dashboards. Run `scripts/verify_lab.py`.
7. Day 7: Publish first writeup: "My security lab: architecture and objectives" + link repo.

## Milestone M0
- ✅ Reproducible lab documented on GitHub.
- ✅ Backlog of 20+ security concepts you do **not** dominate.
- ✅ TryHackMe account (target: top 30%).

## Quick start (Suricata sensor only)
```bash
# Clone or open this repo
docker compose config
docker compose --profile suricata up -d
docker compose --profile suricata logs -f
```

For the full stack (Wazuh/Elastic), see `docs/full-stack.md` (build incrementally; do not install everything at once).

## Repository structure
```
.
├─ docker-compose.yml
├─ .env.example
├─ suricata/
│  ├─ etc/            # suricata.yaml (mount or copy)
│  ├─ logs/
│  └─ rules/custom.rules
├─ scripts/
│  └─ verify_lab.py
├─ docs/
│  ├─ architecture.md
│  ├─ full-stack.md
│  └─ writeup-template.md
├─ .github/workflows/
├─ .gitignore
└─ LICENSE
```

## Next steps
- [ ] Replace all `yourusername` placeholders.
- [ ] Add real lab IPs/hostname notes to `.env` (do NOT commit secrets).
- [ ] Add at least 3 detection rules (port scan, DNS tunneling, SMB lateral movement).
- [ ] Add 1 Python script with tests + GitHub Actions.
- [ ] Publish first writeup and link it in README.

## License
MIT — see `LICENSE`.
