# TrueNAS Community Edition — lab notes

Practical notes for running **TrueNAS Community Edition** (formerly TrueNAS SCALE) as a homelab NAS. This is **not** a vendor brochure: official docs win for install wizards and screenshots.

**Hands-on status:** The only version **personally exercised** in this repo’s history was **SCALE 22.12.1** (Kubernetes Apps / TrueCharts era — see [Historical lab notes](#historical-lab-notes-scale-22121--truecharts)). Sections about **25.10 / Community Edition / Docker Apps** are **compiled from official TrueNAS documentation** (Software Status, 25.10 docs, Apps Market) as of September 2026 — **not** a fresh re-lab on Goldeye. Treat them as pointers, not “I just tested this.”

**Doc baseline:** TrueNAS **25.10.x (Goldeye)** — recommended stable on the [Software Status](https://www.truenas.com/docs/softwarestatus/) page as of September 2026 (e.g. **25.10.7**). Early train: **26.x BETA** (not for production data).

> Naming: from **25.04** onward, iX calls the free Linux product **TrueNAS Community Edition**. Older material still says “SCALE”; same lineage.

## Why use it

- ZFS pools, snapshots, replication, SMB/NFS/iSCSI shares
- Web UI for day-to-day storage ops
- **Apps** on a Docker backend (since **24.10**), plus VMs / Containers on current trains
- Free Community Edition for non-enterprise use; Enterprise adds HA and appliance features

For a full k8s control plane or heavy custom ingress meshes, prefer a dedicated cluster (see sibling notes: [kubernetes](https://github.com/Younest9/kubernetes), [okd](https://github.com/Younest9/okd)) and treat TrueNAS as storage.

## Hardware (official ballpark)

From current Community Edition guidance (verify on the [download / requirements](https://www.truenas.com/download/) pages before buying):

- **RAM:** 8 GB minimum; **16 GB+** recommended (ZFS + Apps needs headroom)
- **Boot:** small SSD/NVMe for the OS
- **Data:** redundant disks for a real pool (mirrors / RAIDZ as you design)
- Prefer **HBA / IT-mode** over hardware RAID controllers for ZFS

## Install (high level)

1. Download the current Community Edition ISO from [TrueNAS downloads](https://www.truenas.com/download-truenas-community-edition) (or the main [download hub](https://www.truenas.com/download/)).
2. Write to USB (or attach ISO to a VM).
3. Boot and complete the installer; set root / admin credentials carefully.
4. Open the web UI, set **Network** (static IP + DNS if not using DHCP), then create a **Storage** pool.

Official walkthroughs: [Getting Started / 25.10](https://www.truenas.com/docs/scale/25.10/), [Installation](https://www.truenas.com/docs/scale/25.10/gettingstarted/install/).

## Apps on 24.10+ / 25.10 (Docker)

TrueNAS **24.10 (Electric Eel)** replaced the old **Kubernetes / k3s Apps** backend with **Docker**. On **25.10**:

1. **Apps → Configuration → Choose Pool** (or Settings) — pick a pool for app data.
2. **Discover Apps** — Stable / Community catalogs (Enterprise catalog on licensed systems).
3. Install from catalog, or deploy custom workloads:
   - **Custom App** (guided), or
   - **Install via YAML** (Docker Compose) — see [Installing Custom Apps](https://apps.truenas.com/managing-apps/installing-custom-apps/).

Compose tip (current Apps Market docs): YAML should start with a top-level Compose element such as `services:` (or `name:` / `include:`). Prefer writing Compose offline, then paste.

**TrueCharts / third-party Helm catalogs** from the SCALE Kubernetes era are **not** the supported path on Docker-backed Apps. Recreate with official/community catalog apps or Compose; TrueCharts moved off SCALE Apps (Talos/cluster tooling for their own path).

Useful links:

- [Apps Market — initial setup](https://apps.truenas.com/getting-started/initial-setup/)
- [Configuring VMs and Apps (25.10)](https://www.truenas.com/docs/scale/25.10/gettingstarted/configure/vmandappconfigscale/)

## Storage & sharing (checklist)

1. Create pool → datasets for shares / app data (isolate app datasets).
2. **Sharing:** SMB / NFS / iSCSI as needed.
3. Snapshots + periodic replication if you care about recovery.
4. Keep OS boot pool separate from bulk data when possible.

## Limitations (Community Edition — product reality)

Still true for Community Edition vs Enterprise (confirm on current Enterprise marketing/docs):

- No TrueNAS **High Availability** cluster appliance features on CE
- Enterprise-only hardware / support / some directory & appliance integrations
- Apps are **Docker-based**, not a full DIY Kubernetes distribution — fine for NAS-adjacent services; not a substitute for a purpose-built k8s lab

## Historical lab notes (SCALE **22.12.1** + TrueCharts)

The findings below were recorded against **TrueNAS SCALE 22.12.1** with the **old Kubernetes Apps** model and **TrueCharts**. They explain why many 2022–2024 “SCALE apps” guides feel wrong on **25.10**.

| Topic (22.12.1 era) | Observation then |
|---|---|
| Official chart networking | Often NodePort-only; limited service-type / ingress knobs vs TrueCharts |
| TrueCharts + official apps | Hard to pair official apps behind a TrueCharts reverse proxy / ingress |
| Custom storage on TrueCharts | HostPath / PVC / NFS mounts sometimes failed to attach while the app still “deployed” |
| Launch Docker Image | Service type fixed to NodePort; little/no ingress config |
| Timezone | Host/UI timezone mismatch broke some chart apps (e.g. Nextcloud clocks) |

**Do not treat that table as current 25.10 bug status.** Re-validate on your build if you still care; prefer Docker Compose or catalog apps on Goldeye.

## Practical recommendations (2026)

1. Stay on the **General / Mission Critical** train from [Software Status](https://www.truenas.com/docs/softwarestatus/) unless you intentionally test **26 BETA**.
2. Use TrueNAS for **ZFS + shares**; put complex app meshes on a VM or separate host if the Apps UI fights you.
3. Prefer **Compose YAML** or catalog apps over resurrecting Kubernetes-era catalogs.
4. Document your pool layout and credentials offline — not in this repo.

## References

- [Software Status](https://www.truenas.com/docs/softwarestatus/)
- [25.10 (Goldeye) docs](https://www.truenas.com/docs/scale/25.10/)
- [25.10 version notes](https://www.truenas.com/docs/scale/25.10/gettingstarted/versionnotes/)
- [Downloads](https://www.truenas.com/download/)
- [TrueNAS Apps Market](https://apps.truenas.com/)
- [Community Edition rename (blog)](https://www.truenas.com/blog/truenas-community-edition-release-2504/)

## License

MIT — see [LICENSE](LICENSE).
