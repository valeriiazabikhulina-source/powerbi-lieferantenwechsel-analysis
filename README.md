# Power BI Dashboard: Qualitätssicherung Lieferantenwechsel

Persönliches Lernprojekt (Oktober 2026), entstanden, um mir Power BI,
Power Query und DAX praktisch anzueignen. Es zeigt, wie sich die Qualität von
Lieferantenwechsel-Prozessen in der Energieversorgung mit Reportings überwachen lässt.

> **Hinweis:** Alle Daten sind synthetisch und frei erfunden
> (siehe `generate_data.py`). Es gibt keinen Bezug zu realen Unternehmen,
> Kunden oder Netzbetreibern.

## Fragestellungen

1. Wie viele Wechselvorgänge gehen pro Monat ein, und wie viele werden abgelehnt?
2. Wie lange dauert die Bearbeitung, und wie oft wird die Zielzeit (10 Tage) eingehalten?
3. Welche Ablehnungsgründe treten am häufigsten auf?
4. Gibt es Netzbetreiber oder Zeiträume mit auffällig vielen Fehlern?
5. Wo lohnt sich eine Prozessoptimierung?

## Daten

| Datei | Inhalt |
|---|---|
| `data/wechselvorgaenge.csv` | ca. 5.400 Vorgänge (Okt 2025 bis Sep 2026): Status, Sparte, Kundentyp, Netzbetreiber, Ablehnungsgrund, Bearbeitungstage |
| `data/netzbetreiber.csv` | 12 fiktive Netzbetreiber mit Region |

Der Datensatz enthält bewusst typische Datenqualitätsprobleme (Duplikate,
uneinheitliche Schreibweisen, fehlende Werte), die in Power Query bereinigt werden.

## Vorgehen

1. **Power Query:** Duplikate entfernen, Text trimmen und vereinheitlichen, leere
   Werte kennzeichnen, Datentypen setzen, Vorgänge ohne Netzbetreiber prüfen.
2. **Datenmodell:** Sternschema mit `Wechselvorgaenge`, `Netzbetreiber` und `Kalender`.
3. **DAX:** Kennzahlen wie Ablehnungsquote, Ø Bearbeitungsdauer, SLA-Quote und
   Vormonatsvergleich (siehe [`dax_measures.md`](dax_measures.md)).
4. **Dashboard** mit drei Seiten:
   - *Übersicht:* KPI-Karten, Verlauf der Vorgänge und der Ablehnungsquote je Monat
   - *Fehleranalyse:* Ablehnungsgründe, Verlauf je Grund, Filter nach Sparte und Kundentyp
   - *Netzbetreiber:* Ranking nach Ablehnungsquote, Detailtabelle mit Drill-through

## Ergebnisse

_Hier folgen Screenshots des Dashboards und eine kurze Zusammenfassung der
Erkenntnisse (siehe Ordner `screenshots/`)._

## Verwendete Werkzeuge

Power BI Desktop, Power Query, DAX, Python (nur zur Datengenerierung)

## Projekt selbst nachbauen

```bash
python generate_data.py   # erzeugt die CSV-Dateien im Ordner data/
```

Danach die CSV-Dateien in Power BI Desktop laden und den Schritten oben folgen.
