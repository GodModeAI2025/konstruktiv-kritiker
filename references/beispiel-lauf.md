# Beispiel-Lauf: Skill auf sich selbst

Dieser Beispiel-Lauf zeigt den `konstruktiv-kritiker` in seiner stärksten Form: angewendet auf sich selbst. Der Skill stresstestet die eigene Adoption.

## Ausgangslage

**Vorhaben:** Adoption des `konstruktiv-kritiker`-Skills durch Personen außerhalb des Maintainers
**Maintainer:** Mark Zimmermann
**Stand:** Frisch gebauter Skill, 2× live in Konversation getestet, 0 externe Nutzer:innen

---

## Mindestschwelle (4-Punkte-Check)

| # | Punkt | Status |
|---|---|---|
| 1 | **Was?** | konstruktiv-kritiker-Skill (161 Zeilen + 7 references/), deutsche Adaption des englischen `premortem`-Skills |
| 2 | **Für wen?** | Primär Mark, sekundär EnBW-Kolleg:innen + Skill-Community + andere Adopter |
| 3 | **Ausgangsposition** | Heute frisch gebaut. mz-architekt-Score ~82 %. **0 externe Nutzer:innen.** |
| 4 | **SMART-Ziel** | „Mind. 3 Personen außerhalb des Maintainers nutzen den Skill aktiv bis 31.12.2026" – S✓ M✓ A✓ R✓ T✓ |

---

## Frame

> Es ist 31. Dezember 2026. Der konstruktiv-kritiker-Skill wird nicht von 3 oder mehr Personen außerhalb Mark Zimmermann aktiv genutzt. Adoption ist gescheitert. Wir schauen zurück und erklären, warum.

---

## 7 Failure Modes

1. **Sprach-/Original-Doppelfalle** – Skill ist deutsch (Markt-Fragmentierung) UND verweist auf englisches Original (Diskreditierungs-Frage)
2. **Trigger funktionieren nicht im Alltag** – Phrasen sind formal, Menschen reden im Alltag informell
3. **Sharing-Mechanik unausgereift** – Keine Skill-Marketplaces, manuelle Installation als Hürde
4. **Maintainer-Aufmerksamkeits-Konkurrenz** – Buch, Podcast, Job priorisieren über Skill-Promo
5. **Onboarding zu rigoros** – 4-Punkt-Mindestschwelle + 6 Schritte = zu viele Klicks bis zum ersten Wert
6. **Konkurrenz mit anderen Decision-Tools** – LLM-Council, alternative Skills, weniger Friction
7. **Maintainer nutzt Skill nicht selbst regelmäßig** – Ohne authentische Routine keine glaubwürdige Promotion

---

## Auszug Deep-Dive: FM5 (Onboarding zu rigoros)

**Fehlergeschichte:**
Eine Power-Userin installiert den Skill. Erste Frage an Claude: „kritisch hinterfragen unser Pricing-Modell". Skill triggert. Aber statt einer schnellen Analyse kommt: „Bevor ich starte, brauche ich 4 Dinge: Was, für wen, Ausgangsposition mit Zahlen, SMART-Erfolg." 4–5 Klärungsfragen folgen. Sie gibt langsam Antworten. Nach Frage 3 verliert sie die Geduld und sagt: „Mach einfach die Analyse."

Skill weigert sich (Anweisung: „Schlechte Kritik auf vagem Kontext schadet mehr als sie hilft"). Sie ist frustriert, beendet die Session. Der Skill ist zu rigoros für Quick-Sessions. Power-User wollen schnellen Output, sie haben den Kontext im Kopf. Mindestschwelle wurde für Qualität hochgezogen – Adoption leidet, weil 50 %+ der ersten Sessions in Frustration enden.

**Annahme:** „Strenges Kontext-Sammeln ist immer besser als pragmatisches Loslegen."

**Frühwarnzeichen:**
- 50 %+ der Erstnutzer:innen brechen vor Schritt 4 ab
- Feedback enthält „zu viele Fragen" oder „fragt zu viel" als wiederkehrendes Thema

---

## Auszug Deep-Dive: FM7 (Maintainer nutzt nicht selbst)

**Fehlergeschichte:**
Im Juni und Juli nutzt der Maintainer den Skill aktiv: einmal für ein Hire, einmal für eine Buch-Marketing-Strategie. Dann: Buch-Deadline. Podcast-Push. Heise-Artikel. Im August kein Skill-Lauf. September auch nicht. Oktober nur einmal als Demo für eine Kollegin.

Die LinkedIn-Posts zum Skill werden generischer: „Mein konstruktiv-kritiker-Skill ist immer noch eine wertvolle Methode" statt „Diese Woche habe ich mit dem Skill folgenden Failure Mode entdeckt: ...". Promotion verliert Authentizität. Externe Nutzer:innen merken: „Wenn der Maintainer ihn nicht nutzt, warum sollte ich?"

**Annahme:** „Der Skill ist gut genug, dass externe Nutzer:innen unabhängig vom Autor adoptieren."

**Frühwarnzeichen:**
- 30+ Tage kein Pre-Mortem-Lauf für eigene Vorhaben
- Skill-Promotion-Posts werden generischer (keine konkreten Beispiele aus aktueller Nutzung)

---

## Synthese

### Wahrscheinlichster Fehler
**FM7 – Maintainer nutzt den Skill nicht selbst regelmäßig.** Dadurch wird Promotion generisch, Authentizität bröckelt, Adoptions-Push verliert Glaubwürdigkeit. Ein Skill ohne lebendigen Maintainer ist ein Skill ohne Sog.

### Gefährlichster Fehler
**FM5 – Onboarding zu rigoros.** Die 4-Punkte-Mindestschwelle plus 6-Schritte-Workflow ist exzellent für Qualität, aber 50 %+ der Erstnutzer:innen brechen ab, bevor sie Wert sehen.

### Versteckte Annahme
„Skill-Adoption funktioniert wie Software-Adoption: gutes Produkt → wird genutzt." Falsch. Skill-Adoption ist **Methoden-Adoption** – braucht aktive Pflege durch Maintainer, regelmäßige Authentizitäts-Beweise, Onboarding-Optimierung, Community-Anbindung.

### Überarbeiteter Plan

1. **Routine etablieren:** 1× pro 2 Wochen eigener Pre-Mortem-Lauf für reales Vorhaben. Kalender-blockiert.
2. **README.md mit 3-Schritte-Quick-Start** auf GitHub – manuelle Installations-Hürde reduzieren.
3. **Quick-Modus via `$ARGUMENTS=schnell` ergänzen:** 2 Fragen statt 4 für Power-User mit Kontext im Kopf.
4. **Trigger-Liste um Umgangssprache erweitern:** „hilf mir kritisch", „was übersehe ich hier", „schau mal drauf".
5. **Englische Variante zurück-übersetzen:** EN + DE-Bundle teilen.
6. **Authentic Use-Cases-Posts monatlich:** „Diese Woche mit dem Skill entdeckt: …" – konkret, nicht abstrakt.
7. **Cross-Promo in Skill-Communities:** Anthropic Skills Discord, GitHub Awesome-Lists.

### Pre-Launch-Checkliste

- [ ] README.md mit 3-Schritte-Quick-Start auf GitHub
- [ ] Trigger-Liste um 5+ umgangssprachliche Phrasen erweitert
- [ ] Routine-Slot im Kalender: 1× alle 2 Wochen eigener Pre-Mortem-Lauf
- [ ] Quick-Modus implementiert mit reduzierter Klärungs-Sequenz
- [ ] Adoption-Tracker: GitHub-Downloads + bekannte Nutzer:innen + Feedback
- [ ] Englische Variante in Planung – Übersetzungs-Sprint im August

---

## Meta-Beobachtung

Der Skill hat sich auf sich selbst angewendet und dabei **drei Schwächen offengelegt**, die durch zwei vorherige produktive Tests (Buch + Podcast) NICHT erkannt wurden:

1. **Onboarding-Friction** (FM5) wurde durch die SMART-Erweiterung gerade VERSTÄRKT – Quick-Modus ist die Antwort.
2. **Maintainer-Authentizität** (FM7) ist eine strukturelle Anforderung ohne direktes Domänen-Cheatsheet.
3. **Sprache-vs-Community-Markt** (FM1) ist ein Skill-spezifisches Problem.

**Erkenntnis:** Der Skill produziert Failure Modes, die zwei produktive Tests nicht aufgedeckt hätten. Das ist der beste Wirksamkeitsbeweis – er kritisiert sich selbst konstruktiv und identifiziert eine Schwäche, die gerade erst eingebaut wurde.
