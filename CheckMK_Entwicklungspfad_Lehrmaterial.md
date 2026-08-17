# Lehrmaterial zum Selbstschulungsplan Checkmk

**Hinweis vorab:** Die folgenden Quellen sind öffentlich verfügbare Materialien des Herstellers und der Community. Ich kann die URLs hier nicht live prüfen – Checkmk strukturiert die Dokumentation gelegentlich um. Sollte ein Link ins Leere laufen, hilft die Volltextsuche unter `docs.checkmk.com`. Bitte zusätzlich beachten, ob der Zugriff auf YouTube und externe Portale aus dem DZ BANK Netz möglich ist bzw. welche internen Vorgaben dafür gelten – dazu liegen mir keine Informationen vor.

**Dauerhafte Basisquellen (für alle Sessions)**

| Quelle | Link |
|---|---|
| Offizielles Handbuch (deutsch) | https://docs.checkmk.com/latest/de/ |
| Offizielles Handbuch (englisch, oft aktueller) | https://docs.checkmk.com/latest/en/ |
| Checkmk YouTube-Kanal / „Checkmk Academy" | https://www.youtube.com/@checkmk-channel |
| Community-Forum | https://forum.checkmk.com/ |
| Checkmk Exchange (Plugins) | https://exchange.checkmk.com/ |
| Werks / Release Notes | https://checkmk.com/werks |
| Kostenlose Webinare & Guided Trials | https://checkmk.com/webinars |

---

## Vorbereitung

| Material | Link |
|---|---|
| Übersicht: Welche Edition passt? | https://checkmk.com/product/editions |
| Download Raw Edition | https://checkmk.com/download |
| Hardware-/Sizing-Empfehlungen | https://docs.checkmk.com/latest/de/cmc_differences.html · https://checkmk.com/blog (Suchbegriff „sizing") |
| Erste Schritte / Einstiegsseite Handbuch | https://docs.checkmk.com/latest/de/intro_welcome.html |

---

## Sprint 1 – Grundlagen & Installation

**Session 1.1 – Architektur & Installation**

| Typ | Material | Link |
|---|---|---|
| Doku | Checkmk installieren (Debian/Ubuntu) | https://docs.checkmk.com/latest/de/install_packages_debian.html |
| Doku | Grundlagen der Instanzverwaltung (OMD) | https://docs.checkmk.com/latest/de/omd_basics.html |
| Doku | Die Architektur von Checkmk | https://docs.checkmk.com/latest/de/arch_overview.html |
| Doku | Benutzerverwaltung & Rollen | https://docs.checkmk.com/latest/de/wato_user.html |
| Video | YouTube-Suche: „Checkmk installation Linux getting started" auf dem offiziellen Kanal | https://www.youtube.com/@checkmk-channel |
| Guided Tour | Interaktive Produkt-Tour / Trial-Guide | https://checkmk.com/product/guided-tour |

**Session 1.2 – Erste Hosts & Services**

| Typ | Material | Link |
|---|---|---|
| Doku | Einstieg: Monitoring einrichten | https://docs.checkmk.com/latest/de/intro_setup_monitor.html |
| Doku | Linux-Agent | https://docs.checkmk.com/latest/de/agent_linux.html |
| Doku | Windows-Agent | https://docs.checkmk.com/latest/de/agent_windows.html |
| Doku | Hosts verwalten | https://docs.checkmk.com/latest/de/wato_hosts.html |
| Doku | Service-Erkennung (Discovery) | https://docs.checkmk.com/latest/de/wato_services.html |
| Doku | Grundlagen des Monitorings / Statuszustände | https://docs.checkmk.com/latest/de/monitoring_basics.html |
| Video | Playlist „Checkmk Academy – Getting started" | https://www.youtube.com/@checkmk-channel/playlists |

---

## Sprint 2 – Konfiguration & Regelwerk

**Session 2.1 – Ordner, Hosts, Tags**

| Typ | Material | Link |
|---|---|---|
| Doku | Ordner & Vererbung (Teil von „Hosts verwalten") | https://docs.checkmk.com/latest/de/wato_hosts.html |
| Doku | Host-Merkmale (Host-Tags) | https://docs.checkmk.com/latest/de/host_tags.html |
| Doku | Labels | https://docs.checkmk.com/latest/de/labels.html |
| Blog | „How to structure your Checkmk configuration" – Suche im Blog | https://checkmk.com/blog |

**Session 2.2 – Regeln & Schwellwerte**

| Typ | Material | Link |
|---|---|---|
| Doku | Regeln – das zentrale Konfigurationskonzept | https://docs.checkmk.com/latest/de/wato_rules.html |
| Doku | Dateisysteme überwachen (Schwellwerte, Trends) | https://docs.checkmk.com/latest/de/monitoring_filesystems.html |
| Doku | Periodische Service-Erkennung | https://docs.checkmk.com/latest/de/wato_services.html |
| Video | YouTube-Suche: „Checkmk rule based configuration" | https://www.youtube.com/@checkmk-channel |
| Forum | Kategorie „Configuration" für Praxisfälle | https://forum.checkmk.com/c/checkmk/ |

---

## Sprint 3 – Benachrichtigungen & Zeitsteuerung

**Session 3.1 – Notification-Pipeline**

| Typ | Material | Link |
|---|---|---|
| Doku | Benachrichtigungen (Hauptartikel) | https://docs.checkmk.com/latest/de/notifications.html |
| Doku | Kontaktgruppen & Zuständigkeiten | https://docs.checkmk.com/latest/de/wato_user.html |
| Doku | E-Mail-Versand einrichten / Mailversand | https://docs.checkmk.com/latest/de/notifications.html#mail |
| Doku | Eigene Benachrichtigungsskripte | https://docs.checkmk.com/latest/de/notifications.html#scripts |
| Video | YouTube-Suche: „Checkmk notifications setup" | https://www.youtube.com/@checkmk-channel |

**Session 3.2 – Zeiten & Dämpfung**

| Typ | Material | Link |
|---|---|---|
| Doku | Zeitperioden | https://docs.checkmk.com/latest/de/timeperiods.html |
| Doku | Wartungszeiten (Downtimes) | https://docs.checkmk.com/latest/de/basics_downtimes.html |
| Doku | Quittieren von Problemen (Acknowledgement) | https://docs.checkmk.com/latest/de/basics_ackn.html |
| Doku | Netzwerk-Topologie / Parents | https://docs.checkmk.com/latest/de/monitoring_network.html |
| Doku | Flapping & Check-Parameter | https://docs.checkmk.com/latest/de/monitoring_basics.html |

---

## Sprint 4 – Erweiterte Datenquellen

**Session 4.1 – SNMP & aktive Checks**

| Typ | Material | Link |
|---|---|---|
| Doku | SNMP-Monitoring | https://docs.checkmk.com/latest/de/snmp.html |
| Doku | Aktive Checks | https://docs.checkmk.com/latest/de/active_checks.html |
| Doku | HTTP/HTTPS-Monitoring & Zertifikate | https://docs.checkmk.com/latest/de/active_checks_httpv2.html |
| Doku | Netzwerk-Interfaces überwachen | https://docs.checkmk.com/latest/de/monitoring_network.html |
| Tool | SNMP-Simulator (snmpsim) für Übungen | https://github.com/lextudio/snmpsim |
| Video | YouTube-Suche: „Checkmk SNMP monitoring" | https://www.youtube.com/@checkmk-channel |

**Session 4.2 – Agent-Erweiterungen**

| Typ | Material | Link |
|---|---|---|
| Doku | Lokale Checks (Local Checks) | https://docs.checkmk.com/latest/de/localchecks.html |
| Doku | Agent-Plugins / Agent erweitern | https://docs.checkmk.com/latest/de/agent_linux.html#plugins |
| Doku | Logdateien überwachen (mk_logwatch) | https://docs.checkmk.com/latest/de/logwatch.html |
| Doku | Piggyback-Daten | https://docs.checkmk.com/latest/de/piggyback.html |
| Doku | Agent Bakery (Enterprise, theoretisch) | https://docs.checkmk.com/latest/de/agent_deployment.html |
| Community | Fertige Plugins als Vorlage | https://exchange.checkmk.com/ |
| Video | YouTube-Suche: „Checkmk local check plugin" | https://www.youtube.com/@checkmk-channel |

---

## Sprint 5 – Auswertung, Automatisierung, API

**Session 5.1 – Graphen, Views, Reporting**

| Typ | Material | Link |
|---|---|---|
| Doku | Messwerte & Graphen | https://docs.checkmk.com/latest/de/graphing.html |
| Doku | Ansichten (Views) | https://docs.checkmk.com/latest/de/views.html |
| Doku | Dashboards | https://docs.checkmk.com/latest/de/dashboards.html |
| Doku | Verfügbarkeit (Availability) | https://docs.checkmk.com/latest/de/availability.html |
| Doku | Reporting (Enterprise) | https://docs.checkmk.com/latest/de/reporting.html |
| Video | YouTube-Suche: „Checkmk dashboards and views" | https://www.youtube.com/@checkmk-channel |

**Session 5.2 – REST-API & Automatisierung**

| Typ | Material | Link |
|---|---|---|
| Doku | REST-API (Konzept & Nutzung) | https://docs.checkmk.com/latest/de/rest_api.html |
| Doku | Interaktive API-Referenz der eigenen Site | `https://<server>/<site>/check_mk/api/doc/` |
| Doku | Kommandozeile: `cmk`-Befehle | https://docs.checkmk.com/latest/de/cmk_commandline.html |
| Doku | Livestatus (lesender Zugriff) | https://docs.checkmk.com/latest/de/livestatus.html |
| Ansible | Offizielle Ansible Collection | https://galaxy.ansible.com/ui/repo/published/checkmk/general/ |
| GitHub | Ansible Collection Quellcode & Beispiele | https://github.com/Checkmk/ansible-collection-checkmk.general |
| Doku | Dynamische Host-Konfiguration (DCD, Enterprise) | https://docs.checkmk.com/latest/de/dcd.html |
| Video | YouTube-Suche: „Checkmk REST API" / „Checkmk Ansible" | https://www.youtube.com/@checkmk-channel |

---

## Sprint 6 – Betrieb, Härtung & Abschlussprojekt

**Session 6.1 – Betrieb & Troubleshooting**

| Typ | Material | Link |
|---|---|---|
| Doku | Backup & Restore | https://docs.checkmk.com/latest/de/backup.html |
| Doku | Updates & Upgrades | https://docs.checkmk.com/latest/de/update.html |
| Doku | Verteiltes Monitoring | https://docs.checkmk.com/latest/de/distributed_monitoring.html |
| Doku | Der Microcore (CMC) & Performance | https://docs.checkmk.com/latest/de/cmc.html |
| Doku | Analyse der Konfiguration / Troubleshooting | https://docs.checkmk.com/latest/de/analyze_configuration.html |
| Doku | HTTPS für die Weboberfläche | https://docs.checkmk.com/latest/de/omd_https.html |
| Doku | LDAP-/AD-Anbindung | https://docs.checkmk.com/latest/de/ldap.html |
| Doku | Sicherheit / Härtung | https://docs.checkmk.com/latest/de/security.html |
| Support | Diagnose-Dump erstellen | https://docs.checkmk.com/latest/de/support_diagnostics.html |

**Session 6.2 – Abschlussprojekt**
Kein neues Lehrmaterial – bewusst ohne Anleitung arbeiten. Als Referenz nur:
- Eigenes Lernjournal aus Sprint 1–5
- Handbuch-Volltextsuche: https://docs.checkmk.com/latest/de/

---

## Optionale Erweiterungen (nach Woche 12)

| Thema | Link |
|---|---|
| Event Console (Syslog / SNMP-Traps) | https://docs.checkmk.com/latest/de/ec.html |
| Kubernetes-Monitoring | https://docs.checkmk.com/latest/de/monitoring_kubernetes.html |
| VMware / ESXi | https://docs.checkmk.com/latest/de/monitoring_vmware.html |
| AWS / Azure / GCP | https://docs.checkmk.com/latest/de/monitoring_aws.html · `monitoring_azure.html` · `monitoring_gcp.html` |
| Grafana-Integration | https://docs.checkmk.com/latest/de/grafana.html |
| Prometheus-Integration | https://docs.checkmk.com/latest/de/monitoring_prometheus.html |
| Eigene Check-Plugins entwickeln | https://docs.checkmk.com/latest/de/devel_intro.html |
| Offizielle Schulungen & Zertifizierung | https://checkmk.com/training |

---

Wenn du möchtest, exportiere ich den vollständigen Plan inklusive dieser Linksammlung als Word- oder Textdatei, oder ergänze pro Session eine Spalte mit geschätzter Lesezeit. Sag einfach Bescheid.