# HTML-Report-Template

Verwende dieses Skeleton als Ausgangspunkt für den HTML-Report. Passe Akzentfarben, Anzahl der Cards und Inhalte an die jeweilige Analyse an.

## Designprinzipien

- **Dunkler Hintergrund** (`#0a0e1a` oder ähnlich), klare Typografie, gut zu scannen
- **Synthese-Abschnitt prominent oben** – die meisten lesen Synthese und überfliegen Cards
  - Wahrscheinlichster Fehler (orange)
  - Gefährlichster Fehler (rot)
  - Versteckte Annahme (lila)
  - Überarbeiteter Plan (türkis, volle Breite)
- **Eine Card pro Fehlergrund** mit eigener Akzentfarbe (oben angeordnet als 4-Punkt-Top-Border)
- **Severity-Indikator** (5 Punkte, gefüllt = Schweregrad)
- **Pre-Launch-Checkliste** als eigener Block mit Häkchen-Boxen
- **Footer** mit Zeitstempel und Untersuchungsgegenstand

## Akzentfarben-Palette (für Cards)

```
Card 1: #ef5350 (rot)
Card 2: #ff7043 (orange-rot)
Card 3: #ffa726 (orange)
Card 4: #ffca28 (gelb)
Card 5: #66bb6a (grün)
Card 6: #42a5f5 (blau)
Card 7: #ab47bc (lila)
Card 8: #26a69a (türkis)
Card 9: #ec407a (pink)
```

## HTML-Skeleton

```html
<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<title>Konstruktive Kritik · {{TITEL}}</title>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", system-ui, sans-serif;
    background: #0a0e1a;
    color: #e8eaf0;
    line-height: 1.6;
    padding: 24px 16px;
  }
  .container { max-width: 880px; margin: 0 auto; }
  header { border-bottom: 1px solid #1f2942; padding-bottom: 24px; margin-bottom: 32px; }
  .pill {
    display: inline-block; background: #2a1a1a; color: #ff6b6b;
    padding: 4px 12px; border-radius: 999px;
    font-size: 11px; font-weight: 600; letter-spacing: 0.08em;
    text-transform: uppercase; margin-bottom: 12px;
  }
  h1 { font-size: 28px; line-height: 1.25; margin-bottom: 8px; color: #fff; }
  .subtitle { color: #8892b0; font-size: 14px; }
  .frame {
    background: linear-gradient(135deg, #1a1228 0%, #0f1525 100%);
    border-left: 3px solid #ff6b6b;
    padding: 20px 24px; border-radius: 6px;
    margin-bottom: 32px; font-style: italic; color: #d8c8e8;
  }
  h2 {
    font-size: 13px; text-transform: uppercase; letter-spacing: 0.12em;
    color: #64ffda; margin: 36px 0 16px;
    padding-bottom: 8px; border-bottom: 1px solid #1f2942;
  }
  .synthesis-grid {
    display: grid; grid-template-columns: 1fr; gap: 16px; margin-bottom: 24px;
  }
  @media (min-width: 700px) { .synthesis-grid { grid-template-columns: 1fr 1fr; } }
  .syn-card {
    background: #11172a; border-radius: 8px; padding: 20px;
    border: 1px solid #1f2942;
  }
  .syn-card.likely { border-left: 4px solid #ffa726; }
  .syn-card.dangerous { border-left: 4px solid #ef5350; }
  .syn-card.hidden { border-left: 4px solid #ab47bc; }
  .syn-card.revised { border-left: 4px solid #26a69a; grid-column: 1/-1; }
  .syn-card h3 {
    font-size: 12px; text-transform: uppercase; letter-spacing: 0.08em;
    color: #8892b0; margin-bottom: 10px;
  }
  .syn-card p { font-size: 15px; color: #e8eaf0; }
  .checklist {
    background: #0f1525; border: 1px solid #1f2942; border-radius: 8px;
    padding: 20px; margin-bottom: 32px;
  }
  .checklist h3 {
    color: #64ffda; font-size: 14px; margin-bottom: 12px;
    text-transform: uppercase; letter-spacing: 0.08em;
  }
  .checklist ul { list-style: none; padding: 0; }
  .checklist li {
    padding: 8px 0 8px 28px; position: relative; font-size: 14px;
    border-bottom: 1px solid #1a2238;
  }
  .checklist li:last-child { border-bottom: none; }
  .checklist li::before {
    content: "▢"; position: absolute; left: 0;
    color: #64ffda; font-size: 16px;
  }
  .fm-grid { display: grid; grid-template-columns: 1fr; gap: 16px; }
  .fm-card {
    background: #11172a; border-radius: 8px; padding: 22px;
    border: 1px solid #1f2942; border-top-width: 4px;
  }
  /* Akzentfarben pro Card via data-color="1..9" */
  .fm-card[data-color="1"] { border-top-color: #ef5350; }
  .fm-card[data-color="2"] { border-top-color: #ff7043; }
  .fm-card[data-color="3"] { border-top-color: #ffa726; }
  .fm-card[data-color="4"] { border-top-color: #ffca28; }
  .fm-card[data-color="5"] { border-top-color: #66bb6a; }
  .fm-card[data-color="6"] { border-top-color: #42a5f5; }
  .fm-card[data-color="7"] { border-top-color: #ab47bc; }
  .fm-card[data-color="8"] { border-top-color: #26a69a; }
  .fm-card[data-color="9"] { border-top-color: #ec407a; }
  .fm-meta {
    display: flex; justify-content: space-between; align-items: center;
    margin-bottom: 12px; flex-wrap: wrap; gap: 8px;
  }
  .fm-tag {
    font-size: 10px; font-weight: 600; letter-spacing: 0.1em;
    text-transform: uppercase; color: #8892b0;
  }
  .severity { display: inline-flex; gap: 3px; }
  .severity span {
    width: 8px; height: 8px; border-radius: 50%; background: #1f2942;
  }
  .severity span.on { background: #ef5350; }
  .fm-card h4 {
    font-size: 18px; color: #fff; margin-bottom: 14px; line-height: 1.3;
  }
  .fm-section {
    margin-top: 14px; padding-top: 14px; border-top: 1px dashed #1f2942;
  }
  .fm-section-label {
    font-size: 10px; font-weight: 700; letter-spacing: 0.1em;
    text-transform: uppercase; color: #64ffda; margin-bottom: 6px;
  }
  .fm-section.warning .fm-section-label { color: #ffa726; }
  .fm-section.assumption .fm-section-label { color: #ab47bc; }
  .fm-section p { font-size: 14px; color: #c8cdd9; }
  footer {
    margin-top: 48px; padding-top: 20px; border-top: 1px solid #1f2942;
    text-align: center; color: #5a6480; font-size: 12px;
  }
</style>
</head>
<body>
<div class="container">

  <header>
    <span class="pill">Konstruktive Kritik</span>
    <h1>{{TITEL_DES_VORHABENS}}</h1>
    <p class="subtitle">{{KURZBESCHREIBUNG · ZIEL · BETEILIGTE · ANZAHL_FEHLERMODI}}</p>
  </header>

  <div class="frame">
    „Es ist {{ZIELDATUM_PLUS_6_MONATE}}. {{VORHABEN}} ist gescheitert. Wir schauen zurück und erklären, warum."
  </div>

  <h2>Synthese</h2>
  <div class="synthesis-grid">
    <div class="syn-card likely">
      <h3>Wahrscheinlichster Fehler</h3>
      <p>{{TEXT}}</p>
    </div>
    <div class="syn-card dangerous">
      <h3>Gefährlichster Fehler</h3>
      <p>{{TEXT}}</p>
    </div>
    <div class="syn-card hidden">
      <h3>Versteckte Annahme</h3>
      <p>{{TEXT}}</p>
    </div>
    <div class="syn-card revised">
      <h3>Überarbeiteter Plan – konkret</h3>
      <p>{{NUMMERIERTE_ÜBERARBEITUNGEN}}</p>
    </div>
  </div>

  <div class="checklist">
    <h3>Pre-Launch-Checkliste</h3>
    <ul>
      <li>{{CHECKPUNKT_1}}</li>
      <li>{{CHECKPUNKT_2}}</li>
      <li>{{CHECKPUNKT_3}}</li>
    </ul>
  </div>

  <h2>Die {{N}} Failure Modes</h2>
  <div class="fm-grid">

    <div class="fm-card" data-color="1">
      <div class="fm-meta">
        <span class="fm-tag">FM1 · {{KATEGORIE}}</span>
        <span class="severity">
          <span class="on"></span><span class="on"></span><span class="on"></span><span></span><span></span>
        </span>
      </div>
      <h4>{{FEHLER_TITEL}}</h4>
      <p>{{FEHLERGESCHICHTE_ABSATZ_1}}</p>
      <p>{{FEHLERGESCHICHTE_ABSATZ_2}}</p>
      <div class="fm-section assumption">
        <div class="fm-section-label">Annahme</div>
        <p>{{ZUGRUNDELIEGENDE_ANNAHME}}</p>
      </div>
      <div class="fm-section warning">
        <div class="fm-section-label">Frühwarnung</div>
        <p>{{FRÜHWARNZEICHEN}}</p>
      </div>
    </div>

    <!-- Weitere Cards mit data-color="2", "3", ... -->

  </div>

  <footer>
    Konstruktive Kritik · {{DATUM}} · Methode nach Gary Klein (HBR 2007)
  </footer>

</div>
</body>
</html>
```

## Anwendungs-Hinweise

- **Severity-Indikator:** 1–5 gefüllte Punkte. Schweregrad orientiert sich an Schadenspotenzial × Wahrscheinlichkeit.
- **Card-Reihenfolge:** Kritischste Failure Modes oben (höchste Severity zuerst).
- **Mobile-Tauglichkeit:** Layout responsiv (Grid bricht auf eine Spalte unter 700 px).
- **Print-fähig:** Dunkles Design ist screen-optimiert. Falls der Nutzer drucken will, hellen Modus mit gleicher Struktur anbieten.
