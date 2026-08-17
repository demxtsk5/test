# Proxmox VE – Entwicklungspfad (10 Wochen · 5 Sprints)

**Zeitbudget:** 2 Sessions à 2 Stunden pro Woche = 4 h/Woche → 40 h gesamt
**Sprintlänge:** 2 Wochen = 4 Sessions = 8 h
**Sprint-Logik:** Jeder Sprint endet mit einem *Sprint-Review* (Definition of Done, prüfbar am Lab) und einer kurzen Retro (Was blockiert? Was wiederholen?).

> **Hinweis zu Links:** Die Dokumentations- und Tool-Links sind offizielle Quellen. Bei YouTube verweise ich bewusst auf **Kanäle plus Suchbegriff** statt auf einzelne Video-IDs, da Einzelvideos häufig ersetzt/aktualisiert werden. Bitte kurz gegenprüfen, ob die jeweils aktuellste Version zur eingesetzten PVE-Major-Version passt.

---

## 0. Vorab: Lab-Basis wählen (Windows vs. macOS)

Der fachliche Lernpfad ist **identisch**. Unterschiedlich ist nur, **wie du das Lab betreibst** und **mit welchen Client-Tools** du arbeitest.

### Variante W – Windows-Nutzer

| Thema | Empfehlung |
|---|---|
| Lab-Plattform | Nested Virtualization: **Hyper-V** oder **VMware Workstation Pro** (für private Nutzung kostenlos), alternativ VirtualBox |
| Voraussetzung | CPU-Virtualisierung im BIOS/UEFI aktiv; für Cluster-Übungen ≥ 32 GB RAM empfohlen (16 GB machbar mit 2 Nodes) |
| Alternative | Gebrauchter Mini-PC (Intel N100 / Refurb-SFF) als physischer Node – deutlich realitätsnäher |
| USB-Stick / ISO | [Ventoy](https://www.ventoy.net) oder [Rufus](https://rufus.ie) |
| SSH / Terminal | Windows Terminal + integriertes OpenSSH, alternativ [PuTTY](https://www.putty.org) |
| Dateitransfer | [WinSCP](https://winscp.net) |
| IaC-Tooling | WSL2 als Linux-Unterbau für Terraform/Ansible ([WSL-Doku](https://learn.microsoft.com/de-de/windows/wsl/install)) |

Nested-Virtualization-Doku: [Microsoft Learn – Nested Virtualization](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/user-guide/nested-virtualization)

### Variante M – macOS-Nutzer

| Thema | Empfehlung |
|---|---|
| **Apple Silicon (M1–M4)** | ⚠️ **Proxmox VE ist x86_64-only.** Ein lokales Nested-Lab ist nur per Emulation (UTM/QEMU) möglich – funktionsfähig, aber sehr langsam. **Empfohlen:** externer Node statt lokal |
| Empfohlene Lösung (Apple Silicon) | (a) günstiger x86-Mini-PC im Heimnetz, (b) Root-Server / dedizierter Host bei einem Hoster mit PVE-Image, (c) Nested PVE in einer x86-Cloud-VM mit aktivierter Nested Virt |
| **Intel-Mac** | Nested Lab lokal möglich mit **VMware Fusion** (privat kostenlos) oder VirtualBox |
| USB-Stick / ISO | [balenaEtcher](https://etcher.balena.io) oder `dd` im Terminal |
| SSH / Terminal | macOS Terminal / iTerm2 – SSH ist nativ vorhanden |
| Dateitransfer | `scp`/`rsync`, GUI: [Cyberduck](https://cyberduck.io) |
| IaC-Tooling | [Homebrew](https://brew.sh) → `brew install terraform ansible` |
| Emulation lokal | [UTM](https://mac.getutm.app) · [UTM-Doku](https://docs.getutm.app) |

**Praxisempfehlung für macOS/Apple Silicon:** Sprint 1 Session 1 dafür nutzen, den externen Node zu beschaffen/bereitzustellen. Alles Weitere läuft dann über den Browser und SSH – ab dann ist der Pfad plattformneutral.

---

## Sprint 1 (Woche 1–2): Grundlagen & lauffähiges Lab

**Sprintziel:** Ein erreichbarer Proxmox-VE-Node mit erster VM und erstem LXC-Container.

| Session | Inhalt | Quellen |
|---|---|---|
| **1.1** | Virtualisierungsgrundlagen: Typ-1 vs. Typ-2, KVM/QEMU vs. LXC, Debian-Unterbau, Lizenz-/Repo-Modell (Enterprise vs. No-Subscription) | [Proxmox VE – Übersicht](https://www.proxmox.com/de/proxmox-virtual-environment/overview) · [Admin Guide, Kap. 1–2](https://pve.proxmox.com/pve-docs/pve-admin-guide.html) · [Paket-Repositories](https://pve.proxmox.com/wiki/Package_Repositories) |
| **1.2** | **W:** Nested Lab in Hyper-V/VMware aufsetzen, ISO booten, Installation<br>**M:** externen/emulierten Node bereitstellen, Installation bzw. Hoster-Image | [Download](https://www.proxmox.com/de/downloads) · [Installation Wiki](https://pve.proxmox.com/wiki/Installation) · [ZFS on Linux](https://pve.proxmox.com/wiki/ZFS_on_Linux) |
| **1.3** | Web-UI-Tour, Nutzer/Rollen/API-Tokens, No-Subscription-Repo setzen, Updates, SSH-Zugang, Grundabsicherung | [User Management](https://pve.proxmox.com/wiki/User_Management) · [Admin Guide – Access Control](https://pve.proxmox.com/pve-docs/pve-admin-guide.html#chapter_user_management) |
| **1.4** | Erste Linux-VM (ISO-Upload, virtio, QEMU Guest Agent) + erster LXC-Container aus Template; Vergleich Ressourcenverbrauch | [Qemu/KVM Guest](https://pve.proxmox.com/wiki/Qemu/KVM_Virtual_Machines) · [QEMU Guest Agent](https://pve.proxmox.com/wiki/Qemu-guest-agent) · [Linux Container](https://pve.proxmox.com/wiki/Linux_Container) |

**Videos:** [Learn Linux TV](https://www.youtube.com/@LearnLinuxTV) → Suche „Proxmox Full Course“ · [Proxmox Server Solutions (offiziell)](https://www.youtube.com/@ProxmoxServerSolutions)

**Definition of Done**
- [ ] Web-UI über HTTPS erreichbar, SSH-Login funktioniert
- [ ] Node ist vollständig aktualisiert, Repos korrekt konfiguriert
- [ ] 1 VM + 1 LXC laufen, Guest Agent meldet die IP
- [ ] Du kannst den Unterschied VM ↔ LXC in drei Sätzen erklären

---

## Sprint 2 (Woche 3–4): Storage & Images

**Sprintziel:** Storage-Modell verstanden, Templates & Snapshots produktiv nutzbar.

| Session | Inhalt | Quellen |
|---|---|---|
| **2.1** | Storage-Typen: Directory, LVM/LVM-Thin, ZFS, NFS/CIFS, Ceph RBD; Content-Types; Thin Provisioning | [Storage Wiki](https://pve.proxmox.com/wiki/Storage) · [Admin Guide – Storage](https://pve.proxmox.com/pve-docs/pve-admin-guide.html#chapter_storage) |
| **2.2** | ZFS praktisch: Pool anlegen, Datasets, Kompression, ARC-Tuning, `zfs`/`zpool`-Basics, Disks hinzufügen/erweitern | [ZFS on Linux](https://pve.proxmox.com/wiki/ZFS_on_Linux) · [OpenZFS Docs](https://openzfs.github.io/openzfs-docs/) |
| **2.3** | Templates & Linked Clones, Cloud-Init-Images bauen und ausrollen | [Cloud-Init Support](https://pve.proxmox.com/wiki/Cloud-Init_Support) · [VM Templates & Clones](https://pve.proxmox.com/wiki/VM_Templates_and_Clones) |
| **2.4** | Snapshots vs. Backups, Disk-Resize, Storage-Migration, Aufräumen verwaister Disks; Helper-Scripts sichten | [community-scripts/ProxmoxVE](https://community-scripts.github.io/ProxmoxVE/) |

**Definition of Done**
- [ ] Mindestens zwei unterschiedliche Storages angebunden
- [ ] Ein Cloud-Init-Template existiert, aus dem in < 2 Min. eine fertige VM entsteht
- [ ] Snapshot erstellt, VM „kaputt gemacht“, per Rollback wiederhergestellt

---

## Sprint 3 (Woche 5–6): Netzwerk, Backup & Restore

**Sprintziel:** Segmentiertes Lab-Netz + funktionierende, getestete Backup-Strategie.

| Session | Inhalt | Quellen |
|---|---|---|
| **3.1** | Linux Bridge, VLAN-aware Bridge, Bonding, `/etc/network/interfaces`, SDN-Überblick | [Network Configuration](https://pve.proxmox.com/wiki/Network_Configuration) · [Admin Guide – SDN](https://pve.proxmox.com/pve-docs/pve-admin-guide.html#chapter_pvesdn) |
| **3.2** | Firewall auf Datacenter-/Node-/VM-Ebene, Security Groups, IP-Sets; optional Router-VM (OPNsense/pfSense) im Lab | [Proxmox Firewall](https://pve.proxmox.com/wiki/Firewall) · [OPNsense Docs](https://docs.opnsense.org) |
| **3.3** | Bordmittel-Backup: `vzdump`, Backup-Jobs, Modi (snapshot/suspend/stop), Retention, Notifications | [Backup and Restore](https://pve.proxmox.com/wiki/Backup_and_Restore) · [`vzdump` Manpage](https://pve.proxmox.com/pve-docs/vzdump.1.html) |
| **3.4** | **Proxmox Backup Server** installieren, Datastore, Namespaces, Deduplizierung, Pruning, Verify; **Restore-Test** | [PBS Doku](https://pbs.proxmox.com/docs/) · [PBS Wiki](https://pbs.proxmox.com/wiki/) |

**Definition of Done**
- [ ] VLAN-getrenntes Lab-Netz funktioniert nachweislich
- [ ] Firewall-Regelwerk greift (Test: geblockter vs. erlaubter Port)
- [ ] PBS läuft, automatischer Job aktiv, **Restore erfolgreich verifiziert**

---

## Sprint 4 (Woche 7–8): Cluster, HA & Ceph

**Sprintziel:** 3-Node-Cluster mit Live-Migration und Hochverfügbarkeit.

| Session | Inhalt | Quellen |
|---|---|---|
| **4.1** | Cluster-Konzepte: Corosync, Quorum, QDevice, Cluster-Netz trennen; 2. und 3. Node joinen | [Cluster Manager](https://pve.proxmox.com/wiki/Cluster_Manager) · [QDevice](https://pve.proxmox.com/pve-docs/pve-admin-guide.html#_corosync_external_vote_support) |
| **4.2** | Offline- und Live-Migration, Replikation (ZFS `pvesr`), Shared vs. Local Storage | [Storage Replication](https://pve.proxmox.com/wiki/Storage_Replication) · [Migration](https://pve.proxmox.com/pve-docs/pve-admin-guide.html#_migration) |
| **4.3** | Ceph-Grundlagen: MON/MGR/OSD, Pools, Replikationsfaktor, Hyper-Converged Setup | [Deploy Hyper-Converged Ceph Cluster](https://pve.proxmox.com/wiki/Deploy_Hyper-Converged_Ceph_Cluster) · [Ceph Docs](https://docs.ceph.com/en/latest/) |
| **4.4** | HA-Gruppen & Ressourcen, Fencing/Watchdog, **Failover-Test** (Node hart abschalten) | [High Availability](https://pve.proxmox.com/wiki/High_Availability) · [Fencing](https://pve.proxmox.com/wiki/Fencing) |

**Videos:** [Techno Tim](https://www.youtube.com/@TechnoTim) → „Proxmox Cluster / Ceph“ · [Jim's Garage](https://www.youtube.com/@Jims-Garage)

**Definition of Done**
- [ ] 3 Nodes im Cluster, Quorum stabil
- [ ] Live-Migration ohne spürbaren Ausfall durchgeführt
- [ ] HA-VM startet nach simuliertem Node-Ausfall automatisch auf einem anderen Node

---

## Sprint 5 (Woche 9–10): Automatisierung, Monitoring & Betrieb

**Sprintziel:** Reproduzierbares Setup per Code + belastbare Betriebsroutine.

| Session | Inhalt | Quellen |
|---|---|---|
| **5.1** | Proxmox-API verstehen: API-Tokens, Rechte, `pvesh`, REST-Aufrufe testen | [API Viewer](https://pve.proxmox.com/pve-docs/api-viewer/) · [Proxmox VE API Wiki](https://pve.proxmox.com/wiki/Proxmox_VE_API) |
| **5.2** | Terraform/OpenTofu: VMs aus Cloud-Init-Templates deklarativ ausrollen | [bpg/proxmox Provider](https://registry.terraform.io/providers/bpg/proxmox/latest/docs) · [OpenTofu](https://opentofu.org/docs/) |
| **5.3** | Ansible: Post-Provisioning, Node-Konfiguration, Inventory über Proxmox-Plugin | [community.general Proxmox-Module](https://docs.ansible.com/ansible/latest/collections/community/general/index.html#plugins-in-community-general) · [Ansible Docs](https://docs.ansible.com/ansible/latest/) |
| **5.4** | Monitoring & Betrieb: Metric Server (InfluxDB/Graphite), Grafana-Dashboard, Notifications, Logs, Patch-Routine, Upgrade-Pfad | [Admin Guide – External Metric Server](https://pve.proxmox.com/pve-docs/pve-admin-guide.html#external_metric_server) · [Notifications](https://pve.proxmox.com/pve-docs/pve-admin-guide.html#chapter_notifications) · [Upgrade-Guides im Wiki](https://pve.proxmox.com/wiki/Category:Upgrade) |

**Definition of Done**
- [ ] `terraform apply` erzeugt reproduzierbar eine lauffähige VM
- [ ] Ansible-Playbook konfiguriert diese VM vollständig ohne manuelle Schritte
- [ ] Grafana zeigt CPU/RAM/Storage der Nodes
- [ ] Du hast eine dokumentierte Runbook-Seite: Backup, Restore, Patching, Failover

---

## Plattform-Unterschiede im Überblick

| Aspekt | Windows | macOS |
|---|---|---|
| Lokales Nested-Lab | Gut möglich (Hyper-V / VMware Workstation) | Nur auf Intel-Macs sinnvoll; Apple Silicon → externer x86-Node |
| Cluster-Übungen (Sprint 4) | Lokal machbar bei ≥ 32 GB RAM | Praktisch nur mit externem Host / Cloud-Nodes |
| Terminal/SSH | Windows Terminal + OpenSSH / PuTTY | Nativ im Terminal |
| IaC-Umgebung | WSL2 empfohlen | Homebrew, nativ |
| ISO auf USB | Ventoy / Rufus | balenaEtcher / `dd` |

---

## Fortschrittskontrolle

- **Wöchentlich (15 Min am Ende von Session 2):** Was ist erledigt, was blockiert?
- **Am Sprintende:** Definition-of-Done-Checkliste abhaken. Nicht Erreichtes wandert an den Anfang des Folgesprints – Umfang lieber kürzen als Qualität.
- **Lab-Journal:** Jede Session in Markdown dokumentieren (Ziel, Befehle, Fehler, Lösung). Das wird später deine interne Betriebsdokumentation.
- **Puffer:** Sprint 3 und Sprint 4 erfahrungsgemäß am zeitintensivsten – dort ggf. eine Zusatzsession einplanen.

---

Wenn du möchtest, kann ich daraus eine **Checklisten-Datei (Markdown/TXT)**, eine **Word-Version** oder eine **Sprint-Übersicht als PowerPoint** erstellen – sag einfach kurz Bescheid, Michael.