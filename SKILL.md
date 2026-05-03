---
name: konstruktiv-kritiker
description: "Konstruktive Kritik an Plänen, Launches, Produkten, Einstellungen, Strategien oder Entscheidungen — bevor sie scheitern. Nutzt die Pre-Mortem-Methode (Klein/HBR): geht davon aus, das Vorhaben sei in 6 Monaten bereits gescheitert, und arbeitet rückwärts, um jeden Grund dafür zu finden. Erzeugt einen überarbeiteten Plan mit aufgedeckten blinden Flecken. PFLICHT-TRIGGER: 'kritisch hinterfragen', 'konstruktive Kritik', 'Schwachstellen finden', 'blinde Flecken aufdecken', 'was übersehe ich', 'stresstest mein', 'zukunftssicher machen', 'Pre-Mortem dazu', 'Premortem für', 'mach eine Pre-Mortem', 'spiel Advocatus Diaboli', 'finde Schwachstellen'. STARKE TRIGGER: 'was könnte schiefgehen', 'wo bricht das', 'was könnte das killen', 'finde Schwachstellen im Plan', 'Risiken aufdecken', 'übersehe ich etwas', 'Plan stresstesten'. NICHT triggern bei einfachen Feedback-Anfragen, Faktenfragen oder Anfragen zum LLM-Council. TRIGGERN, wenn jemand einen Plan oder eine Entscheidung hat, bei der die Kosten eines Fehlers hoch sind."
---

# Konstruktiver Kritiker

Eine Pre-Mortem ist das Gegenteil einer Post-Mortem. Statt herauszufinden, was schiefgelaufen ist, *nachdem* etwas gescheitert ist, stellt man sich vor, es sei bereits gescheitert, und findet heraus, warum – *bevor* man beginnt.

Die Methode stammt vom Psychologen **Gary Klein**. Er publizierte sie in der *Harvard Business Review* (2007). **Daniel Kahneman** (Nobelpreisträger, *Thinking, Fast and Slow*) nannte sie seine wertvollste Entscheidungstechnik. Google, Goldman Sachs und Procter & Gamble nutzen sie vor wichtigen Entscheidungen.

Die Kernerkenntnis: Wenn man Menschen fragt „Was könnte schiefgehen?", bekommt man vorsichtige, abgesicherte Antworten. Sagt man hingegen „Das ist bereits gescheitert, erklärt mir warum", schaltet das Gehirn in den Erzählmodus und produziert deutlich spezifischere, kreativere, ehrlichere Gründe. Forscher an Wharton und Cornell nannten das *prospective hindsight* und zeigten, dass es die Fähigkeit zur Identifikation von Ursachen zukünftiger Ergebnisse um ca. 30 % steigert (Mitchell, Russo & Pennington, 1989).

**Warum das für KI-gestützte Entscheidungen wichtig ist:** Claude tendiert standardmäßig zu zustimmenden, optimistischen Antworten. Fragt man „Ist das ein guter Plan?", findet Claude Gründe, Ja zu sagen. Die Pre-Mortem durchbricht dieses Muster, indem sie den Frame auf „Das ist tot, erklär wie es gestorben ist" zwingt. Claude hört auf, nach Gründen zu suchen, warum der Plan funktioniert, und beginnt stattdessen zu erklären, wie er gescheitert ist.

---

## Eingabe

`$ARGUMENTS` – Interpretiere als:

| Eingabe | Aktion |
|---------|--------|
| *(leer)* | Lies Konversationskontext + Workspace-Dateien |
| Vorhabens-Beschreibung | Nutze als Startpunkt, ergänze fehlenden Kontext |
| `domain=buch` / `produkt` / `hire` / `strategie` / `mna` / `forschung` / `bildung` / `gruendung` / `event` / `internationalisierung` / `fundraising` / `migration` / `reorg` / `kampagne` / `karriere` / `community` / `vertrag` | Lade passendes Frühwarn-Cheatsheet aus `references/` |
| `kein-html` | Skip HTML-Report, nur Markdown-Transkript |
| `kurz` | Kompakte Synthese im Chat ohne Files |

---

## Wann verwenden

**Gute Pre-Mortem-Ziele:**
- Ein Produkt oder Feature, das du gleich bauen willst
- Ein Launch-Plan, bei dem Geld oder Reputation auf dem Spiel stehen
- Eine Preisänderung oder ein Geschäftsmodell-Wechsel
- Eine Einstellung, die du vornehmen willst
- Ein Strategie- oder Positionierungs-Pivot
- Eine Partnerschaft oder ein Deal, den du evaluierst
- Eine Firmengründung oder ein Markteintritt
- Eine Reorganisation oder ein Teamumbau
- Jede Verpflichtung, bei der die Kosten eines Fehlers hoch sind

**Schlechte Pre-Mortem-Ziele:**
- Vage Ideen ohne konkreten Plan (zuerst beim Planen helfen, dann Pre-Mortem)
- Fragen mit einer richtigen Antwort (einfach beantworten)
- Kreatives Feedback zu einem Entwurf (das ist Lektorat, keine Pre-Mortem)
- Bereits getroffene, irreversible Entscheidungen (eine Pre-Mortem ist nur nützlich, wenn man noch etwas ändern kann)

---

## Kontext erfassen (Mindestschwelle)

Eine Pre-Mortem ist nur so gut wie der Kontext, auf dem sie läuft. Vager Input produziert vage Fehlerszenarien, die niemandem helfen. Vor dem Start muss eine Mindest-Kontextschwelle erreicht sein.

### Schritt 1: Vorhandenen Kontext scannen

Bevor du den Nutzer irgendetwas fragst, suche nach Kontext, der bereits verfügbar ist:

**A. Die aktuelle Konversation.** Der Nutzer hat möglicherweise bereits einen Plan, einen Launch, ein Produkt oder eine Entscheidung besprochen. Lies die Konversation zurück und extrahiere alles Relevante.

**B. Der Workspace.** Scanne schnell nach Dateien, die relevanten Kontext enthalten könnten:
- `CLAUDE.md` oder `claude.md` (Business-Kontext, Präferenzen, Constraints)
- Jedes `memory/`-Verzeichnis (Zielgruppen-Profile, Business-Details, vergangene Entscheidungen)
- Dateien, die der Nutzer explizit referenziert oder angehängt hat
- Projektdateien, Briefings oder Pläne, die sich auf das Vorhaben beziehen

Verwende `Glob` und schnelle `Read`-Aufrufe. Nicht mehr als 30 Sekunden dafür aufwenden. Du suchst nach den Schlüsseldateien, die die Fehlerszenarien in der Realität verankern.

### Schritt 2: Kontextsuffizienz bewerten

Nach dem Scan prüfe, ob du genug hast für eine nützliche Pre-Mortem. Du brauchst **vier** Dinge:

1. **Was ist es?** – Ein klares Verständnis des Vorhabens (ein Produkt, ein Launch, eine Einstellung, eine Preisänderung, eine Strategie). Du musst es dem Nutzer in einem Satz zurück beschreiben können.
2. **Für wen / wen betrifft es?** – Zielgruppe, Kund:innen, Team, Stakeholder. Fehlerszenarien hängen stark davon ab, wer beteiligt ist.
3. **Ausgangsposition: Wo stehst du heute?** – Konkrete Baseline mit Zahlen, nicht „so mittel". Beispiele: aktuelle Verkaufszahlen, Hörer:innen, Charts-Position, MRR, Headcount, Conversion-Rate, Reichweite, Pipeline-Volumen. **Ohne Baseline keine Lücke. Ohne Lücke keine scharfen Failure Modes.**
4. **SMART-Erfolg: Was bedeutet Erfolg konkret?** – Scheitern ist definiert als das Gegenteil von Erfolg. Wenn du nicht weißt, was Erfolg bedeutet, kannst du auch nicht definieren, was Scheitern bedeutet. Validiere das Erfolgskriterium aktiv gegen alle fünf SMART-Kriterien:
    - **S — Spezifisch:** Eindeutig benannt? („Top 10 in Apple Podcasts Tech-Charts Deutschland" – nicht „bekannt werden")
    - **M — Messbar:** Mit harter Metrik prüfbar? (Charts-Position, Umsatz, NPS, verkaufte Exemplare – nicht „Aufmerksamkeit")
    - **A — Achievable / Realistisch:** Im Vergleich zur Ausgangsposition im Zeitrahmen mathematisch erreichbar? **Wenn die Lücke offensichtlich zu groß ist, ist genau das die wichtigste versteckte Annahme im Pre-Mortem – mache es im Frame explizit.**
    - **R — Relevant:** Zahlt das Ziel auf ein größeres, verstandenes Ziel ein?
    - **T — Terminiert:** Konkretes Datum, nicht „bald" oder „dieses Jahr"

### Schritt 3: Lücken konversationell füllen

Wenn du alle vier Punkte hast, gehe sofort zur Pre-Mortem über. Keine unnötigen Fragen stellen.

Wenn ein oder mehrere Punkte fehlen, frage nach dem wichtigsten fehlenden Punkt zuerst. **Eine Frage nach der anderen.** Bewerte nach jeder Antwort, ob du nun genug hast. Frage so lange, bis die Schwelle erreicht ist, aber nie mehr als nötig.

Beispiele für fokussierte Kontextfragen:
- „Was genau willst du launchen/bauen/entscheiden?" (wenn du nicht weißt, was es ist)
- „Für wen ist das?" (wenn du den Plan kennst, aber nicht die Zielgruppe)
- „Was bedeutet Erfolg konkret – mit Zahl und Datum?" (wenn du Plan und Zielgruppe kennst, aber nicht das Erfolgskriterium)

Das Ziel ist, die Mindestschwelle so schnell wie möglich zu erreichen, ohne dass sich der Nutzer fühlt, als würde er ein Formular ausfüllen. **Konversationell, nicht interrogativ.** Wenn du eine Antwort aus dem Kontext ableiten kannst, tue das, statt zu fragen.

**Realismus-Check explizit:** Wenn die Lücke zwischen Ausgangsposition und SMART-Ziel mathematisch sehr groß wirkt (z. B. „3.000 → 100.000 in 8 Monaten"), notiere das als zentrale Achievable-Annahme. Sie wird in der Synthese fast immer auftauchen.

**Eskalation:** Nach 3 Klärungsfragen ohne ausreichenden Kontext brichst du ab und schlägst Plan-Schärfung vor. Schlechte Kritik auf vagem Kontext schadet mehr als sie hilft.

---

## Workflow (6 Schritte)

### 1. Frame setzen

Nachdem du genug Kontext hast, setze den Pre-Mortem-Frame explizit:

> „OK, ich habe genug Kontext. Starten wir die Pre-Mortem. Die Prämisse: Es ist 6 Monate in der Zukunft. [Das Vorhaben/der Launch/die Entscheidung] ist gescheitert. Es ist vorbei. Wir schauen zurück und versuchen zu verstehen, was schiefgelaufen ist."

Dieser Frame ist nicht Deko – er ist der psychologische Mechanismus. Er verschiebt den Modus von „Bewerte diesen Plan" (was zustimmende Antworten triggert) zu „Erkläre warum das gestorben ist" (was ehrliche, spezifische Fehleridentifikation triggert). Ohne ihn fällt die Analyse auf höfliche Risikobewertung zurück.

### 2. Roh-Fehlergründe generieren

Führe die Roh-Pre-Mortem als eine umfassende Analyse durch. Keine vorgegebenen Kategorien, keine Linsen, keine Einschränkungen. Nur die Kern-Klein-Methode:

„Dieser Plan ist 6 Monate in der Zukunft gescheitert. Generiere jeden ernsthaften Grund, warum er gestorben sein könnte. Sei umfassend. Sei spezifisch. Verankere jeden Grund in den tatsächlichen Details des Plans. Fülle nicht mit schwachen Gründen auf und höre nicht zu früh auf, wenn es mehr gibt."

Der Output ist eine umfassende Liste von Fehlergründen, jeder in 1–2 Sätzen. Manche Pläne haben 4 echte Fehlermodi, andere 9 – die Anzahl muss real sein für diesen spezifischen Plan, nicht aufgefüllt.

Jeder Fehlergrund muss:
- Spezifisch für diesen Plan sein (kein generischer Rat, der auf alles zutrifft)
- In tatsächlichen Plan-Details verankert sein
- Eine echte Bedrohung darstellen (kein Randfall oder minimale Unannehmlichkeit)

**Optional – Domänen-Cheatsheets:** Wenn `$ARGUMENTS` eine Domäne enthält oder das Vorhaben klar zuordenbar ist, lade das passende Cheatsheet als Inspiration:

- `references/fruehwarnung-buch.md` – Buch- und Publikationsprojekte
- `references/fruehwarnung-produkt.md` – SaaS-/Produkt-Launches, Workshops, Kurse
- `references/fruehwarnung-hire.md` – Einstellungen, Berater:innen, lange Mandate
- `references/fruehwarnung-strategie.md` – Pivots, Positionierungs-Wechsel
- `references/fruehwarnung-mna.md` – M&A, Übernahmen, Joint Ventures
- `references/fruehwarnung-forschung.md` – Forschungsanträge, Drittmittel
- `references/fruehwarnung-bildung.md` – Bildungsangebote, Kurse, Weiterbildungen
- `references/fruehwarnung-gruendung.md` – Firmengründung, Startup-Launch
- `references/fruehwarnung-event.md` – Konferenzen, Events, Veranstaltungen
- `references/fruehwarnung-internationalisierung.md` – Marktexpansion, Lokalisierung
- `references/fruehwarnung-fundraising.md` – Finanzierungsrunden, Crowdfunding
- `references/fruehwarnung-migration.md` – IT-Migration, Systemwechsel
- `references/fruehwarnung-reorg.md` – Reorganisation, Teamumbau
- `references/fruehwarnung-kampagne.md` – Marketingkampagnen, Go-to-Market
- `references/fruehwarnung-karriere.md` – Karrierewechsel, beruflicher Umbruch
- `references/fruehwarnung-community.md` – Community, Open-Source-Projekte
- `references/fruehwarnung-vertrag.md` – Großaufträge, Vertragsverhandlungen

Die Cheatsheets sind Inspiration, keine Pflicht. Generiere immer auch plan-spezifische Failure Modes, die nicht in den Listen stehen.

### 3. Deep-Dives parallel (ein Agent pro Fehlergrund, alle gleichzeitig)

Nimm jeden Fehlergrund aus Schritt 2 und spawne einen Sub-Agenten pro Grund, alle parallel. Jeder Agent nimmt seinen zugewiesenen Fehlergrund und geht unabhängig in die Tiefe.

**Sub-Agent-Prompt-Vorlage:**

```
Du bist Ermittler in einer konstruktiven Kritik-Analyse. Dir wurde ein spezifischer Fehlergrund zugewiesen, den du in der Tiefe analysieren sollst.

Der Plan:
---
[voller Kontext: was es ist, für wen, wie Erfolg aussieht, plus relevanter Workspace-Kontext]
---

FRAME: Wir sind 6 Monate in der Zukunft. Dieser Plan ist gescheitert.

DEIN ZUGEWIESENER FEHLERGRUND: [der spezifische Fehlergrund aus Schritt 2]

Deine Aufgabe ist es, bei diesem einen Fehler in die Tiefe zu gehen. Schreibe die Geschichte, wie er sich tatsächlich abgespielt hat. Sei konkret. Nutze Details aus dem Plan. Lass es real wirken, wie eine Fallstudie zu etwas, das tatsächlich passiert ist.

Dein Output sollte enthalten:

1. DIE FEHLERGESCHICHTE: Eine 2–3 Absätze lange Erzählung, wie sich dieser spezifische Fehler abgespielt hat. Nutze Details aus dem Plan. Benenne konkrete Momente, in denen Dinge schiefgingen, und warum.

2. DIE ZUGRUNDELIEGENDE ANNAHME: Die eine Sache, die der Nutzer für selbstverständlich gehalten hat und die diesen Fehler erst möglich gemacht hat. Formuliere sie in einem Satz.

3. FRÜHWARNZEICHEN: 1–2 konkrete, beobachtbare Signale, auf die der Nutzer achten kann und die anzeigen würden, dass dieser Fehlermodus beginnt, sich abzuspielen. Das sollten Dinge sein, die man tatsächlich sehen oder messen kann, keine vagen Gefühle.

Halte die gesamte Antwort unter 300 Wörtern. Sei direkt. Beschönige nichts. Drücke dich nicht herum.
```

**Fallback:** Ohne Sub-Agenten (z. B. Claude.ai ohne Task-Tool) führst du die Deep-Dives sequenziell selbst durch. Langsamer, aber dasselbe Ergebnis.

### 4. Synthese

Lies alle Deep-Dives und produziere den **Pre-Mortem-Report**:

1. **Wahrscheinlichster Fehler** – Welches Fehlerszenario ist am wahrscheinlichsten angesichts dessen, was du über den Plan weißt? Warum? Hierauf sollte sich der Nutzer zuerst konzentrieren.
2. **Gefährlichster Fehler** – Welches Fehlerszenario würde den größten Schaden anrichten, wenn es eintritt, selbst wenn es weniger wahrscheinlich ist? Hiergegen lohnt es sich, sich abzusichern.
3. **Versteckte Annahme** – Was ist über alle Fehleranalysen hinweg die größte Annahme, die der Nutzer macht und die er wahrscheinlich nicht hinterfragt hat? Hier liegt oft der eigentliche Wert der Pre-Mortem: die Sache, die für den Nutzer so offensichtlich ist, dass er vergessen hat, dass es eine Annahme ist.
4. **Überarbeiteter Plan** – Welche konkreten Änderungen würden den Plan widerstandsfähiger machen? Sei konkret. Nicht „überlege deine Preisgestaltung", sondern „teste den Preis bei 297 € mit 20 Personen, bevor du dich öffentlich festlegst". Jede Überarbeitung muss direkt auf ein spezifisches Fehlerszenario mappen.
5. **Pre-Launch-Checkliste** – 3–5 spezifische Dinge, die der Nutzer verifizieren, testen oder einrichten sollte, bevor er loslegt. Jeder Punkt sollte einen der identifizierten Fehlermodi verhindern oder erkennen.

### 5. HTML-Report generieren

Generiere einen visuellen HTML-Report und speichere ihn im Workspace des Nutzers.

**Datei:** `kritik-report-[timestamp].html`

Der Report ist eine einzelne, eigenständige HTML-Datei mit Inline-CSS. Designprinzipien:

- **Dunkler Hintergrund** (`#0a0e1a` oder ähnlich), klare Typografie, leicht zu scannen
- **Synthese-Abschnitt prominent oben** – die meisten lesen die Synthese und überfliegen die Cards
- **Eine visuelle Card pro Fehlergrund** mit Fehlergeschichte, zugrundeliegender Annahme und Frühwarnzeichen. Verwende unterschiedliche Akzentfarben pro Card, damit sie visuell unterscheidbar sind.
- **Severity-Indikator** für jeden Fehlermodus (5 Punkte, gefüllt = Schweregrad)
- **Die Agenten-Übersicht**: Zeige die Anzahl der Agenten und ihre Ergebnisse als Grid oder Card-Layout, damit der Nutzer den vollen Umfang der Pre-Mortem auf einen Blick sieht
- **Pre-Launch-Checkliste** als eigener Block mit Checkbox-Symbolen
- **Footer** mit Zeitstempel und Untersuchungsgegenstand

Verwende die Vorlage aus `references/html-template.md` als Ausgangspunkt. Öffne die HTML-Datei nach der Generierung.

**Skip-Bedingung:** Wenn `$ARGUMENTS` `kein-html` oder `kurz` enthält, überspringe diesen Schritt.

### 6. Markdown-Transkript speichern

**Datei:** `kritik-transcript-[timestamp].md`

Enthält:
- Den erfassten Kontext (Was, Wer, Ausgangsposition, Erfolgskriterium)
- Die Roh-Fehlergründe
- Alle Deep-Dive-Analysen der Agenten
- Die vollständige Synthese

---

## Output-Format

Jede Pre-Mortem-Session produziert zwei Dateien:

```
kritik-report-[timestamp].html       # visueller Report zum Scannen
kritik-transcript-[timestamp].md     # vollständiges Transkript als Referenz
```

Der Nutzer sieht den HTML-Report zuerst. Das Transkript ist da, wenn er tiefer in die Begründung hinter jedem Fehlerszenario eintauchen will.

Zusätzlich eine knappe Zusammenfassung im Chat: wahrscheinlichster Fehler, versteckte Annahme, wichtigste Plan-Korrektur. **Maximal drei Sätze.** Der Report hat die vollständigen Details.

---

## Beispiel: Pre-Mortem eines 297-€-Workshops

**Nutzer:** „Stresstest mein Plan: Ich will einen 297-€-Live-Workshop launchen, wie man Claude für Marketing-Teams einsetzt. 50 Plätze. Zielgruppe: Marketing-Manager in Unternehmen mit 10–50 Mitarbeitenden."

**Roh-Pre-Mortem identifiziert 6 Fehlergründe:**
1. Marketing-Manager in dieser Unternehmensgröße brauchen Genehmigung für 297 € Weiterbildung – das erzeugt Friction, die nicht eingeplant ist
2. „Claude für Marketing" ist ein tool-spezifischer Pitch in einem Markt, in dem die meisten Manager noch klären, ob KI überhaupt für sie relevant ist
3. Die Zielgruppe, die tatsächlich kauft, könnten Solopreneure sein, nicht Team-Manager – Mismatch zwischen Inhalt und Teilnehmer:innen
4. Ein Workshop für Marketing-Teams braucht Demo-Umgebungen mit realistischen Marketing-Daten und Multi-Seat-Setups – das sind 5 Wochen Vorbereitung, nicht die 2, die budgetiert sind
5. Wenn 60 % der Teilnehmer:innen Solopreneure sind, werden Reviews und Case Studies nicht bei der Marketing-Manager-Zielgruppe resonieren, die du für zukünftige Kohorten brauchst
6. Bei 297 € × 50 Plätzen ist der maximale Umsatz 14.850 € – das rechtfertigt möglicherweise nicht den Vorbereitungsaufwand im Vergleich zu anderen Einnahmequellen

**6 Agenten gehen unabhängig tief auf jeden Grund ein und produzieren Fehlergeschichten, zugrundeliegende Annahmen und Frühwarnzeichen.**

**Synthese:** Wahrscheinlichster Fehler ist der Zielgruppen-Mismatch: Du zielst auf Personen, die eine Genehmigung für 297 € brauchen, was Friction erzeugt, die nicht eingeplant ist. Gefährlichster Fehler: Solopreneure statt Team-Manager anziehen bedeutet, dass deine Case Studies und Testimonials bei der eigentlichen Zielkäufer:innen-Gruppe für zukünftige Kohorten nicht resonieren werden – das Problem potenziert sich über die Zeit. Versteckte Annahme: Du nimmst an, „Marketing-Manager in Unternehmen mit 10–50 Personen" sei eine erreichbare Zielgruppe, aber diese Personen identifizieren sich nicht so und halten sich nicht an denselben Orten auf. Überarbeiteter Plan: Führe eine 47-€-Pilot-Session mit 20 Personen durch. Nutze sie, um herauszufinden, ob deine tatsächlichen Käufer:innen Team-Manager oder Solopreneure sind, und baue den vollen Workshop für die, die tatsächlich auftauchen.

**Vollständiger Beispiel-Lauf** (Skill auf sich selbst angewendet): siehe `references/beispiel-lauf.md`.

---

## Wichtige Hinweise

- **Frame immer explizit setzen.** „Das ist bereits gescheitert" ist der psychologische Mechanismus, der die Pre-Mortem funktionieren lässt. Ohne ihn fällt die Analyse auf höfliche Risikobewertung zurück.
- **Sub-Agenten immer parallel spawnen, nie sequenziell** (wenn verfügbar). Sequentielles Spawning verschwendet Zeit und lässt frühere Antworten spätere beeinflussen.
- **Umfassend, aber nicht aufgefüllt.** Finde jeden echten Fehlergrund. Höre nicht bei 3 auf, wenn es 7 gibt. Aber erzwinge keine 7, wenn es nur 3 gibt. Die Anzahl muss real sein für diesen spezifischen Plan.
- **Die Synthese ist das Produkt.** Die meisten Nutzer lesen die Synthese und überfliegen die einzelnen Fehler-Cards. Die Synthese muss konkret und handlungsleitend sein.
- **Nichts beschönigen.** Der ganze Sinn einer Pre-Mortem ist, dem Nutzer Dinge zu sagen, die er nicht hören will, bevor die Realität es tut. Wenn ein Plan ernsthafte Probleme hat, sage es direkt.
- **Der überarbeitete Plan muss konkret sein.** Nicht „überlege deine Preisgestaltung", sondern „führe einen 47-€-Pilot mit 20 Personen durch, bevor du dich auf den vollen 297-€-Workshop festlegst". Jede Überarbeitung muss etwas sein, das der Nutzer diese Woche tun kann.
- **Mindestkontext respektieren.** Es ist besser, eine Frage mehr zu stellen, als eine schlechte Pre-Mortem auf unzureichendem Kontext zu produzieren.
- **Baseline ist Pflicht.** Wenn der Nutzer die Ausgangsposition nicht in Zahlen benennen kann, ist die Pre-Mortem zu vage. Frag nach – auch wenn er drängt loszulegen.
- **SMART-Validierung nicht überspringen.** Besonders das „A" (Achievable) kostet 30 Sekunden Nachdenken und entlarvt oft das eigentliche Problem: ein mathematisch unrealistisches Ziel.
- **Cheatsheets als Inspiration, nicht als Korsett.** Plan-spezifische Failure Modes immer höher gewichten als generische Domänen-Listen.
- **Nicht das LLM-Council.** Das Council gibt mehrere Perspektiven auf eine Entscheidung *jetzt*. Die Pre-Mortem schickt Claude in die Zukunft, wo die Entscheidung bereits gescheitert ist, und arbeitet rückwärts, um zu erklären, warum. Anderer psychologischer Mechanismus, anderer Output. Wenn der Nutzer mehrere Perspektiven statt Fehleranalyse will, schlage das Council vor.

---

## Struktur

```
konstruktiv-kritiker/
├── SKILL.md (diese Datei)
└── references/
    ├── sub-agent-prompt.md          # Prompt-Template für Deep-Dives
    ├── html-template.md             # HTML-Report-Skeleton
    ├── beispiel-lauf.md             # Vollständiger Workshop-Beispiel-Lauf
    ├── fruehwarnung-buch.md         # Buch- und Publikationsprojekte
    ├── fruehwarnung-produkt.md      # Produkt-Launches, Workshops, Kurse
    ├── fruehwarnung-hire.md         # Einstellungen, Berater:innen
    ├── fruehwarnung-strategie.md    # Pivots, Positionierungs-Wechsel
    ├── fruehwarnung-mna.md          # M&A, Übernahmen, Joint Ventures
    ├── fruehwarnung-forschung.md    # Forschungsanträge, Drittmittel
    ├── fruehwarnung-bildung.md      # Bildungsangebote, Kurse, Weiterbildungen
    ├── fruehwarnung-gruendung.md    # Firmengründung, Startup-Launch
    ├── fruehwarnung-event.md        # Konferenzen, Events, Veranstaltungen
    ├── fruehwarnung-internationalisierung.md  # Marktexpansion, Lokalisierung
    ├── fruehwarnung-fundraising.md  # Finanzierungsrunden, Crowdfunding
    ├── fruehwarnung-migration.md    # IT-Migration, Systemwechsel
    ├── fruehwarnung-reorg.md        # Reorganisation, Teamumbau
    ├── fruehwarnung-kampagne.md     # Marketingkampagnen, Go-to-Market
    ├── fruehwarnung-karriere.md     # Karrierewechsel, beruflicher Umbruch
    ├── fruehwarnung-community.md    # Community, Open-Source-Projekte
    └── fruehwarnung-vertrag.md      # Großaufträge, Vertragsverhandlungen
```

---

## Quellen & Inspiration

Dieser Skill ist die deutsche Adaption und Erweiterung eines englischsprachigen `premortem`-Skills. Übersetzung sprachlich auf den deutschen Fachbuch- und Unternehmenskontext zugeschnitten; Methodik und Mechanik bleiben dem Original treu.

- **Methode:** Gary Klein, *„Performing a Project Premortem"*, Harvard Business Review, September 2007
- **Bekanntheit:** Daniel Kahneman, *Thinking, Fast and Slow* (2011) – beschreibt die Technik als seine wertvollste Entscheidungstechnik
- **Empirie:** Mitchell, Russo & Pennington (1989), *Journal of Behavioral Decision Making* – ca. 30 % bessere Ursachen-Identifikation durch *prospective hindsight*
- **Mechanik:** Frame-Setzung, parallele Deep-Dives pro Fehlergrund, strukturierte Synthese – stammen aus dem englischen Original-Skill
