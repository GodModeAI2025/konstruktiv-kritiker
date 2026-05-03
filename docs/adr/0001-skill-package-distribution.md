# ADR-0001 — Erzeugung und Distribution der `.skill`-Datei

| Feld           | Wert                                              |
|----------------|---------------------------------------------------|
| **Status**     | Akzeptiert                                        |
| **Datum**      | 2026-05-03                                        |
| **Autor**      | Mark Zimmermann                                   |
| **Betrifft**   | Build- und Distributions-Pipeline des Skills      |
| **Format**     | MADR (Markdown Architectural Decision Records)    |

---

## Kontext und Problembeschreibung

Der `konstruktiv-kritiker`-Skill liegt im Source-Repository als Folder mit `SKILL.md` und `references/` vor. Für die Distribution in Claude.ai wird gemäß der [Anthropic-Spezifikation](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) eine `.skill`-Datei benötigt — technisch ein ZIP-Archiv mit dem Skill-Folder als Wurzel (nicht als Unterordner).

Damit stellen sich zwei verbundene Fragen:

1. **Wie wird die `.skill`-Datei erzeugt?** (Tooling, Reproduzierbarkeit)
2. **Wie wird sie aktuell gehalten?** (Drift zwischen Source und Distribution)

Die Antwort beeinflusst direkt das primäre Skill-Ziel — Adoption durch externe Nutzer:innen — weil die Installations-Hürde laut Pre-Mortem (FM3 *Sharing-Mechanik unausgereift*) einer der zentralen Adoptions-Killer ist.

---

## Entscheidungstreiber

- **Niedrige Adoptionshürde** für externe Nutzer:innen: idealerweise „Download → Upload in Claude.ai → fertig"
- **Reproduzierbarkeit** des Build-Outputs (gleicher Source ⇒ gleiche `.skill`)
- **Drift-Freiheit** zwischen Source-Folder und committed `.skill`
- **Minimaler Maintainer-Aufwand** (Solo-Maintainer, vgl. Pre-Mortem FM4 *Aufmerksamkeits-Konkurrenz*)
- **Offline-/Custom-Builds** für Entwickler:innen, die forken oder anpassen wollen
- **Spec-Konformität** mit der Anthropic-Skill-Spezifikation (Skill-Folder als ZIP-Wurzel, nicht als Unterordner)

---

## Erwogene Optionen

### Option A — Manuelle `zip`-Anleitung in der README
Nur Dokumentation, keine vorgefertigte `.skill` im Repo. Nutzer:innen führen `zip -r konstruktiv-kritiker.skill SKILL.md references/` selbst aus.

### Option B — Pre-built `.skill` manuell ins Repo committen
Maintainer baut die `.skill` lokal und committet sie regelmäßig. Convenience-Download für Nutzer:innen.

### Option C — `package_skill.py` von Anthropic
Anthropic-Standard-Tool aus dem Skill-Creator. Validiert Skill-Struktur automatisch. Erfordert Python-Setup.

### Option D — Custom Build-Script (Bash/Makefile)
Projektspezifisches Script (`build.sh` oder `Makefile`), das `zip` mit den richtigen Excludes orchestriert. Teil des Repos.

### Option E — GitHub Actions Workflow (CI)
Bei jedem Push auf `main` wird die `.skill` neu gebaut und entweder committet oder als Release-Asset publiziert. Vollautomatisch.

### Option F — Hybrid: GitHub Actions + Pre-built im Repo + Manuelle Anleitung
Kombination aus B, D, E: CI baut bei Push, committet die aktualisierte `.skill` zurück, README dokumentiert auch den manuellen Weg.

---

## Entscheidung

Gewählt: **Option F (Hybrid)** — primär CI-basiert, mit pre-built `.skill` im Repo und manueller Fallback-Anleitung.

**Begründung:** Externe Nutzer:innen erwarten einen Direkt-Download der fertigen `.skill` (B). Drift-Freiheit lässt sich nur mit Automatisierung garantieren (E). Manuelle Anleitung (A) bleibt nötig für Forks, Offline-Builds und Skill-Inspekteur:innen, die der CI-Output nicht vertrauen. Die drei Bausteine ergänzen sich zu einem robusten Setup ohne nennenswerten Maintainer-Aufwand nach einmaligem CI-Setup.

### Konkrete Umsetzung

| Baustein                          | Verantwortlich        | Trigger              |
|-----------------------------------|----------------------|----------------------|
| `.github/workflows/build-skill.yml` | GitHub Actions      | Push auf `main`      |
| `konstruktiv-kritiker.skill` (Repo) | CI-Workflow         | Auto-Commit per CI   |
| README-Sektion „Variante A"       | Maintainer (statisch) | n. a.                |

Der CI-Workflow:
1. checkt das Repo aus
2. führt `zip -r konstruktiv-kritiker.skill SKILL.md references/` aus
3. committet die aktualisierte Datei zurück mit Marker `[skip ci]`
4. publiziert sie zusätzlich als Release-Asset bei jedem Tag

### Konsequenzen

**Positiv**
- Externe Nutzer:innen erhalten mit einem Klick eine immer aktuelle `.skill`
- Drift zwischen Source-Folder und distribuiertem ZIP ist strukturell ausgeschlossen
- Manuelle Anleitung erlaubt Offline- und Custom-Builds (Forks)
- Keine externe Abhängigkeit zur Build-Zeit (außer GitHub Actions selbst)
- Spec-konformes Output (Skill-Folder als ZIP-Wurzel) wird durch CI-Validierung sichergestellt

**Negativ**
- Einmaliger CI-Setup-Aufwand (GitHub-Actions-Workflow + ggf. Token für Auto-Commit)
- Repo enthält eine 45 KB große Binary-Datei — bei reiner Markdown-Repo-Hygiene unschön, aber bei dieser Größe akzeptabel
- Branches ohne CI-Lauf können eine veraltete `.skill` haben (kompensiert durch Repo-Konvention: Distribution nur ab `main`)
- CI-Schreibrechte aufs Repo nötig — minimal, aber ein Auth-Vektor

---

## Pro und Contra der Optionen

### Option A — Manuelle Anleitung
- ✅ Null Maintainer-Aufwand
- ✅ Kein Binary im Repo
- ❌ Hohe Adoptionshürde (jeder User muss zippen)
- ❌ Nutzer-Fehler wahrscheinlich (falsche ZIP-Struktur, vergessene Files)
- ❌ Verstärkt FM3 (*Sharing-Mechanik unausgereift*) aus dem Pre-Mortem

### Option B — Pre-built `.skill` manuell committen
- ✅ Niedrige Adoptionshürde (Direkt-Download)
- ❌ Drift bei jedem Source-Change ohne ZIP-Update
- ❌ Maintainer-Pflicht: ZIP nach jeder Änderung neu bauen
- ❌ Vergessen ist wahrscheinlich → Nutzer:innen bekommen veraltete `.skill`

### Option C — `package_skill.py` von Anthropic
- ✅ Standard-Tool mit Validation
- ❌ Externe Python-Abhängigkeit (`scripts.quick_validate`)
- ❌ Nicht trivial zu installieren ohne den ganzen Skill-Creator
- ❌ Nutzer:innen ohne Python schreiben aus

### Option D — Custom Build-Script
- ✅ Reproduzierbar
- ✅ Dokumentiert sich selbst (Script *ist* die Doku)
- ❌ Löst Drift-Problem nicht (Maintainer muss Script ausführen)
- ❌ Plattformspezifisch (Bash auf macOS/Linux ≠ Windows)

### Option E — Reines GitHub Actions
- ✅ Vollautomatisch
- ✅ Drift-frei
- ❌ `.skill` als Release-Asset bedeutet ein Klick mehr (Releases-Tab) für Nutzer:innen
- ❌ Bei Forks ohne CI-Setup keine `.skill` verfügbar

### Option F — Hybrid (gewählt)
- ✅ Beste Adoptionserfahrung (Direkt-Download im Repo-Root)
- ✅ Automatisch aktuell durch CI
- ✅ Manuelle Anleitung als Fallback und Inspektions-Hilfe
- ⚠️ Komplexer als Einzeloptionen — gerechtfertigt durch das Adoptions-Ziel

---

## Implementierungsstatus

- [x] Initiale `.skill` manuell erstellt (45 KB) und committet
- [x] README-Sektion „Variante A: Manuell zippen" geschrieben
- [ ] **TODO:** `.github/workflows/build-skill.yml` aufsetzen
- [ ] **TODO:** Auto-Commit-Token (GITHUB_TOKEN reicht) in Workflow-Permissions konfigurieren
- [ ] **TODO:** Test mit kleinem Source-Change verifizieren (Workflow läuft, `.skill` aktualisiert sich)
- [ ] **TODO:** Bei erstem Tag: Release-Asset-Publikation aktivieren

---

## Zukünftige Überlegungen / Migration-Pfade

- **Wenn Anthropic ein offizielles Skill-Registry einführt** (analog npm/PyPI): Migration zu zentraler Distribution prüfen. Die `.skill`-Datei im Repo wird dann redundant.
- **Wenn `package_skill.py` als CLI-Standalone verfügbar wird** (ohne Skill-Creator-Abhängigkeit): Option C reaktivieren — gibt Validation-Vorteile gegenüber `zip`.
- **Wenn der Skill multi-language wird** (DE + EN + …): Build-Matrix in CI ergänzen, mehrere `.skill`-Varianten parallel publizieren.

---

## Referenzen

- Anthropic Skill-Spezifikation: <https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview>
- Anthropic Skills Repository: <https://github.com/anthropics/skills>
- `package_skill.py` (Skill-Creator): <https://github.com/anthropics/skills>
- MADR-Format: <https://adr.github.io/madr/>
- Pre-Mortem-Befunde, die diese Entscheidung motivieren: `references/beispiel-lauf.md` (FM3 *Sharing-Mechanik unausgereift*, FM4 *Aufmerksamkeits-Konkurrenz*)
