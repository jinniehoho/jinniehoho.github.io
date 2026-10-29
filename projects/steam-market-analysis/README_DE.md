# Steam Market & Product Analysis

> Public source snapshot: the two notebooks are provided with saved outputs and local metadata removed. Their analytical code is unchanged. They have not been rerun end to end for this publication. The original CSV, processed data, practice exercises and PBIX files are not distributed. The SQL folder is currently empty; the PostgreSQL queries/views required to reproduce the report are not yet included.

[Portfolio](https://jinniehoho.github.io/) · [Report (English PDF)](../../reports/steam-report.pdf) · [Notebooks](notebooks/) · [Data model](docs/data_model.md)


## Projektübersicht

Dieses Projekt analysiert den Steam-PC-Spielemarkt aus der Perspektive eines kleinen Indie-Game-Studios, das sich in der frühen Planungsphase eines neuen Spiels befindet.

Das Ziel besteht nicht darin, ein einzelnes „bestes“ Genre zu bestimmen. Stattdessen werden Marktangebot, beobachtete Spieleraktivität, Nutzerreaktionen, Preisstrukturen und aktuelle Marktentwicklungen verschiedener Spielsegmente miteinander verglichen.

Auf Grundlage dieser Ergebnisse werden schließlich Marktsegmente identifiziert, die für eine weiterführende Produktanalyse interessant sein könnten.

---

## Business-Kontext

### Stakeholder

Product / Business Lead eines kleinen Indie-Game-Studios.

### Business-Ziel

Die Analyse soll die frühe Produktplanung unterstützen und unter anderem folgende Fragen beantworten:

- In welchen Genres ist das Marktangebot besonders hoch?
- Welche Genres zeigen eine vergleichsweise hohe Spieleraktivität bzw. Traction?
- Wie unterscheiden sich Nutzerzufriedenheit und Engagement zwischen verschiedenen Spieleigenschaften?
- Wie unterscheiden sich Traction und Zufriedenheit zwischen verschiedenen Preissegmenten?
- Wie hat sich die relative Marktpräsenz verschiedener Genres im Zeitverlauf verändert?
- Gibt es Segmente mit vergleichsweise geringem Angebot, aber auffälliger Traction, die eine weiterführende Untersuchung rechtfertigen?

Die Analyse dient der strukturierten Produkt- und Markterkundung und nicht der Vorhersage eines kommerziellen Erfolgs.

---

## Datensatz

**Steam Games Dataset – FronkonGames**

Quelle:

- Hugging Face
- Steam API
- SteamSpy

Der Datensatz enthält Informationen zu Steam-Spielen, unter anderem:

- Veröffentlichungsdatum
- Preis
- Geschätzte Besitzerzahl
- Peak CCU
- Positive und negative Bewertungen
- Empfehlungen
- Durchschnittliche und mediane Spielzeit
- Genres
- Kategorien
- Tags
- Entwickler und Publisher
- Plattformunterstützung
- Metacritic- und User-Scores

Der Rohdatensatz wird separat gespeichert und während der Analyse nicht verändert.

---

## Wichtige Hinweise zur Dateninterpretation

Der Datensatz enthält keine tatsächlichen Verkaufs- oder Umsatzdaten.

Daher gelten folgende Interpretationsregeln:

- `Estimated owners` wird als Proxy für Ownership bzw. Traction verwendet und nicht als tatsächliche Verkaufszahl interpretiert.
- `Peak CCU` wird als Indikator für Aktivität bzw. Traction verwendet und nicht als Gesamtzahl der Spieler.
- Die Anzahl der Reviews wird nicht automatisch als Nutzerzufriedenheit interpretiert.
- Spielzeit wird als Engagement betrachtet und nicht automatisch mit Zufriedenheit gleichgesetzt.
- Beobachtete Zusammenhänge werden als deskriptive Zusammenhänge und nicht als kausale Effekte interpretiert.
- Identifizierte Marktsegmente gelten als Kandidaten für weitere Untersuchungen und nicht als garantierte Marktchancen.

---

## Analytischer Rahmen

Das Projekt folgt dem analytischen Ablauf:

**Supply / Competition**  
→ **Demand / Traction**  
→ **Satisfaction & Engagement**  
→ **Pricing**  
→ **Market Trend**  
→ **Candidate Segments**

---

## 1. Marktangebot / Wettbewerb

### Fragestellung

In welchen Genres ist das Marktangebot besonders hoch und wie unterscheidet sich die aktuelle Veröffentlichungsaktivität?

Wichtige Dimensionen und Kennzahlen:

- Genre
- Anzahl der Spiele
- Neue Veröffentlichungen
- Veröffentlichungszeitraum

Eine hohe Anzahl an Spielen wird zunächst als hohe Angebotskonzentration interpretiert und nicht automatisch als unattraktive Wettbewerbssituation.

---

## 2. Nachfrage / Traction

### Fragestellung

Welche Genres zeigen eine vergleichsweise hohe beobachtete Spieler-Traction?

Mögliche Traction-Indikatoren:

- Estimated owners
- Peak CCU
- Recommendations
- Review-Volumen

Wo sinnvoll, werden sowohl die gesamte Traction eines Genres als auch typische Werte pro Spiel betrachtet.

Dadurch soll verhindert werden, dass Genres allein aufgrund einer hohen Anzahl veröffentlichter Spiele automatisch stärker erscheinen.

---

## 3. Nutzerzufriedenheit & Engagement

### Fragestellung

Wie unterscheiden sich Nutzerzufriedenheit und Engagement zwischen Genres und Spieleigenschaften?

Mögliche Zufriedenheitsindikatoren:

- Anteil positiver Reviews
- User Score
- Recommendations

Engagement-Indikatoren:

- Durchschnittliche Spielzeit
- Mediane Spielzeit

Als Vergleichsdimensionen werden unter anderem Genres, Kategorien und ausgewählte Tags verwendet.

Zufriedenheit und Engagement werden dabei als unterschiedliche analytische Konzepte behandelt.

---

## 4. Preisstruktur

### Fragestellung

Wie unterscheiden sich Spieler-Traction und Zufriedenheit zwischen verschiedenen Preissegmenten?

Die Analyse vergleicht Preisgruppen anhand von:

- Traction-Indikatoren
- Zufriedenheitsindikatoren
- gegebenenfalls Engagement-Indikatoren

Free-to-Play-Spiele werden bei Bedarf separat betrachtet, da ihre Marktstruktur deutlich von kostenpflichtigen Spielen abweichen kann.

---

## 5. Marktentwicklung

### Fragestellung

Wie haben sich Genre-Präsenz und beobachtete Traction im Zeitverlauf verändert?

Auf Basis des Veröffentlichungsdatums werden unter anderem untersucht:

- Veränderungen der Genre-Abdeckung
- aktuelle Veröffentlichungsaktivität
- relative Marktpräsenz im Zeitverlauf

Veränderungen der Genre-Abdeckung werden als Veränderung der relativen Marktpräsenz interpretiert und nicht automatisch als Marktwachstum.

---

## 6. Analyse potenzieller Marktsegmente

Die abschließende Analyse verwendet keine einzelne Kennzahl, sondern kombiniert Ergebnisse aus den vorherigen Analyseschritten.

Mögliche Kandidatensegmente werden anhand mehrerer Faktoren betrachtet:

- Angebotsintensität
- beobachtete Traction
- Nutzerzufriedenheit
- Engagement
- aktuelle Marktpräsenz

Ziel ist es, Segmente zu identifizieren, die für eine weiterführende Produktanalyse interessant sein könnten.

Die Ergebnisse stellen keine Prognose oder Garantie für kommerziellen Erfolg dar.

---

## Grundsätze der Datenaufbereitung

Für das Projekt gilt der Grundsatz:

> **No cleaning without analytical reason.**

Werte werden nicht allein deshalb entfernt oder verändert, weil sie ungewöhnlich erscheinen.

Bei jedem Datenproblem wird zunächst geprüft:

1. Was bedeutet der Wert?
2. Ist er für eine Business-Fragestellung relevant?
3. Handelt es sich tatsächlich um ein Datenqualitätsproblem?
4. Würde eine Transformation die ursprüngliche Bedeutung verändern?

Der Datenworkflow folgt dem Schema:

**Raw**  
→ **Audit**  
→ **Decision**  
→ **Clean / Transform**  
→ **Validate**  
→ **Processed**

Der ursprüngliche Rohdatensatz bleibt unverändert.

---

## Data Audit

Die Datenprüfung umfasst unter anderem:

- Größe des Datensatzes
- Datentypen
- Fehlende Werte
- Nullwerte
- Duplikate
- Auffällige Werte
- Mehrfachwerte in kategorialen Spalten
- Numerische Verteilungen
- Zeitliche Abdeckung der Veröffentlichungsdaten
- Struktur der Estimated-Owners-Bereiche

Entscheidungen werden nach folgendem Schema dokumentiert:

| Column | Beobachtetes Problem | Business-Relevanz | Entscheidung | Begründung |
|---|---|---|---|---|
| Beispiel | Beispielproblem | Zugehörige Business-Frage | Keep / Transform / Exclude | Analytische Begründung |

---

## Technologie-Stack

### Python / Pandas

Verwendet für:

- Dateninspektion
- Data Audit
- Datenbereinigung
- Transformation
- Erstellung neuer Variablen
- Explorative Analyse
- Validierung

### PostgreSQL

Verwendet für:

- Strukturierte Speicherung der Analysedaten
- SQL-Aggregationen
- Wiederverwendbare Analyseabfragen
- Vorbereitung der Daten für Power BI

### Power BI

Verwendet für:

- Interaktives Reporting
- KPI-Visualisierung
- Marktvergleiche
- Trendanalyse
- Finales Decision-Support-Dashboard

### Excel

Selektiv verwendet für:

- Projektplanung
- Dokumentation
- Zwischenkontrollen

---

## Power-BI-Bericht

Der finale Power-BI-Bericht besteht aus sechs Seiten.

### 1. Marktüberblick

Überblick über den Steam-Markt und das Genre-Angebot.

### 2. Angebot vs. Traction

Vergleich von Marktangebot und beobachteter Spieler-Traction zur Identifikation unterschiedlicher Marktpositionen.

### 3. Nutzerreaktion & Preis

Analyse von Zufriedenheit, Engagement und Performance verschiedener Preissegmente.

### 4. Markttrends

Darstellung der Veränderung relativer Genre-Abdeckung und Marktpräsenz im Zeitverlauf.

### 5. Markteintritt

Zusammenführung der wichtigsten Analyseergebnisse zur Eingrenzung potenziell interessanter Marktsegmente.

### 6. Detailanalyse der Kandidaten

Vertiefte Analyse ausgewählter Genres sowie unterstützender Produktsignale.

Die letzte Seite dient als Decision-Support-Zusammenfassung und nicht als Prognose des kommerziellen Erfolgs.

---

## Analytische Interpretation

Die finale Analyse konzentriert sich auf Segmente, bei denen mehrere Signale gleichzeitig in eine interessante Richtung weisen.

Ein Kandidatensegment kann beispielsweise folgende Eigenschaften aufweisen:

- Vergleichsweise moderates Angebot
- Überdurchschnittliche beobachtete Traction
- Stabile oder zunehmende aktuelle Marktpräsenz
- Unterstützende Nutzerreaktionen

Diese Signale werden gemeinsam interpretiert und nicht anhand einer einzelnen Kennzahl bewertet.

Zusätzlich werden bei ausgewählten Kandidatensegmenten Spieleigenschaften und Kategorien betrachtet.

---

## Limitationen

Bei der Interpretation der Ergebnisse müssen mehrere Einschränkungen berücksichtigt werden.

### Keine tatsächlichen Verkaufs- oder Umsatzdaten

Der Datensatz enthält keine verifizierten Verkaufszahlen oder Umsätze.

Estimated Owners und Aktivitätskennzahlen dienen daher ausschließlich als Proxy.

### Geschätzte Besitzerzahlen

`Estimated owners` basiert auf Schätzungen und kann breite Wertebereiche enthalten.

Die Werte dürfen nicht als exakte Verkaufszahlen interpretiert werden.

### Historische Akkumulation

Ältere Spiele hatten mehr Zeit, Besitzer, Reviews, Empfehlungen und Spielzeit zu akkumulieren.

Der Veröffentlichungszeitraum muss daher bei Vergleichen berücksichtigt werden.

### Überschneidende Genres

Steam-Spiele können mehreren Genres, Kategorien und Tags gleichzeitig zugeordnet sein.

Genre-Aggregationen sind daher nicht gegenseitig ausschließend.

### Fehlende und ungleichmäßig verfügbare Daten

Einige Variablen, beispielsweise externe Bewertungsscores, sind nur für einen Teil der Spiele verfügbar.

Sie werden daher nicht automatisch als repräsentativ für den gesamten Steam-Markt betrachtet.

### Beobachtungsdaten

Die Analyse untersucht Zusammenhänge in historischen Steam-Daten.

Sie ermöglicht keine kausalen Aussagen über den Einfluss bestimmter Spieleigenschaften auf den kommerziellen Erfolg.

### Nicht enthaltene Business-Faktoren

Mehrere für den Erfolg eines Spiels wichtige Faktoren sind im Datensatz nicht enthalten, beispielsweise:

- Entwicklungsbudget
- Marketingausgaben
- Reputation des Studios
- Markenbekanntheit
- Produktionsqualität
- Entwicklungsaufwand
- Fähigkeiten und Ressourcen des Teams
- Externe Vertriebskanäle

Kandidatensegmente sollten daher immer gemeinsam mit Produktionsumfang und Fähigkeiten des Studios bewertet werden.

---

## Projektstruktur

- `README.md`
- `README_DE.md`
- `README.md`
- `data/raw/` (local only, not published)
- `data/processed/` (local only, not published)
- `notebooks/`
- `sql/` (not included; original folder currently empty)
- [Report PDF](../../reports/steam-report.pdf)
- `docs/`

Der Rohdatensatz wird bewusst getrennt von den aufbereiteten Analysedaten gespeichert.

---

## Projekt ansehen

### Power BI

Öffnen:

the [English PDF report](../../reports/steam-report.pdf); the German PDF is withheld because its last page is cropped

mit Power BI Desktop.

Zusätzlich ist eine PDF-Version des Berichts enthalten, damit die Ergebnisse auch ohne Power BI schnell eingesehen werden können.

### Python

Die Notebooks dokumentieren den Workflow von:

- Dateninspektion
- Data Audit
- Datenbereinigung
- Transformation
- Validierung
- Analysevorbereitung

### SQL

Der lokale Bericht verwendet PostgreSQL-Views. Die SQL-Definitionen sind in dieser Veröffentlichung noch nicht enthalten; die vollständige Pipeline ist damit noch nicht reproduzierbar.

---

## Aktualisierung der Power-BI-Daten

Der Power-BI-Bericht enthält das importierte Analysemodell.

Für eine Aktualisierung der Daten kann eine erneute Konfiguration der ursprünglichen PostgreSQL- bzw. lokalen Datenquellenverbindung erforderlich sein, da lokale Pfade und Zugangsdaten vom jeweiligen System abhängen.

Der bereits erstellte Bericht kann auch ohne Aktualisierung der Datenquelle vollständig betrachtet werden.

---

## Projektziel

Dieses Projekt wurde sowohl als analytisches Abschlussprojekt als auch als Portfolio-Projekt entwickelt.

Der vorgesehene Workflow ist unten dargestellt. Die SQL- und Berichtsschritte sind mit dem öffentlichen Stand noch nicht vollständig reproduzierbar:

**Data Acquisition**  
→ **Data Understanding**  
→ **Data Audit**  
→ **Data Preparation**  
→ **SQL Analysis**  
→ **Data Modeling**  
→ **Business Intelligence**  
→ **Interpretation**

Der Schwerpunkt liegt nicht ausschließlich auf der Visualisierung von Daten, sondern auf der nachvollziehbaren Verbindung zwischen Datenaufbereitung, analytischen Entscheidungen und einer konkreten Business-Fragestellung.