# Frühwarnzeichen – IT-Migration / Systemwechsel

Domänen-Cheatsheet für Vorhaben rund um Cloud-Migration, ERP-Rollouts, Legacy-Ablösung, Plattformwechsel, Datenbank-Migration, Tool-Konsolidierung. Lade dieses File in die Roh-Analyse als Inspiration für domänentypische Failure Modes.

## Scope & Planung

- **Scope** wächst nach Projektstart – „wenn wir schon migrieren, dann auch gleich X und Y"
- **Bestandsaufnahme** des Altsystems unvollständig – undokumentierte Integrationen tauchen während der Migration auf
- **Abhängigkeiten** zwischen Systemen nicht kartiert – Migration von System A bricht System B
- **Zeitplan** basiert auf Herstellerangaben, nicht auf eigener Erfahrung oder Pilotierung
- **Rollback-Strategie** existiert nicht oder wurde nie getestet
- **Parallelbetrieb** (alt + neu gleichzeitig) nicht eingeplant oder nicht finanziert

## Datenmigration

- **Datenqualität** im Altsystem unzureichend – Bereinigung vor Migration nicht eingeplant
- **Mapping** der Datenfelder zwischen Alt und Neu unvollständig
- **Historische Daten** sollen vollständig migriert werden, obwohl nur ein Bruchteil benötigt wird
- **Testmigration** mit Echtdaten nicht durchgeführt – nur mit Testdaten validiert
- **Datenverlust** in der Migration erst Wochen später bemerkt, weil niemand die Vollständigkeit prüft
- **Performance** des neuen Systems mit realer Datenmenge nicht getestet

## Nutzer:innen-Akzeptanz

- **Change-Management** beschränkt sich auf eine E-Mail und ein PDF-Handbuch
- **Schulungen** finden statt, aber Wochen vor dem Go-Live – Wissen ist beim Start vergessen
- **Power-User** des Altsystems wurden nicht in die Auswahl einbezogen
- **Workarounds** im Altsystem haben sich als informelle Prozesse etabliert – das neue System bildet sie nicht ab
- **Beschwerden** häufen sich in den ersten 2 Wochen – „Vorher ging das einfacher"
- **Shadow-IT** entsteht: Teams nutzen weiterhin das Altsystem oder Excel als Parallellösung

## Technische Risiken

- **Integrationen** (APIs, Schnittstellen, Middleware) sind der Engpass, nicht die Kernsysteme
- **Customizations** im Altsystem wurden über Jahre aufgebaut – Nachbau im Neusystem teurer als gedacht
- **Performance** unter Last nicht getestet – System kollabiert am ersten Arbeitstag
- **Sicherheitsanforderungen** im neuen System nicht äquivalent zum alten (Berechtigungen, Rollen, Audit-Logs)
- **Vendor-Lock-in** durch proprietäre Formate oder Verträge im neuen System
- **Monitoring** und Alerting für das neue System nicht rechtzeitig aufgesetzt

## Organisation & Stakeholder

- **Projektleitung** hat keine Entscheidungskompetenz – jede Änderung braucht Steering-Committee-Freigabe
- **Fachbereiche** betrachten die Migration als IT-Projekt und beteiligen sich nicht aktiv
- **Externe Dienstleister** haben Anreize, den Scope zu vergrößern, nicht zu begrenzen
- **Go-Live-Termin** ist politisch gesetzt, nicht an Readiness-Kriterien geknüpft
- **Budget-Überziehung** wird zu spät eskaliert – Steering Committee erfährt es nach Faktor 2x
- **Wissensträger:innen** des Altsystems verlassen das Unternehmen während der Migration

## Klassische Migrations-Fallen

- **„Wir migrieren 1:1"** – eine 1:1-Migration ist die teuerste und riskanteste Variante. Jede Migration ist eine Chance zu vereinfachen.
- **„Der Hersteller sagt 6 Monate"** – Hersteller kalkulieren den Happy Path. Reale Migrationen dauern 2–3x länger.
- **„Das neue System kann alles, was das alte kann"** – es kann anderes. Die Lücken zeigen sich im Alltag, nicht in der Demo.
- **„Die Datenmigration ist der einfache Teil"** – sie ist fast immer der schwierigste, zeitaufwändigste und fehleranfälligste Teil.
- **„Nach dem Go-Live sind wir fertig"** – nach dem Go-Live beginnt die Stabilisierungsphase, die 3–6 Monate dauert.

## Typische versteckte Annahmen

- „Die Daten im Altsystem sind korrekt und vollständig."
- „Nutzer:innen akzeptieren das neue System, sobald sie es kennenlernen."
- „Parallelbetrieb ist optional." (Er ist fast immer notwendig.)
- „Der externe Dienstleister kennt unsere Prozesse." (Er kennt sein Produkt.)
- „Ein erfolgreicher Pilotbereich beweist, dass der Rollout klappt."

## Eskalations-Indikatoren

Wenn 3+ dieser Zeichen gleichzeitig auftreten, ist ein Go-Live-Readiness-Review Pflicht:
- Datenmigration noch nicht mit Echtdaten getestet
- Schulungen nicht abgeschlossen oder zu lange her
- Offene Blocker-Tickets im zweistelligen Bereich
- Rollback-Strategie existiert nicht oder wurde nicht getestet
