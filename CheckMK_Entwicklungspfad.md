# Entwicklungspfad Checkmk

**Format:** 2 × 2 Stunden pro Woche (z. B. Di & Do) · **Dauer:** 12 Wochen / 6 Sprints à 2 Wochen · **Gesamtaufwand:** ca. 48 h
**Start:** KW 34 (ab 18.08.2026) · **Zielbild:** eigenständiger Betrieb, Konfiguration und Erweiterung einer Checkmk-Umgebung

---

## 0. Vorbereitung (einmalig, vor Sprint 1 – ca. 1 h)

| Punkt | Umsetzung |
|---|---|
| Lab-Umgebung | 1 VM „cmk-server" (Debian 12 / Ubuntu LTS, 4 vCPU, 8 GB RAM), 2–3 Test-Hosts (1 × Linux, 1 × Windows, 1 × SNMP-Gerät oder Simulation) |
| Edition | Checkmk Raw Edition (freie Version) – für Enterprise-Features ggf. Trial-Lizenz |
| Doku-Basis | Offizielles Handbuch (docs.checkmk.com), Checkmk YouTube-Kanal, Community-Forum |
| Lernjournal | Ein Git-Repo oder OneNote/Confluence-Seite: pro Session Notizen, Befehle, Screenshots, offene Fragen |
| Backup | VM-Snapshot nach jedem Sprint → ermöglicht risikofreies „Kaputtmachen" |

> **Hinweis:** Bitte vorab prüfen, ob für das Lab interne Vorgaben (Betriebsmittel, Netzsegment, Softwarefreigabe) gelten – dazu kann ich hier keine verbindliche Auskunft geben.

---

## Sprint 1 (Woche 1–2): Grundlagen & Installation

**Sprintziel:** Lauffähige Checkmk-Site mit ersten überwachten Hosts.

**Session 1.1 – Architektur & Installation (2 h)**
- 45 min Theorie: Site-Konzept (OMD), Core (CMC/Nagios), Checkmk-Agent, Datenfluss, Editions-Unterschiede
- 75 min Praxis: Paket installieren, `omd create/start`, Weboberfläche, Benutzerverwaltung, Passwortrichtlinie

**Session 1.2 – Erste Hosts & Services (2 h)**
- Agent auf Linux- und Windows-Host ausrollen
- Host anlegen, Service Discovery, „Activate Changes"-Workflow verstehen
- Grundlagen der GUI: Views, Dashboards, Status-Farben

**Übungen zur Vertiefung**
1. Zweite Site (`omd create test`) anlegen und parallel betreiben.
2. Site stoppen/starten/löschen, Verzeichnisstruktur `/omd/sites/<site>` dokumentieren.
3. 3 Hosts vollständig aufnehmen, Discovery-Ergebnis in eigenen Worten erklären.

**Definition of Done:** Alle Testhosts sind grün, du kannst den Weg „Agent → Server → GUI" ohne Doku erklären.

---

## Sprint 2 (Woche 3–4): Konfiguration & Regelwerk

**Sprintziel:** Sicherer Umgang mit dem regelbasierten Konfigurationskonzept.

**Session 2.1 – Ordner, Hosts, Tags (2 h)**
- Ordnerhierarchie als Vererbungsstruktur
- Host-Tags, Labels, Host-Attribute
- Sinnvolle Ordnungsstruktur entwerfen (z. B. Standort / Umgebung / Systemtyp)

**Session 2.2 – Regeln & Schwellwerte (2 h)**
- Regelketten, Reihenfolge, Bedingungen, „Effective parameters" analysieren
- Schwellwerte für Filesystem, CPU, Memory anpassen
- Services deaktivieren, Service-Beschreibungen anpassen, periodische Discovery

**Übungen zur Vertiefung**
1. Filesystem-Warnschwelle nur für Hosts mit Tag `prod` auf 85/95 % setzen.
2. Bewusst eine widersprüchliche Regel bauen und mit „Effective parameters" die Wirkung nachweisen.
3. Ordnerstruktur für ein fiktives Rechenzentrum mit 50 Hosts modellieren (auf Papier + im Tool).

**DoD:** Du kannst begründen, warum eine bestimmte Regel greift oder nicht.

---

## Sprint 3 (Woche 5–6): Benachrichtigungen & Zeitsteuerung

**Sprintziel:** Funktionierendes, nachvollziehbares Alarmierungskonzept.

**Session 3.1 – Notification-Pipeline (2 h)**
- Kontakte, Kontaktgruppen, Rollen/Berechtigungen
- Notification Rules, Fallback-Kontakt, Mail-Versand (lokaler MTA oder Test-SMTP)
- Eskalationen und Wiederholungen

**Session 3.2 – Zeiten & Dämpfung (2 h)**
- Timeperiods (Geschäftszeit vs. 24/7)
- Downtimes (geplant/spontan), Acknowledgements, Kommentare
- Flapping, „Max check attempts", Parent-Hosts & Netzwerktopologie zur Alarmunterdrückung

**Übungen zur Vertiefung**
1. Alarme für Tag-`test`-Hosts nur Mo–Fr 08–18 Uhr, für `prod` rund um die Uhr.
2. Eskalation bauen: nach 30 min unquittiert → zweite Kontaktgruppe.
3. Parent-Host definieren, Router-Ausfall simulieren, Ergebnis: nur 1 Alarm statt 10.
4. Wartungsfenster per Kommandozeile/API setzen.

**DoD:** Ein Testalarm durchläuft nachweislich die gewünschte Kette (Notification-Log auswerten).

---

## Sprint 4 (Woche 7–8): Erweiterte Datenquellen

**Sprintziel:** Über den Standard-Agent hinaus überwachen.

**Session 4.1 – SNMP & aktive Checks (2 h)**
- SNMP v2c/v3, Community/Credentials, SNMP-Walk, Auto-Detection
- Aktive Checks: HTTP(S), TCP-Port, Ping, Zertifikatsablauf
- `check_http` / `check_cert` praktisch konfigurieren

**Session 4.2 – Agent-Erweiterungen (2 h)**
- Local Checks (eigenes Skript in `/usr/lib/check_mk_agent/local`)
- Agent Plugins (z. B. MySQL, Apache, `mk_logwatch`)
- Piggyback-Prinzip, Agent Bakery (nur Enterprise – theoretisch behandeln)

**Übungen zur Vertiefung**
1. Local Check in Bash schreiben, der die Anzahl angemeldeter User meldet (OK/WARN/CRIT + Perfdata).
2. Logfile-Überwachung: definiertes Muster in `/var/log/syslog` erzeugt CRIT.
3. Zertifikatsprüfung einer internen URL inkl. Warnung 30 Tage vor Ablauf.
4. SNMP-Gerät (oder Simulator) aufnehmen und Interface-Monitoring konfigurieren.

**DoD:** Mindestens ein eigener Check liefert korrekte Statuswerte inkl. Graph.

---

## Sprint 5 (Woche 9–10): Auswertung, Automatisierung, API

**Sprintziel:** Daten nutzbar machen und Konfiguration automatisieren.

**Session 5.1 – Graphen, Views, Reporting (2 h)**
- RRD-Datenhaltung, Performance-Daten, Custom Graphs
- Eigene Views und Dashboards bauen, Filter, Sortierung
- Verfügbarkeitsberichte (Availability), Event-Historie, SLA-Gedanke

**Session 5.2 – REST-API & Automatisierung (2 h)**
- Automation-User anlegen, REST-API-Doku im eigenen Server nutzen
- Hosts per `curl`/Python anlegen, Discovery und Activate Changes automatisieren
- Ausblick: Ansible-Modul, Dynamic Configuration Daemon (Enterprise)

**Übungen zur Vertiefung**
1. Skript: 10 Hosts aus CSV per REST-API anlegen, Discovery ausführen, aktivieren.
2. Dashboard „Betriebsübersicht" mit Top-10-CPU, offenen Problemen, Alarmhistorie.
3. Verfügbarkeitsreport für einen Host über 7 Tage erzeugen und interpretieren.

**DoD:** Host-Anlage läuft vollständig skriptgesteuert und idempotent.

---

## Sprint 6 (Woche 11–12): Betrieb, Härtung & Abschlussprojekt

**Sprintziel:** Betriebsreife nachweisen.

**Session 6.1 – Betrieb & Troubleshooting (2 h)**
- Backup/Restore einer Site, Update-/Upgrade-Pfade (`omd update`)
- Logs: `~/var/log/`, `cmk -D`, `cmk -vvI`, `cmc.log`, Debugging fehlender Services
- Performance-Tuning: Check-Intervalle, Helper-Anzahl, Skalierung / verteiltes Monitoring (Konzept)
- Härtung: HTTPS, LDAP/SSO-Anbindung (konzeptionell), Berechtigungskonzept

**Session 6.2 – Abschlussprojekt (2 h)**
Aufbau einer „produktionsnahen" Mini-Umgebung von Grund auf, ohne Anleitung:
- Ordner-/Tag-Konzept, ≥ 5 Hosts unterschiedlicher Typen
- Regelwerk mit differenzierten Schwellwerten
- Alarmierung mit Eskalation und Geschäftszeiten
- 1 eigener Local Check, 1 aktiver Check
- Dashboard + Availability-Report
- Backup erstellen und Restore in neuer Site testen

**DoD:** Restore erfolgreich, Dokumentation im Lernjournal vollständig, Umgebung ist einem Kollegen in 15 min erklärbar.

---

## Wochenrhythmus (Empfehlung pro 2-h-Block)

| Zeit | Inhalt |
|---|---|
| 0:00–0:10 | Rückblick: letzte Session, offene Punkte |
| 0:10–0:45 | Theorie / Doku-Lesen zum Thema |
| 0:45–1:45 | Praxis im Lab |
| 1:45–2:00 | Lernjournal aktualisieren, nächste Übung festlegen |

**Sprint-Review (15 min am Ende jedes Sprints):** DoD prüfen, unerledigte Übungen in den Folgesprint übernehmen, Snapshot ziehen.

---

## Optionale Erweiterungen (nach Woche 12)

- Verteiltes Monitoring mit Remote-Sites
- Event Console (Syslog/SNMP-Traps)
- Kubernetes-, Cloud- oder VMware-Monitoring
- Grafana-Anbindung, Prometheus-Integration
- Zertifizierung: „Checkmk Certified Professional" als Zielmarke

---

Wenn du möchtest, erstelle ich dir daraus eine Wochenübersicht mit konkreten Kalenderdaten als Word- oder Textdatei – sag einfach Bescheid.