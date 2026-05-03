# Sub-Agent-Prompt-Vorlage

Verwendung: Pro identifiziertem Fehlergrund einen Sub-Agenten parallel mit dieser Vorlage spawnen. Wenn keine echten Sub-Agenten verfügbar sind (z. B. Claude.ai ohne Task-Tool), führe die Deep-Dives sequenziell selbst durch.

## Prompt

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

## Hinweise zur Anwendung

- **Parallelisierung ist Pflicht** (wenn möglich): Sequentielle Deep-Dives lassen frühere Antworten spätere beeinflussen und reduzieren die Diversität der Analysen.
- **Pro Agent ein Fehlergrund**: Niemals zwei Fehlergründe an denselben Agenten geben – das verwässert die Tiefe.
- **Voller Kontext mitgeben**: Der Agent kennt den Plan nicht aus der Konversation. Alles relevante (Was, Wer, Erfolg, plus Workspace-Auszüge) muss im Prompt enthalten sein.
- **Wort-Limit ernst nehmen**: 300 Wörter zwingen zur Verdichtung. Längere Outputs verlieren an Schärfe.
