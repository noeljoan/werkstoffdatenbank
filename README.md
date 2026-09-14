<div align="center">

# 🔩 Werkstoffdatenbank

**Zentrale Verwaltung, Pflege und Bereitstellung von Werkstoffdaten** — Desktop-GUI für die Datenpflege, mehrsprachige Web-App zum Suchen, Ansehen & Teilen.

![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-Backend-009688?logo=fastapi&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-Datenbank-003B57?logo=sqlite&logoColor=white)
![Tkinter](https://img.shields.io/badge/Tkinter-Desktop--GUI-informational)
![i18n](https://img.shields.io/badge/Sprachen-DE%20%7C%20EN%20%7C%20FR%20%7C%20ES-blueviolet)
![PDF](https://img.shields.io/badge/Datenblatt--PDF-4%20Sprachen-e8a000)
![FKM](https://img.shields.io/badge/FKM%202002-FFD--Import%20%26%20Export-6a1b9a)
![Regeln](https://img.shields.io/badge/Chemie%E2%86%92Eigenschaften-regelbasiert-c0392b)
![KI](https://img.shields.io/badge/KI--gest%C3%BCtzt-Import%20%26%20Norm--Status-2e7d32)

</div>

---

## ✨ Was kann die App?

| | |
|---|---|
| 🗂️ **Alle Werkstoffdaten an einem Ort** | Normen, Liefernormen, chemische Zusammensetzung (32 Hauptelemente + offene Liste weiterer Elemente), mechanische, physikalische, dynamische Eigenschaften, Spannungs-Dehnungs-Diagramm, Wöhlerkurve, Wärmebehandlung, Härte, Reinheitsgrad, Dokumente, Nachfolger/Alternativen |
| 🧬 **Chemie → Eigenschaften (Werkstoffvergleich & Einflussanalyse)** | Regelbasierte, werkstofffamilien- und legierungssystem-abhängige Analyse: welches Element wirkt bei diesem konkreten Werkstoff wie auf welche Eigenschaft — mit Quelle, Gültigkeitsbereich, Bedingung und Vertrauensstatus je Regel. Fe-Basis (Stahl/Gusseisen), Al-Basis und Cu-Basis bereits mit Ausgangsregeln befüllt, jederzeit ohne Codeänderung erweiterbar |
| 🤖 **KI-Import** | Datenblatt (PDF/TXT) rein → KI extrahiert alle Felder inkl. Fußnoten → Vorschau prüfen → speichern. Als Desktop-Dialog **und** als eigenständiges Browser-Tool verfügbar |
| 🧪 **Werkstoffgenerator & Werkstoff ergänzen** | Aus Rm + Werkstoffgruppe (optional Rp0,2/A5/E-Modul) werden Wechselfestigkeiten und zyklische Kennwerte berechnet — als neuer Werkstoff oder feldweise bestätigte Ergänzung eines bestehenden. Vergleichsfenster ist frei skalierbar mit Scrollbereich |
| 📈 **Kurven-Generatoren** | Spannungs-Dehnungs-Diagramm und Wöhlerkurve werden live aus vorhandenen Kennwerten berechnet und angezeigt — als GUI-Tab **und** im PDF-Datenblatt. Fehlende Einzelwerte werden automatisch aus anderen Kennwert-Zeilen desselben Werkstoffs ergänzt (z. B. E-Modul nach einem FFD-Import) |
| 📑 **Norm-Update-Assistent** | Neue PDF-Fassung einer Norm hochladen (Datei-Dialog **oder** Drag & Drop) → KI vergleicht mit dem DB-Stand → Diff-Protokoll → nur bestätigte Felder werden übernommen |
| 🔍 **Norm-Status-Prüfung (KI)** | Monatliche Prüfliste: prüft per Websuche, ob die hinterlegte Normausgabe noch aktuell ist — mit Quellenpflicht, nie ohne Bestätigung übernommen |
| 📄 **FFD-Export & -Import (FKM 2002)** | Werkstoff als `.ffd`-Datei (STEYR/FEST-FILE-Format) exportieren **oder** eine `.ffd`-Datei aus einem Versuch einlesen — Werte werden vor der Übernahme immer in einem Prüfdialog angezeigt, nie automatisch übernommen |
| 🖥️ **Desktop-GUI** | Vollständige Datenpflege, CSV-Import, PDF-Datenblätter, ANSYS-Export, FFD-Export/-Import, Regel-Verwaltung |
| 🌐 **Web-App** | Durchsuchen, ansehen, PDF herunterladen — im Browser, auch im WLAN vom Handy aus |
| 🌍 **4 Sprachen** | Web-Oberfläche **und** PDF-Datenblatt komplett auf Deutsch, Englisch, Französisch, Spanisch. Für die Desktop-GUI steht die technische Grundlage (Sprachmenü, Persistenz, Übersetzungstabelle) bereits — die vollständige Übersetzung aller GUI-Texte ist ein laufendes, schrittweises Vorhaben (siehe [GUI-Mehrsprachigkeit](#-gui-mehrsprachigkeit-im-aufbau)) |
| 🏷️ **Differenzierender Anzeigename** | `Kurzname+Behandlungszustand+Beschichtung` (z. B. `S235JR+N`) — nur wenn die Zusatzangaben auch gesetzt sind |
| 🔢 **Automatische Werkstoff-ID** | Jeder Werkstoff bekommt fortlaufend `M00001`, `M00002`, … (5-stellig) + Revisionsstand |
| 📎 **PDFs direkt anhängen** | Normen, Liefernormen, Datenblätter, Prüfberichte — landen sicher in der Datenbank, kein Dateichaos |
| ⚙️ **ANSYS-Export** | Fertige `.mac`- und Workbench-`.xml`-Dateien auf Knopfdruck |

---

## 🚀 Schnellstart

```powershell
# 1. Ins Projektverzeichnis
cd app

# 2. Abhängigkeiten installieren
pip install -r requirements.txt

# 3a. Desktop-GUI starten (Datenpflege)
python -m gui

# 3b. ODER Web-App starten (Browser)
python -m uvicorn backend.main:app --reload --port 8000
```

Web-App dann öffnen unter **http://localhost:8000** 🎉

> 💡 **Erste Ausführung oder Update?** Immer zuerst `python migrate.py` ausführen (idempotent, siehe [Migration](#-migration-nach-updates)). Unsicher, ob die Datenbank vollständig ist? `python schema_diagnose.py` zeigt exakt, was fehlt. Für Beispieldaten: `python -m cli.admin daten beispiele`.

---

## 📚 Inhaltsverzeichnis

- [Voraussetzungen & Installation](#️-voraussetzungen--installation)
- [Anwendung starten](#️-anwendung-starten)
- [Migration nach Updates](#-migration-nach-updates)
- [Schema-Diagnose](#-schema-diagnose)
- [KI-Import (Datenblatt-Import)](#-ki-import-datenblatt-import)
- [Werkstoffgenerator & Werkstoff ergänzen](#-werkstoffgenerator--werkstoff-ergänzen)
- [Kurven-Generatoren](#-kurven-generatoren-spannungs-dehnung--wöhlerkurve)
- [Chemie → Eigenschaften: Werkstoffvergleich & Einflussanalyse](#-chemie--eigenschaften-werkstoffvergleich--einflussanalyse)
- [Norm-Update-Assistent](#-norm-update-assistent)
- [Norm-Status-Prüfung (KI)](#-norm-status-prüfung-ki)
- [FFD-Export & FFD-Import (FKM 2002)](#-ffd-export--ffd-import-fkm-2002)
- [Mehrsprachigkeit (Web & PDF)](#-mehrsprachigkeit-web--pdf)
- [GUI-Mehrsprachigkeit (im Aufbau)](#-gui-mehrsprachigkeit-im-aufbau)
- [Werkstoff-ID, Revision & Anzeigename](#-werkstoff-id-revision--anzeigename)
- [GUI im Überblick](#️-gui-im-überblick)
- [Web-App im Überblick](#-web-app-im-überblick)
- [Datenmodell](#-datenmodell)
- [API-Referenz](#-api-referenz)
- [CLI-Referenz](#-cli-referenz)
- [CSV-Import](#-csv-import)
- [PDF-Datenblatt](#-pdf-datenblatt)
- [ANSYS-Export](#️-ansys-export)
- [PDFs zu Dokumenten & Normen](#-pdfs-zu-dokumenten--normen)
- [Netzwerkzugriff (Handy/Tablet)](#-netzwerkzugriff-handytablet)
- [Troubleshooting](#-troubleshooting)

---

## ⚙️ Voraussetzungen & Installation

```powershell
python --version    # 3.10 oder höher

cd app
pip install -r requirements.txt
```

`tksheet` ist eine **Pflichtabhängigkeit** — ohne installiertes Paket lässt sich die Werkstoff-Detailansicht nicht öffnen (`ImportError`), da sechs Tabs (Mechanisch, Physikalisch, Dynamische Eigenschaften, Wärmebehandlung, Härte, Reinheitsgrad) direkt darauf aufbauen. `tkinterdnd2` (Drag & Drop im Norm-Update-Assistenten) ist dagegen echt optional — fehlt es, läuft die GUI normal weiter, nur ohne Drag & Drop beim PDF-Hochladen.

**Auto-Speichern statt Speichern-Button:** Änderungen an einzelnen Zellen werden automatisch ~0,9 Sekunden nach der letzten Eingabe gespeichert (kein Klick nötig) — ein kleiner Statustext ("✓ Gespeichert HH:MM:SS") bestätigt das unauffällig. Nur die riskanten Aktionen bleiben bewusst mit einer Rückfrage abgesichert: **Zeile löschen** (fragt vor dem sofortigen Löschen+Speichern nach) und **↺ Sitzung zurücksetzen** (stellt den Stand beim Öffnen des Tabs wieder her und speichert diesen sofort).

---

## ▶️ Anwendung starten

### Desktop-GUI

```powershell
cd app
python -m gui
```
Startet sofort, kein Server nötig.

### Web-App

```powershell
cd app
python -m uvicorn backend.main:app --reload --port 8000
```

| Adresse | Zweck |
|---|---|
| http://localhost:8000 | Web-App |
| http://localhost:8000/docs | Swagger-UI |
| http://localhost:8000/redoc | ReDoc |

Für Zugriff aus dem WLAN (Handy, Tablet, anderer PC): `--host 0.0.0.0` statt `--reload` verwenden — Details unter [Netzwerkzugriff](#-netzwerkzugriff-handytablet).

---

## 🔄 Migration nach Updates

Nach jedem Code-Update mit neuen Feldern/Tabellen einmal ausführen:

```powershell
cd app
python migrate.py
```

✅ **Idempotent** — beliebig oft ausführbar, bestehende Daten bleiben unangetastet. Dabei werden u. a. automatisch nachgezogen:
- fehlende Werkstoff-IDs vergeben (`M00001`, …) bzw. bestehende vierstellige IDs auf **5-stellig** aufgefüllt,
- neue Tabellen angelegt (`waermebehandlungen`, `haerte_werte`, `reinheitsgrade`, `norm_status_pruefungen`, `elementwirkung_regeln`),
- neue Spalten in bestehenden Tabellen ergänzt, z. B. die fehlenden **Min-Werte für 17 Elemente**, die zuvor nur ein Max-Feld hatten, sowie die drei neu ergänzten Spurelemente **Ce (Cer), O (Sauerstoff), Ga (Gallium)**,
- ein **Ausgangsbestand an Elementwirkungs-Regeln** (Fe-/Al-/Cu-Basis) wird einmalig eingespielt, sofern die Tabelle noch leer ist — eigene, über den Verwaltungsdialog ergänzte Regeln werden dabei nie überschrieben.

---

## 🔍 Schema-Diagnose

Ist nicht sicher, ob `migrate.py` wirklich alles nachgezogen hat (z. B. nach manuellem Kopieren einzelner Dateien)?

```powershell
cd app
python schema_diagnose.py
```

Vergleicht die **tatsächliche** Struktur von `data/werkstoff.db` erschöpfend gegen das SQLAlchemy-Modell (`backend/models.py`) und listet exakt auf, welche Tabellen/Spalten fehlen — reiner Lesezugriff, schreibt nichts.

---

## 🤖 KI-Import (Datenblatt-Import)

Datenblatt (PDF/TXT) rein → ein LLM extrahiert alle erkennbaren Felder ins Werkstoffdatenbank-Schema → Vorschau prüfen & bearbeiten → speichern. Verfügbar in **zwei Varianten mit identischem KI-Prompt und Datenschema**:

| | Desktop-Dialog | Browser-Tool |
|---|---|---|
| Aufruf | GUI → Menü **Import → 🤖 KI-Import (Datenblatt/Norm) …** | `werkstoff_import.html` direkt im Browser öffnen |
| Speicherweg | Direkt über `gui/db_service.py` gegen `data/werkstoff.db` | REST-API (Backend muss laufen) |
| Details, API-Key-Handling | — | siehe **README_werkstoff_import.md** |

**Was wird erkannt:** Kurzname, Werkstoffnummer, Normen, chemische Zusammensetzung (**alle 32 Hauptelemente, jeweils mit Min UND Max** — auch bei Elementen wie P, S, V, Cu, B, N u. a., die früher nur ein Max-Feld hatten), plus offene Liste weiterer Elemente, Mechanisch/Physikalisch/Dynamisch/Wärmebehandlung/Härte/Reinheitsgrad — inkl. Fußnoten (aufgelöst je Zeile *und* als unveränderte Legende).

**Gusseisen-Probestückbuchstaben (S/U/C):** Bei EN-GJS-/EN-GJL-/EN-GJV-Bezeichnungen bezeichnet ein am Kurznamen angehängtes S, U oder C nach EN 1563/EN 1561 die **Art des Probestücks** (getrennt gegossen / angegossen / Strangguss) — **kein** Behandlungszustand, auch wenn zufällig gleichlautende Codes in der Behandlungszustand-Stammliste existieren. Der Buchstabe bleibt Teil des Kurznamens; ein Warnhinweis erscheint in der GUI, sobald ein Gusseisen-Werkstoff geöffnet wird.

**Bruchdehnung A vs. A5 vs. A min:** Ein bloßes „A [%]" ohne weiteren Zusatz sowie „A5 [%]" werden beide nach `a5` gespeichert. Nur bei explizitem „min"/„Amin" im Spaltenkopf geht der Wert nach `a_min`.

---

## 🧪 Werkstoffgenerator & Werkstoff ergänzen

GUI → Menü **Import/Export → 🪄 Werkstoffgenerator …** (neuer Werkstoff) bzw. Detailansicht → **🧪 Werkstoff ergänzen** (bestehenden Werkstoff auffüllen)

Anders als der KI-Import (der vorhandene Datenblattwerte *ausliest*) **berechnet** der Generator fehlende Kennwerte aus wenigen Eingaben (Rm, Werkstoffgruppe, optional Rp0,2/A5/E-Modul): Wechselfestigkeiten σWzd/σWb/σSchzd/τWt/τWs sowie die zyklischen Kennwerte K'/n'/σf'/b/εf'/c.

- **Neuer Werkstoff** → legt einen neuen Werkstoff an (Bemerkung automatisch *„Berechnet, nicht gemessen"*) oder exportiert direkt als `.ffd`.
- **Bestehender Werkstoff ergänzen** → Feld-für-Feld-Vergleich zwischen aktuellem DB-Stand und Vorschlag; nur angehakte, tatsächlich leere Felder werden übernommen.
- Beide Dialogfenster sind **frei skalierbar** (inkl. Mindestgröße) und die Vergleichstabelle sitzt in einem **Scrollbereich mit Mausrad-Unterstützung** — bei vielen Feldern bleibt immer alles erreichbar, unabhängig von der Fenstergröße.

> ⚠️ **Alle berechneten Werte sind Näherungen aus öffentlich dokumentierten Ingenieurformeln** (FKM-Gruppenverhältnisse, Uniform Material Law nach Bäumel & Seeger 1990) — **keine Reproduktion einer bestimmten kommerziellen Software**. Vor sicherheitsrelevanter Verwendung: mit Literatur- oder Versuchswerten gegenprüfen. Details je Formel stehen als Kommentare in `gui/werkstoff_formeln.py` und `gui/fkm_formeln.py`.

---

## 📈 Kurven-Generatoren (Spannungs-Dehnung & Wöhlerkurve)

Zwei zusätzliche Tabs im Werkstoff-Editor — **reine Visualisierung**, es wird nichts in die Datenbank geschrieben. Beide Kurven werden live aus bereits vorhandenen Kennwerten berechnet und erscheinen automatisch auch im PDF-Datenblatt.

**📉 Spannungs-Dehnungs-Diagramm** — idealisierte 14-Punkte-Kurve aus E-Modul, Streckgrenze **oder** Dehngrenze, Zugfestigkeit und Bruchdehnung. Zwei Varianten je nach hinterlegtem Kennwert (mit/ohne ausgeprägte Streckgrenze).

**📊 Wöhlerkurve** — idealisierte Drei-Geraden-Konstruktion (statische Festigkeit → Zeitfestigkeit → Dauerfestigkeit), alle Beanspruchungsarten (Zug/Druck, Biegung, Torsion) gemeinsam farblich getrennt in einem Diagramm.

**🔧 Automatischer Werte-Ausgleich zwischen Kennwert-Zeilen:** Mechanische Kennwerte werden in dieser App teils über mehrere Zeilen verteilt gepflegt (z. B. Rm/Re durchmesserabhängig als Größeneinfluss-Tabelle). Steht ein für die Kurve nötiger Wert wie E-Modul oder A5 auf einer *anderen* Zeile als die für Rm ausgewählte — etwa weil er nach einem FFD-Import als eigene Zeile ohne Durchmesserbezug hinzukam — wird er automatisch von dort ergänzt, statt die Kurve fälschlich als „nicht berechenbar" zu melden.

> ⚠️ Beide sind **plausible Näherungskurven zwischen bekannten Eckwerten**, **keine echte Messkurve**. Fehlen die nötigen Basiswerte tatsächlich (auf keiner Zeile), erscheint ein präziser Hinweistext statt eines falschen Diagramms.

Konsistent in allen drei Oberflächen verfügbar — GUI-Tab, PDF-Datenblatt **und** Web-Frontend, alle nutzen dieselbe Zeichenlogik (`gui/kurven_charts.py`).

---

## 🧬 Chemie → Eigenschaften: Werkstoffvergleich & Einflussanalyse

GUI → Werkstoff-Detailansicht → Tab **Kennwerte → Einflussanalyse**, oder Menü **Chemie → 🧪 Eigenschaften: Werkstoffvergleich & Einflussanalyse …** (freier Vergleich zweier beliebiger Werkstoffe)

Zeigt für die tatsächlich hinterlegte chemische Zusammensetzung eines Werkstoffs, **welches Element bei diesem konkreten Werkstoff wie wirkt** — als Analyse-/Engineering-Hinweis mit Quelle, **nicht** als automatisch gültige Berechnung.

**Der entscheidende Punkt:** Die Wirkung eines Elements hängt stark von der Werkstofffamilie *und* dem konkreten Legierungssystem ab — Cr wirkt bei niedriglegiertem Stahl vor allem auf die Härtbarkeit, bei nichtrostendem Stahl dagegen vor allem auf die Passivierung/Korrosionsbeständigkeit (DIN EN 10088, PREN-Wert). Es gibt deshalb **keine globale Regel** „Cr ↑ → Korrosionsbeständigkeit ↑", sondern eine datengetriebene Architektur:

```
Werkstoff → Werkstofffamilie → Legierungssystem → Element → Regel → Eigenschaftseinfluss
```

| Ebene | Beispiel |
|---|---|
| Werkstofffamilie | `Fe-Basis`, `Al-Basis`, `Cu-Basis` (Ni-/Ti-/Mg-/Co-Basis bereits vorbereitet, noch ohne recherchierte Regeln) |
| Legierungssystem (optional, automatisch geschätzt) | „Nichtrostender Stahl (austenitisch)", „Werkzeugstahl", „Messing (CuZn)", „AlMgSi (6xxx)" — `None` = allgemeine Familien-Regel |
| Regel | Element, Eigenschaft, Richtung (↑/↓/↑↓/abhängig), **Wirkung** (qualitativer Text), **Gültigkeitsbereich**, **Bedingung** (wovon der Effekt zusätzlich abhängt), **Quelle**, **Regel-Status** (validiert/empfohlen/vorläufig) |

Automatisch erkannt: **Kupfer-** (`Cu`/`CW`/`CC`-Präfix) und **Aluminiumlegierungen** (`Al`/`EN AW`/`EN AC`-Präfix) bekommen eine eigenständige, für NE-Metalle passende Wissensbasis — **kein** „Fe bildet die Matrix"-Unsinn mehr bei einer Kupferlegierung. Die verdichtete Eigenschafts-Übersicht (Härte/Zähigkeit/Schweißeignung/Durchhärtbarkeit über CEV/ZTU) bleibt bewusst eine reine Stahl-Heuristik und zeigt bei NE-Metallen transparent „Nicht anwendbar" statt einer falschen Übertragung.

**⚙ Elementwirkungs-Regeln verwalten** (eigener Dialog, aus dem Analyse-Fenster oder dem Chemie-Menü erreichbar): Regeln lassen sich hier **ohne Codeänderung** anlegen, bearbeiten, deaktivieren oder löschen — filterbar nach Werkstofffamilie/Element. Genau darüber lassen sich künftig weitere Familien (Nickelbasis, Titan, Magnesium, Kobalt) oder feinere Legierungssysteme ergänzen.

> ⚠️ Jede Regel ist ein **qualitativer** Hinweis („kann … beeinflussen", „abhängig von …"), keine Zahlenwert-Behauptung. Der Disclaimer-Banner ist in jeder Ansicht permanent sichtbar.

---

## 📑 Norm-Update-Assistent

GUI → Menü **Import/Export → 📑 Norm-Update-Assistent …**

Lädt eine neue PDF-Fassung einer bereits im Register vorhandenen Norm hoch (Datei-Dialog **oder** Drag & Drop), lässt eine KI den Inhalt mit dem aktuellen DB-Stand vergleichen und zeigt ein Änderungsprotokoll. **Nichts wird automatisch übernommen** — jede Zeile muss einzeln bestätigt werden.

---

## 🔍 Norm-Status-Prüfung (KI)

GUI → Menü **Import/Export → 🔍 Norm-Status prüfen (monatliche Prüfliste) …**

Prüft **nur**, ob die hinterlegte Ausgabe einer Norm noch aktuell ist — per Websuche über ein OpenRouter-Modell mit Websuche-Fähigkeit. Findet das Modell keine belastbare Quelle, wird das Ergebnis als „unsicher" markiert statt geraten. Übernahme erfordert einen expliziten Klick.

---

## 📄 FFD-Export & FFD-Import (FKM 2002)

GUI → **📄 FFD Export** / **📥 FFD Import** (Detailansicht) oder Menü **Import/Export → FFD (FKM 2002) exportieren/importieren …**

**Export** schreibt den aktuell ausgewählten Werkstoff als `.ffd`-Datei (STEYR/FEST-FILE-Format 2.0) für FKM-2002-basierte Betriebsfestigkeitsauswertungen. **Import** liest umgekehrt eine `.ffd`-Datei ein — z. B. aus einem eigenen Versuch oder einer anderen Werkstoffdatenbank — und legt die erkannten Werte als **neue** Zeile bei den mechanischen bzw. dynamischen Eigenschaften ab, ohne bestehende Zeilen zu verändern.

**Automatisch verwendete/befüllte DB-Felder:**

| .ffd-Inhalt | Datenbankfeld |
|---|---|
| Rm, Rp0,2 | `MechEigenschaft.rm`, `.rp02` |
| E-Modul, A5, HB | `MechEigenschaft.e_modul`, `.a5`, `.hb` |
| σWzd, σWb, τWt | `DynamischeEigenschaft.sigma_wzd`, `.sigma_wb`, `.tau_wt` |
| K', n', σf', b, εf', c | `DynamischeEigenschaft.k_strich`, `.n_strich`, `.sigma_f_strich`, `.b_exponent`, `.eps_f_strich`, `.c_exponent` |

Fehlen dynamische Kennwerte beim Export, greift automatisch ein **Fallback** über das FKM-Wechselfestigkeitsverhältnis (σW ≈ Faktor × Rm, je Werkstoffgruppe zwischen 0,34 und 0,45).

**Beim Import ist jeder extrahierte Wert vor dem Speichern editierbar** — das Dateiformat wurde nur durch Analyse realer Beispieldateien rekonstruiert (keine offizielle Spezifikation), Dateien aus anderer Software können in Details abweichen. Ein Warnhinweis macht das im Prüfdialog transparent.

<details>
<summary>🔍 Genauigkeit & offene Punkte je Feld</summary>

| Feld | Status |
|---|---|
| Rm, Rp0,2 | sicher |
| σWzd/σWb/τWt | sicher (DB-Wert) bzw. Näherung (FKM-Fallback) |
| A5, HB | sicher |
| K', n', σf', b, εf', c | Näherung (Uniform Material Law), Abweichung ~15–35 % |

</details>

---

## 🌍 Mehrsprachigkeit (Web & PDF)

Sowohl die **Web-Oberfläche** als auch das **PDF-Datenblatt** sind komplett übersetzt — Buttons, Labels, Tabs, Statustexte, Fehlermeldungen, Tabellenüberschriften. Die **eingegebenen Daten** bleiben unverändert in der Sprache, in der sie erfasst wurden.

```
🇩🇪 Deutsch   🇬🇧 English   🇫🇷 Français   🇪🇸 Español
```

| Ebene | Datei | Mechanismus |
|---|---|---|
| Web-Frontend | `frontend/static/js/i18n.js` | `t(key)`, Sprache in `localStorage` |
| Backend / API-Fehlermeldungen | `backend/i18n.py` | `X-Lang`-Header |
| PDF-Datenblatt | `backend/i18n.py` (`pdf_*`-Schlüssel) | Query-Parameter `?lang=de\|en\|fr\|es` |

Direkter Aufruf in gewünschter Sprache: `GET /api/werkstoffe/{id}/datenblatt.pdf?lang=en`

---

## 🖥 GUI-Mehrsprachigkeit (im Aufbau)

Die Desktop-GUI enthält seit Kurzem die **technische Grundlage** für dieselbe 4-Sprachigkeit wie die Web-Oberfläche:

- **`gui/i18n.py`** — zentrale Übersetzungstabelle, strukturell an `frontend/static/js/i18n.js` angelehnt, mit `L(schlüssel)`-Lookup und sicherem Fallback (fehlende Übersetzung → Deutsch → Schlüsselname)
- **`gui/sprache_config.py`** — persistiert die gewählte Sprache in `data/sprache_settings.json`
- **Menü 🌐 Sprache** im Hauptfenster — Auswahl wird gespeichert, wirkt aber erst **nach einem Neustart** der Anwendung (bewusste Design-Entscheidung: anders als der Browser hat Tkinter keinen "Reload"-Mechanismus, ein Live-Umschalten müsste jedes offene Fenster aktiv neu aufbauen)

**Aktueller Stand:** Die Infrastruktur steht und ist mit einem Kern-Wortschatz (Speichern/Abbrechen/Schließen/Löschen/… sowie dem Fenstertitel) startklar vorbelegt. Die vollständige Übersetzung der insgesamt rund 1.400 in der GUI fest codierten deutschen Textstellen (über 40 Dateien) ist ein **laufendes, schrittweise fortgeführtes Vorhaben** — nicht migrierte Stellen bleiben bis dahin auf Deutsch, die App funktioniert währenddessen jederzeit vollständig.

---

## 🔢 Werkstoff-ID, Revision & Anzeigename

Jeder neue Werkstoff bekommt automatisch:

| Feld | Beispiel | Vergabe |
|---|---|---|
| `werkstoff_id_nr` | `M00001` | Fortlaufend, 5-stellig, nicht editierbar |
| `revision` | `001` | Start immer bei `001` |

**Anzeigename:** Um Werkstoffe mit gleichem Grundnamen, aber unterschiedlichem Behandlungszustand oder Beschichtung eindeutig zu unterscheiden, wird überall automatisch gebildet:

```
Kurzname + "+" + Behandlungszustand + "+" + Beschichtungsart
```

Beispiele: `S235JR` (kein Zusatz gesetzt) · `S235JR+N` · `RSt37-2+N`. Ist keines der beiden Felder gesetzt, entspricht der Anzeigename genau dem Kurznamen.

---

## 🖥️ GUI im Überblick

**Tabs im Detailbereich** (in dieser Reihenfolge):

| Tab | Inhalt |
|---|---|
| 📏 Normen | Zuordnen/entfernen, Status-Anzeige, **⬇ Download-Button** für angehängte Norm-PDFs |
| 🚚 Liefernormen | Halbzeug, Lieferant, Bezeichnung, PDF-Anhang je Liefernorm |
| 🧪 Zusammensetzung | **32 Hauptelemente**, jeweils Min UND Max, inkl. offener Liste weiterer Elemente |
| 🧬 Einflussanalyse | Regelbasierte [Chemie → Eigenschaften](#-chemie--eigenschaften-werkstoffvergleich--einflussanalyse)-Analyse für den geöffneten Werkstoff |
| ⚙️ Mechanisch | Rm (Einzelwert und/oder Rm-von/-bis-Bereich), Re, ReL, Rp0,2, Rp1, A5, A min, Z, KV, HB, HRC, E-Modul u. v. m. — je Temperatur, Durchmesserbereich & Probestück-Art |
| 📉 Spannungs-Dehnung | Live berechnetes Diagramm |
| 🌡️ Physikalisch | Dichte, λ, cp, α, ß, ρel, E dyn, E (statisch), G, χ, ν — je Temperatur |
| 🔁 Dynamische Eigenschaften | σWb, σWzd, σSchzd, τWt, τWs, K1C — je Durchmesserbereich |
| 📊 Wöhlerkurve | Live berechnete Wöhlerkurve mit Dropdown Zug-Druck/Biegung/Torsion |
| 🔥 Wärmebehandlung | Art, Medium, Temperaturbereich, Dauer |
| 🔩 Härte | Analyseverfahren, HRC/HB/HV als Min–Max-Spanne, HAT |
| 🔬 Reinheitsgrad | Durchmesserbereich, K2/K3/K4-Kennzahlen |
| 📄 Dokumente | Notizen + PDF-Anhänge |
| 🔗 Nachfolger & Alternativen | Verknüpfung zu Nachfolge- und Alternativwerkstoffen |
| ℹ️ Allgemein | Behandlungszustand, Beschichtungsart, Schmelzbereich, Anwendungsgebiete, Bemerkung |

**Aktionsleiste in der Detailansicht:** ✎ Bearbeiten · 📥 CSV importieren · 🖶 PDF drucken · ⚙ ANSYS Export · 📐 FFD Export · 📥 FFD Import · 🧪 Werkstoff ergänzen

**Chemie-Menü:** 🧪 Eigenschaften: Werkstoffvergleich & Einflussanalyse · ⚙ Elementwirkungs-Regeln verwalten

**Sprache-Menü:** 🌐 Deutsch / English / Français / Español (siehe [GUI-Mehrsprachigkeit](#-gui-mehrsprachigkeit-im-aufbau))

**Stammdaten-Menü:** Normen-Register, Werkstoffgruppen, Dokumente/Richtlinien-Register, Zusatzsymbol-Register (Behandlungszustand, Beschichtungsart, Halbzeug, Lieferant).

**Import/Export-Menü:** CSV-Import · 🤖 KI-Import · 🪄 Werkstoffgenerator · 📑 Norm-Update-Assistent · 🔍 Norm-Status prüfen · FFD-Export/-Import

---

## 🌐 Web-App im Überblick

- 🔍 Freitextsuche + Filter nach Gruppe/Status
- 📋 Header: Anzeigename, Werkstoff-ID, Revision, Werkstoffnummer, Status, Schmelzbereich, Änderungsdatum
- 🏷️ **Normen** rein lesend mit Status-Badge und **⬇ PDF-Download**
- 🧹 **Automatische Spaltenausblendung**: durchgängig leere Spalten werden ausgeblendet
- ⬇️ Direkter PDF-Download aus dem Dokumente-Tab sowie des kompletten, mehrsprachigen Werkstoffdatenblatts:
  ```
  GET /api/dokumente/{id}/pdf
  GET /api/werkstoffe/{id}/datenblatt.pdf?lang=de|en|fr|es
  ```

---

## 🗃 Datenmodell

Kern-Tabellen (SQLAlchemy, `backend/models.py`): `werkstoffe`, `werkstoffgruppen`, `normen`, `norm_status_pruefungen`, `liefernormen`, `chem_zusammensetzung` (32 Hauptelemente, alle mit Min/Max), `chem_zusatzelemente`, `mech_eigenschaften`, `phys_eigenschaften`, `dynamische_eigenschaften` (inkl. `k_strich`/`n_strich`/`sigma_f_strich`/`b_exponent`/`eps_f_strich`/`c_exponent`), `waermebehandlungen`, `haerte_werte`, `reinheitsgrade`, `dokumente`, `zusatzsymbole`, `werkstoff_alternativen`, `werkstoff_revisionen`, **`elementwirkung_regeln`** (Werkstofffamilie, Legierungssystem, Element, Eigenschaft, Richtung, Wirkung, Gültigkeitsbereich, Bedingung, Quelle, Regel-Status — siehe [Chemie → Eigenschaften](#-chemie--eigenschaften-werkstoffvergleich--einflussanalyse)).

Für die vollständige, immer aktuelle Feldliste ist `backend/models.py` maßgeblich.

---

## 🔌 API-Referenz

Vollständige, interaktive Referenz unter `/docs` (Swagger) bzw. `/redoc`, sobald die Web-App läuft. Wichtigste Endpunkte:

| Endpunkt | Zweck |
|---|---|
| `GET /api/werkstoffe` | Liste, mit Such-/Filterparametern |
| `GET /api/werkstoffe/{id}` | Detail |
| `GET /api/werkstoffe/{id}/datenblatt.pdf?lang=` | PDF-Datenblatt |
| `GET /api/normen` | Normen-Register |
| `GET /api/normen/{id}/pdf` | Norm-PDF-Anhang |
| `GET /api/dokumente/{id}/pdf` | Dokument-PDF-Anhang |
| `POST /api/ki-import/...` | KI-Import-Backend (siehe README_werkstoff_import.md) |

---

## 📥 CSV-Import

GUI: Werkstoff auswählen → **📥 CSV importieren**

```text
# Mechanisch
temperatur;rm;rp02;a5;z;kv;hb;hrc;e_modul;quelle
20;700;490;14;40;35;210;;210;DIN EN 10083-2

# Physikalisch
temperatur;dichte;waermeleitf;spez_waerme;ausdehn_koeff;el_widerstand;quelle
20;7.85;48.0;490;11.5;18.0;Richtwert
```

Trennzeichen `;` oder `,` — wird automatisch erkannt.

---

## 📄 PDF-Datenblatt

GUI → **🖶 PDF drucken** · Web-App → **📄 PDF erstellen**

DIN-A4-Datenblatt mit Kopfzeile, Allgemeinen Angaben, zugeordneten Normen, Liefernormen, Zusammensetzung (**inkl. eigener Tabelle „Weitere Elemente"**, sofern welche hinterlegt sind), Mechanischen/Physikalischen/Dynamischen Eigenschaften, Spannungs-Dehnungs-Diagramm und Wöhlerkurve (sofern berechenbar), Wärmebehandlung, Härte, Reinheitsgrad und Bemerkung.

- **Nur belegte Felder/Diagramme** erscheinen — leere Spalten werden automatisch ausgeblendet
- **4 Sprachen** für alle Feld-/Spaltenbezeichnungen
- Unicode-Sonderzeichen (⌀, ², µ, ⁻⁶, ≤, ν, χ, °) über eingebettete Schriftart (DejaVu Sans)

---

## ⚙️ ANSYS-Export

GUI → **⚙ ANSYS Export**

| Format | Datei | Ziel |
|---|---|---|
| APDL-Makro | `.mac` | ANSYS Mechanical APDL |
| MatML 3.1 XML | `.xml` | ANSYS Workbench → Engineering Data |

**Automatische Einheitenkonvertierung:**

| Eigenschaft | Datenbank | ANSYS |
|---|---|---|
| E-Modul | GPa | Pa (×10⁹) |
| Dichte | g/cm³ | kg/m³ (×1000) |
| Ausdehnungskoeff. | 10⁻⁶/K | 1/K (×10⁻⁶) |
| El. Widerstand | µΩ·cm | Ω·m (×10⁻⁸) |

---

## 📎 PDFs zu Dokumenten & Normen

**Dokumente** (Notizen, Datenblätter, Prüfberichte — je Werkstoff): Werkstoff → Tab **Dokumente** → **+ Neu** → Titel + Typ wählen → **📎 PDF wählen** → Speichern.

**Normen** (zentrales Stammdaten-Register): Stammdaten → **Normen verwalten …** → Norm auswählen/anlegen → **📎 PDF wählen** → Speichern. Überall dort, wo diese Norm einem Werkstoff zugeordnet ist, erscheint automatisch ein **⬇ Download-Button**.

Alle PDFs werden base64-kodiert **in der Datenbank** gespeichert — keine externe Dateiablage.

> ⚠️ Für PDFs > 10 MB empfiehlt sich externe Ablage mit Pfad-Referenz statt DB-Speicherung (Base64-Overhead ~33 %).

---

## 📶 Netzwerkzugriff (Handy/Tablet)

```powershell
python -m uvicorn backend.main:app --host 0.0.0.0 --port 8000
```

Dann im selben WLAN über `http://<PC-IP-Adresse>:8000` erreichbar — **nicht** `https://`.

Checkliste bei Verbindungsproblemen:
- ✅ Windows-Firewall: Port 8000 freigeben
- ✅ Netzwerkprofil auf **Privat** stellen
- ✅ iOS: iCloud Private Relay testweise deaktivieren
- ✅ Beide Geräte im **gleichen** WLAN

---

## 🛠 Troubleshooting

| Problem | Lösung |
|---|---|
| `No module named gui` | Falsches Verzeichnis — `cd app` bevor `python -m gui` |
| `no such column: ...` | Migration fehlt — `python migrate.py` ausführen, bei Unsicherheit vorher `python schema_diagnose.py` |
| Ein Dialog öffnet sich als **leeres, weißes Fenster** | Typisches Symptom einer Exception direkt in `__init__` — Terminal-Ausgabe prüfen |
| PDF zeigt "Kein PDF angehängt" trotz vorhandenem Anhang | `__pycache__`-Ordner löschen, Server/GUI neu starten |
| Werkstoff-ID wird nicht 5-stellig angezeigt | Einmalig `python migrate.py` ausführen |
| Ansicht nach FFD-Import/„Werkstoff ergänzen"/Generator nicht aktuell | Sollte automatisch passieren (Hauptfenster wartet auf Dialogschluss, bevor neu geladen wird) — falls doch nicht: `__pycache__` löschen, GUI neu starten |
| Web-App vom Handy nicht erreichbar | Siehe [Netzwerkzugriff](#-netzwerkzugriff-handytablet) |
| Kurven-Tab zeigt Hinweistext statt Diagramm | Fehlende Basiswerte — der Hinweistext nennt genau, was fehlt (siehe auch [automatischer Werte-Ausgleich](#-kurven-generatoren-spannungs-dehnung--wöhlerkurve)) |
| Elementwirkungs-Einflussanalyse zeigt „keine Regel hinterlegt" | Für dieses Element/diese Werkstofffamilie liegt noch keine Regel vor — über **⚙ Elementwirkungs-Regeln verwalten** ergänzbar |
| FFD-Import: Werte wirken unplausibel | Format wurde per Reverse-Engineering rekonstruiert — jeder Wert ist vor dem Speichern editierbar, bitte im Prüfdialog kontrollieren |
| Sprachumschaltung in der GUI zeigt keine Wirkung | Erwartbar — wirkt erst nach einem **Neustart** der Anwendung (siehe [GUI-Mehrsprachigkeit](#-gui-mehrsprachigkeit-im-aufbau)) |
| Berechnete FFD-/Generator-Werte weichen stark von einer bekannten Referenz ab | Erwartbar bei Näherungsformeln — für die betroffene Werkstoffgruppe fehlt ggf. noch eine kalibrierte Näherung |

---

<div align="center">

*Werkstoffdatenbank — intern entwickelt, für den täglichen Engineering-Einsatz.*
*Copyright (C) Noel Joan - 2026. Alle Rechte vorbehalten.*
</div>
