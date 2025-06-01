# Abschlussprojekt IHK - Evaluation von Proxmox

Dieses Repository dokumentiert mein Abschlussprojekt zum Fachinformatiker für Systemintegration (IHK Dortmund, Winter 2024).  
Ziel war die Evaluation von Proxmox als Ersatz oder Ergänzung zu Microsoft Hyper-V.

---

## Inhalt

- [Projektbeschreibung](#projektbeschreibung)
- [Testumgebung](#testumgebung)
- [Testergebnisse](#testergebnisse)
- [Fazit](#fazit)

## Projektbeschreibung

Hyper-V bereitete aufgrund der Benutzerverwaltung und der Hardwareanforderungen Probleme.  
Ziel war es, Proxmox hinsichtlich folgender Punkte zu evaluieren:

- Benutzerverwaltung inkl. Active Directory Anbindung
- Plattformunabhängige Verwaltung
- Kompatibilität mit älterer Hardware
- Performancevergleich zu Hyper-V
- Unterstützung von Nested Virtualisierung

## Testumgebung

- 2 Office-PCs (Intel i3 CPU, 8GB RAM, 500GB SSD)
- Netzwerk mit eigenem VLAN
- Installation von Proxmox, Hyper-V, Windows Server 2019 und Ubuntu 20.04

## Testergebnisse

- Proxmox bietet umfangreiche Benutzerverwaltung (lokal + AD)
- Nested Virtualisierung wird unterstützt
- Bessere Performance als Hyper-V auf älterer Hardware
- Verwaltung über Webbrowser auf allen Plattformen möglich

## Fazit

Proxmox ist ein starker Kandidat als Ersatz oder Ergänzung für Hyper-V in IT-Schulungsumgebungen.

---

#
