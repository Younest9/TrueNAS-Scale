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

The text below is the **original hands-on write-up** from this repo (testing **TrueNAS SCALE 22.12.1**, custom catalog = **TrueCharts**, Kubernetes Apps era). Kept for the record. It is **not** a claim about **25.10** Docker Apps.

### Limitations (as written for 22.12.1)

> The version of TrueNAS SCALE we are using for testing is 22.12.1.

* TrueNAS SCALE does not support Clustering.
* TrueNAS SCALE does not support High Availability.
* TrueNAS SCALE does not support TrueNAS Enterprise features such as TrueNAS Enterprise Plugins, TrueNAS Enterprise Active Directory, TrueNAS Enterprise LDAP, TrueNAS Enterprise Kerberos, TrueNAS Enterprise SNMP, TrueNAS Enterprise S3...
* TrueNAS SCALE does not support TrueNAS Enterprise hardware features such as TrueNAS Enterprise Hardware Encryption, TrueNAS Enterprise Hardware Acceleration...
* TrueNAS SCALE does not offer a lot of customization options for the applications deployed from a docker image, or the official chart (Forcing you to exposing apps in nodePort always, not integrating a reverse proxy, etc.)

### Known Issues (as written for 22.12.1)

> The version of TrueNAS SCALE we are using for testing is 22.12.1.

When Testing, we found the following issues : (The custom chart we used is TrueCharts)

* When deploying apps from the official chart, the apps are accessible only on NodePort, we cannot configure them to use a certain type of service (ClusterIP, LoadBalancer, etc.). on the other hand, when deploying apps from the custom chart, we can configure the service type to use.
* When deploying a reverse proxy from the custom chart, it works as expected, but pairing it with apps from the official chart, it's not possible to configure them to use the reverse proxy. (For example, when deploying a reverse proxy, and a Nextcloud app from the official chart, it's not possible to configure the ingress option of the Nextcloud app to use the reverse proxy).
* When deploying apps from a custom chart, there's an option to expose the apps as a ClusterIP, but not on the official chart (Same App, different chart).
* When deploying apps from the custom chart, it's possible to add custom storage, but for some raison, it doesn't work as expected. The apps are deployed, but the storage is not mounted (All type of storage: NFS, HostPath, EmptyDir, PVC, etc.). Also, we can deploy an app using custom chart when there's no storage needed in the configuration, but when we add a storage, it doesn't work as expected (For a lot of apps using the custom chart).
* When deploying apps using **Launch Docker Image** option, there's no option to configure the service type (NodePort, ClusterIP, LoadBalancer, etc.), it's always NodePort. Also, there's no option to configure the ingress option.
* It's required to edit the **timezone** of TrueNAS SCALE to match the timezone of the host, otherwise, the apps deployed from the custom chart will not work as expected (For example, when deploying a Nextcloud app from the custom chart, the timezone is not set correctly, and the app is not working as expected).

**Do not treat the 22.12.1 list as current 25.10 bug status.** Prefer Docker Compose or catalog apps on Goldeye; re-lab before asserting new issues.

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
