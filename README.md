# konstruktiv-kritiker

> Stresstest deine Pläne, bevor sie scheitern.

Ein Claude-Skill, der Pläne, Launches, Einstellungen, Strategien und Entscheidungen kritisch hinterfragt – auf Basis der **Pre-Mortem-Methode** von Gary Klein (Harvard Business Review 2007).

**Live-Demo:** [Landingpage](https://godmodeai2025.github.io/konstruktiv-kritiker/) · **Inspiration:** Englischsprachiger `premortem`-Skill, hier deutsch adaptiert und erweitert.

---

## Was er tut

Claude tendiert standardmäßig zu zustimmenden, optimistischen Antworten. Dieser Skill durchbricht das Muster mit einem psychologischen Trick – dem Pre-Mortem-Frame:

> „Es ist 6 Monate in der Zukunft. Dein Vorhaben ist gescheitert. Wir schauen zurück und erklären, warum."

Forschung (Mitchell, Russo & Pennington, 1989) zeigt: Wer ein Ergebnis als bereits eingetreten annimmt, identifiziert Ursachen ca. 30 % besser als wer „was könnte schiefgehen?" fragt.

---

## Schnellstart

### Variante A · Manuell zippen (3 Schritte)

```bash
# 1. Repository klonen
git clone https://github.com/GodModeAI2025/konstruktiv-kritiker.git

# 2. Den Ordner als ZIP packen (WICHTIG: Skill-Ordner ist die ZIP-Wurzel)
cd konstruktiv-kritiker
zip -r ../konstruktiv-kritiker.skill . -x ".git/*" "index.html"

# 3. In Claude.ai hochladen unter: Customize > Skills > +
```

### Variante B · `package_skill.py` von Anthropic

```bash
# Skill-Creator von Anthropic (enthält package_skill.py) installieren, dann:
python package_skill.py /pfad/zu/konstruktiv-kritiker

# Erzeugt konstruktiv-kritiker.skill im Output-Verzeichnis
# Upload in Claude.ai unter Customize > Skills
```

### Variante C · Claude Code

```bash
# In Claude Code: Skill direkt in das Skills-Verzeichnis kopieren
cp -r konstruktiv-kritiker ~/.claude/skills/
```

Dann ist der Skill in jeder Claude-Code-Session automatisch verfügbar.

---

## Trigger

Der Skill aktiviert sich auf folgende Phrasen (Auswahl):

**Pflicht-Trigger:** „kritisch hinterfragen", „konstruktive Kritik", „Schwachstellen finden", „blinde Flecken aufdecken", „was übersehe ich", „stresstest mein", „zukunftssicher machen", „Pre-Mortem dazu", „spiel Advocatus Diaboli"

**Starke Trigger:** „was könnte schiefgehen", „wo bricht das", „was könnte das killen", „Risiken aufdecken", „Plan stresstesten"

---

## Struktur

```
konstruktiv-kritiker/
├── SKILL.md                          # Hauptanleitung (161 Zeilen)
├── README.md                         # Dieses File
├── index.html                        # Landingpage (GitHub Pages)
└── references/
    ├── sub-agent-prompt.md           # Prompt-Template für Deep-Dives
    ├── html-template.md              # HTML-Report-Skeleton
    ├── beispiel-lauf.md              # Vollständiger Beispiel-Lauf
    ├── fruehwarnung-buch.md          # Domänen-Cheatsheet: Buchprojekte
    ├── fruehwarnung-produkt.md       # Domänen-Cheatsheet: Produkt-Launches
    ├── fruehwarnung-hire.md          # Domänen-Cheatsheet: Einstellungen
    └── fruehwarnung-strategie.md     # Domänen-Cheatsheet: Strategie-Pivots
```

---

## Workflow (6 Schritte)

1. **Frame setzen** – „Es ist 6 Monate in der Zukunft, das Vorhaben ist gescheitert"
2. **Roh-Fehlergründe generieren** – Jeden ernsthaften Failure Mode auflisten
3. **Deep-Dives parallel** – Pro Fehlergrund ein Sub-Agent mit Fehlergeschichte, Annahme, Frühwarnzeichen
4. **Synthese** – Wahrscheinlichster Fehler / Gefährlichster Fehler / Versteckte Annahme / Überarbeiteter Plan / Pre-Launch-Checkliste
5. **HTML-Report generieren** – `kritik-report-[timestamp].html`
6. **Markdown-Transkript speichern** – `kritik-transcript-[timestamp].md`

---

## Mindestschwelle (4-Punkte-Check)

Bevor der Skill startet, validiert er:

1. **Was ist es?** – In einem Satz beschreibbar
2. **Für wen / wen betrifft es?** – Zielgruppe, Stakeholder
3. **Ausgangsposition** – Mit harten Zahlen, nicht „so mittel"
4. **SMART-Erfolg** – Specific, Measurable, Achievable, Relevant, Time-bound

Ohne alle vier Punkte ist die Pre-Mortem zu vage. Der Skill fragt gezielt nach.

---

## Quellen & Inspiration

Dieser Skill ist die deutsche Adaption und Erweiterung eines englischsprachigen `premortem`-Skills. Übersetzung sprachlich auf den deutschen Fachbuch- und Unternehmenskontext zugeschnitten; Methodik und Mechanik bleiben dem Original treu.

- **Methode:** Gary Klein, *„Performing a Project Premortem"*, Harvard Business Review, September 2007
- **Bekanntheit:** Daniel Kahneman, *Thinking, Fast and Slow* (2011) – beschreibt die Technik als seine wertvollste Entscheidungstechnik
- **Empirie:** Mitchell, Russo & Pennington (1989), *Journal of Behavioral Decision Making* – ca. 30 % bessere Ursachen-Identifikation durch *prospective hindsight*

---

## Lizenz

MIT-Lizenz – freie Nutzung, Anpassung, Weitergabe.

---

## Architektur-Entscheidungen

Größere strukturelle Entscheidungen werden als ADRs (Architectural Decision Records) im MADR-Format dokumentiert:

- [ADR-0001: Erzeugung und Distribution der `.skill`-Datei](docs/adr/0001-skill-package-distribution.md) — Hybrid-Ansatz aus CI-Build, pre-built `.skill` im Repo und manueller Fallback-Anleitung

---

## Beitragen

Issues und Pull Requests willkommen. Vor allem geschätzt:

- Weitere Domänen-Cheatsheets (z. B. M&A, Forschungsanträge, Bildungsangebote)
- Übersetzungen (Englisch zurück, Französisch, Spanisch)
- Reale Anwendungsfälle als Case Studies
