# Nachhaltige Energiewirtschaft (Modul 32941, Einheit 6)

Begleitmaterial zu Kapitel 2 „Erneuerbare Energien und Preisbildung am Strommarkt“ des Studienbriefs *Nachhaltige Energiewirtschaft* (Modul 32941 „Nachhaltigkeit“, Einheit 6, Bucksteeg/Delic)

Dieses Repository enthält zwei Dateien, mit denen Sie das Merit-Order-Modell aus unterschiedlichen Perspektiven nachvollziehen können:

| Datei | Was sie tut | Programm |
|---|---|---|
| `Merit_Order_Notebook_32941.ipynb` | Visualisiert die Merit Order und erlaubt es, Nachfrage, erneuerbare Einspeisung und CO₂-Preis interaktiv zu verändern, ganz ohne Solver. Bezug: Abschnitte 2.2 und 2.3 | Visual Studio Code mit Jupyter |
| `BasisModell.gms` | Formuliert die kurzfristige Einsatzplanung als lineares Optimierungsproblem, bestimmt den kostenminimalen Kraftwerkseinsatz und den Marktpreis als Schattenpreis der Lastdeckungsbedingung. Bezug: Abschnitt 2.2.5 | GAMS Studio |

Beide Dateien verwenden dieselben Zahlen und Annahmen wie der Studienbrief
(Tabelle 7 und folgende).

> **Wichtiger Hinweis vorab:** Das Notebook wird **ohne gespeicherte Ergebnisse**
> ausgeliefert. Es wurde vor der Veröffentlichung über „Clear All Outputs“
> bereinigt und ist **nicht vorberechnet**. Alle Tabellen und Abbildungen
> entstehen erst, wenn Sie die Zellen selbst ausführen. Wenn Sie das Notebook
> öffnen und zunächst nur Text und Programmcode sehen, ist das also kein Fehler,
> sondern der Auslieferungszustand.

---

## Inhaltsverzeichnis

1. [Repository herunterladen](#1-repository-herunterladen)
2. [Was Sie insgesamt installieren](#2-was-sie-insgesamt-installieren)
3. [Teil A: Python, VS Code und das Jupyter-Notebook](#teil-a-jupyter-notebook)
   - [A.1 Python installieren](#a1-python-installieren)
   - [A.2 Visual Studio Code installieren](#a2-visual-studio-code-installieren)
   - [A.3 Erweiterungen Python und Jupyter installieren](#a3-erweiterungen-python-und-jupyter-installieren)
   - [A.4 Benötigte Pakete installieren](#a4-benötigte-pakete-installieren)
   - [A.5 Notebook öffnen, Kernel wählen, ausführen](#a5-notebook-öffnen-kernel-wählen-ausführen)
   - [A.6 Wenn eine Fehlermeldung ein fehlendes Paket anzeigt](#a6-wenn-eine-fehlermeldung-ein-fehlendes-paket-anzeigt)
   - [A.7 Weitere häufige Probleme](#a7-weitere-häufige-probleme)
4. [Teil B: GAMS einrichten und `BasisModell.gms` rechnen](#teil-b-gams)
   - [B.1 GAMS installieren](#b1-gams-installieren)
   - [B.2 Lizenz einrichten](#b2-lizenz-einrichten)
   - [B.3 HiGHS als Standardsolver einstellen](#b3-highs-als-standardsolver-einstellen-wichtig)
   - [B.4 Modell öffnen und starten](#b4-modell-öffnen-und-starten)
   - [B.5 Ergebnisse ansehen: GDX, Listing, Excel](#b5-ergebnisse-ansehen-gdx-listing-excel)
   - [B.6 Häufige Fehlermeldungen in GAMS](#b6-häufige-fehlermeldungen-in-gams)
5. [Welche Abschnitte wann bearbeitet werden](#5-welche-abschnitte-wann-bearbeitet-werden)

## 1. Repository herunterladen

Sie brauchen kein Git-Wissen. Zwei Wege stehen zur Auswahl:

**Weg 1 (empfohlen, ohne Zusatzsoftware):**
Auf der Startseite des Repositories auf den grünen Button **Code** klicken, dann
**Download ZIP**. Anschließend das Archiv entpacken, zum Beispiel nach
`Dokumente\Modul32941`.

**Weg 2 (mit Git):**

```bash
git clone https://github.com/fuh-energy/Nachhaltige-Energiewirtschaft.git
```

Empfehlung zum Speicherort: Legen Sie den Ordner **lokal** ab, nicht in einem
synchronisierten Cloud-Ordner (OneDrive, Dropbox, iCloud). GAMS legt beim Rechnen
mehrere temporäre Dateien an, die von der Synchronisierung gesperrt werden können.
Vermeiden Sie außerdem sehr lange Pfade und Sonderzeichen im Pfadnamen.

## 2. Was Sie insgesamt installieren

| Für | Software | Kosten | Ungefährer Zeitbedarf |
|---|---|---|---|
| `Merit_Order_Notebook_32941.ipynb` | Python 3.12, Visual Studio Code, Erweiterungen „Python“ und „Jupyter“, vier Python-Pakete | kostenlos | 20 bis 30 Minuten |
| `BasisModell.gms` | GAMS inklusive GAMS Studio, dazu eine kostenlose Lizenz | kostenlos für Studium und Lehre | 20 bis 30 Minuten |

Beide Teile sind voneinander unabhängig. Sie können mit dem Notebook beginnen und
GAMS später einrichten oder umgekehrt.

# Teil A: Jupyter-Notebook

Das Notebook läuft ohne GAMS und ohne Solver. Vorkenntnisse in Python sind nicht
erforderlich. Sie führen die Zellen lediglich in der vorgegebenen Reihenfolge aus.

## A.1 Python installieren

Das Notebook wurde **mit Python 3.12.3 erstellt und getestet**. Verwenden Sie
bitte eine Version aus der Reihe **3.12**.

1. Öffnen Sie **<https://www.python.org/downloads/>**, dort den Bereich
   „Looking for a specific release?“, und wählen Sie eine Version **3.12.x**.
2. **Windows:** Laden Sie den „Windows installer (64-bit)“ herunter. Setzen Sie
   im ersten Installationsdialog unbedingt das Häkchen bei
   **„Add python.exe to PATH“**, bevor Sie auf „Install Now“ klicken. Ohne dieses
   Häkchen findet VS Code die Installation später oft nicht.
3. **macOS:** Laden Sie den „macOS 64-bit universal2 installer“ herunter und
   folgen Sie dem Installationsassistenten. (Das mit macOS mitgelieferte Python
   ist für unsere Zwecke nicht geeignet.)
4. **Linux:** Nutzen Sie die Paketverwaltung Ihrer Distribution, unter
   Ubuntu beispielsweise `sudo apt install python3.12 python3.12-venv`.

Sollten Sie bereits über Python auf ihrem Computer verfügen, prüfen Sie ggf. die Installation in der Eingabeaufforderung bzw. im Terminal:

```bash
# Windows
py --version

# macOS und Linux
python3 --version
```

Die Ausgabe sollte mit `Python 3.12.` beginnen.

## A.2 Visual Studio Code installieren

1. Öffnen Sie **<https://code.visualstudio.com/download>**
2. Wählen Sie das Paket für Ihr Betriebssystem und installieren Sie es mit den
   Standardeinstellungen. Unter Windows empfiehlt sich, die Option
   „Open with Code“ für Ordner mit zu aktivieren.

VS Code ist ein Editor, der Jupyter-Notebooks direkt anzeigen und ausführen kann.
Ein separater Browser-basierter Jupyter-Server ist nicht nötig.

## A.3 Erweiterungen Python und Jupyter installieren

Beide Erweiterungen stammen von Microsoft und sind kostenlos.

1. Starten Sie VS Code.
2. Öffnen Sie die Seitenleiste **Extensions**: Symbol mit den vier Quadraten in
   der linken Leiste, oder Tastenkombination `Strg + Umschalt + X`
   (macOS: `Cmd + Umschalt + X`).
3. Suchen Sie nach **`Python`**. Wählen Sie den Eintrag **Python** von
   *Microsoft* und klicken Sie auf **Install**. Die Erweiterung „Pylance“ wird
   automatisch mitinstalliert.
4. Suchen Sie anschließend nach **`Jupyter`**. Wählen Sie den Eintrag **Jupyter**
   von *Microsoft* und klicken Sie ebenfalls auf **Install**. Auch hier werden
   mehrere zugehörige Erweiterungen (unter anderem für die Zellenausgabe und die
   interaktiven Regler) automatisch mitinstalliert.
5. Starten Sie VS Code einmal neu.

Kontrolle: Unter *Extensions > Installed* müssen jetzt sowohl „Python“ als auch
„Jupyter“ aufgeführt sein.

## A.4 Benötigte Pakete installieren

Das Notebook benötigt vier Pakete:

| Paket | Wofür |
|---|---|
| `pandas` | Tabellen (Kraftwerkspark, Merit-Order-Tabellen, Preistabellen) |
| `numpy` | Numerische Berechnungen |
| `matplotlib` | Abbildungen 11 bis 14 |
| `ipywidgets` | Die interaktiven Regler für Nachfrage, Wind, PV und CO₂-Preis |

Öffnen Sie zunächst den Kursordner in VS Code: **File > Open Folder**, dann den
entpackten Repository-Ordner auswählen. Öffnen Sie anschließend ein Terminal in
VS Code: **Terminal > New Terminal** oder `Strg + Ö` (macOS: `Ctrl + ö`).

**Empfohlener Weg mit virtueller Umgebung.** Eine virtuelle Umgebung hält die
Pakete dieses Kurses von Ihrer übrigen Python-Installation getrennt. Das erspart
Ihnen später Versionskonflikte.

```bash
# Windows
py -3.12 -m venv .venv
.venv\Scripts\activate
python -m pip install --upgrade pip
pip install pandas numpy matplotlib ipywidgets

# macOS und Linux
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install pandas numpy matplotlib ipywidgets
```

Liegt im Repository eine Datei `requirements.txt`, genügt statt der letzten Zeile:

```bash
pip install -r requirements.txt
```

**Einfacher Weg ohne virtuelle Umgebung.** Wenn Sie auf die Trennung verzichten
möchten:

```bash
# Windows
py -m pip install pandas numpy matplotlib ipywidgets

# macOS und Linux
python3 -m pip install pandas numpy matplotlib ipywidgets
```

## A.5 Notebook öffnen, Kernel wählen, ausführen

1. Klicken Sie in der Dateiliste links auf **`Merit_Order_Notebook_32941.ipynb`**.
2. **Kernel auswählen:** Oben rechts im Notebook steht ein Button
   **„Select Kernel“**. Klicken Sie darauf, wählen Sie
   *Python Environments* und dort Ihre Umgebung aus: bei Nutzung einer virtuellen
   Umgebung den Eintrag mit `.venv`, sonst die Installation **Python 3.12.x**.
   Ohne ausgewählten Kernel lässt sich keine Zelle ausführen.
   Wenn VS Code Sie beim ersten Öffnen fragt, ob die empfohlenen Erweiterungen
   installiert werden sollen, bestätigen Sie das.
3. **Ausführen:** Einzelne Zelle mit `Umschalt + Enter`. Alle Zellen
   nacheinander mit dem Button **Run All** in der Leiste oberhalb des Notebooks.
4. **Reihenfolge einhalten:** Die Zellen bauen aufeinander auf. Abschnitt 1
   („Vorbereitung“) muss immer zuerst laufen, weil dort die Funktionen definiert
   und die Regler vorbereitet werden. Wenn Sie mittendrin einsteigen, erhalten
   Sie `NameError`-Meldungen.

**Zur Erinnerung:** Das Notebook enthält bewusst **keine gespeicherten
Ergebnisse**. Alle Tabellen und Abbildungen entstehen erst durch Ihre eigenen
Läufe. Wenn Sie zwischendurch aufräumen möchten, verwenden Sie den Befehl
**Clear All Outputs** in der Notebook-Leiste. Damit kehren Sie in den
Auslieferungszustand zurück, ohne dass Inhalte verloren gehen.

Wenn alles funktioniert, sehen Sie in Abschnitt 5 die
Angebotskurve mit gestrichelter Nachfragelinie und darüber Schieberegler für
**Nachfrage** und **CO₂-Preis**.

## A.6 Wenn eine Fehlermeldung ein fehlendes Paket anzeigt

Die typische Meldung lautet:

```
ModuleNotFoundError: No module named 'pandas'
```

Statt `pandas` kann dort auch `numpy`, `matplotlib` oder `ipywidgets` stehen. Die
Ursache ist immer dieselbe: Das genannte Paket fehlt in genau der Python-Umgebung,
die als Kernel ausgewählt ist. Dafür gibt es drei verschiedene Lösungswege (abgestuft nach steigendem Aufwand):

**Weg 1: Der Vorschlag von VS Code.** In vielen Fällen blendet VS Code direkt
unter der Fehlermeldung einen Button **„Install“** oder einen Hinweis
„Install packages“ ein. Ein Klick genügt.

**Weg 2: Installation direkt aus dem Notebook heraus.** Legen Sie eine neue
Zelle ganz oben an und führen Sie sie aus:

```python
%pip install pandas numpy matplotlib ipywidgets
```

Das Präfix `%pip` (nicht `!pip`) stellt sicher, dass in **die aktuell aktive
Kernel-Umgebung** installiert wird. Anschließend den Kernel neu starten
(Button **Restart**) und die Zellen erneut ausführen.

**Weg 3: Über das Terminal.** Terminal in VS Code öffnen, gegebenenfalls die
virtuelle Umgebung aktivieren (siehe A.4) und den `pip install`-Befehl aus A.4
ausführen. Danach im Notebook den Kernel neu starten.

**Wenn der Fehler nach der Installation bestehen bleibt**, ist fast immer der
falsche Kernel ausgewählt: Sie haben in Umgebung A installiert, das Notebook
rechnet aber in Umgebung B. Prüfen Sie das mit einer Zelle:

```python
import sys
print(sys.executable)
print(sys.version)
```

Der ausgegebene Pfad muss zu der Umgebung gehören, in der Sie installiert haben
(bei virtueller Umgebung also einen Bestandteil `.venv` enthalten). Andernfalls
oben rechts über **Select Kernel** die richtige Umgebung wählen.

**Sonderfall `ipywidgets`.** Das Notebook ist bewusst so gebaut, dass es auch
**ohne** dieses Paket vollständig durchläuft. Fehlt es, erscheint der Hinweis
„Die interaktiven Regler sind nicht verfügbar“, und statt der Regler wird jeweils
das im Studienbrief verwendete Ausgangsbeispiel berechnet. Alle Tabellen und
Abbildungen entstehen trotzdem. Sie verlieren nur die Möglichkeit, Werte
interaktiv zu variieren.

## A.7 Weitere häufige Probleme

| Symptom | Ursache | Lösung |
|---|---|---|
| „Select Kernel“ zeigt keine Python-Umgebung an | Python nicht installiert oder nicht im Suchpfad | Python nach A.1 installieren, unter Windows mit dem Häkchen „Add python.exe to PATH“; danach VS Code neu starten |
| Regler werden als leeres Feld oder als Text `interactive(children=...)` angezeigt | Jupyter-Erweiterung oder Widget-Unterstützung nicht aktiv | Erweiterung „Jupyter“ nach A.3 installieren, VS Code neu starten, Kernel neu starten |
| `NameError: name 'TECH' is not defined` (oder `merit_order`, `de`, `CO2_BASE`) | Zellen wurden nicht in der Reihenfolge ausgeführt | **Run All** ab Abschnitt 1 ausführen |
| Abbildungen erscheinen nicht | Kernel wurde zwischendurch neu gestartet | **Run All** erneut ausführen |
| Zelle bleibt bei `[*]` stehen | Kernel rechnet noch oder hängt | Warten; falls nötig **Interrupt**, dann **Restart** und **Run All** |
| `pip` bricht mit Kompilierfehlern ab (`building wheel failed`) | Python-Version zu neu für die Pakete | Python 3.12.x installieren und als Kernel wählen (siehe A.1) |
| Umlaute oder das Zeichen € werden falsch dargestellt | Encoding-Problem des Editors | Sicherstellen, dass die Datei als UTF-8 geöffnet ist; unverändert aus dem Repository erneut herunterladen |
| Ergebnisse weichen von den Zahlen im Studienbrief ab | Eingabedaten wurden beim Experimentieren verändert | Notebook aus dem Repository erneut herunterladen; Ihre Änderungen vorher in einer Kopie sichern |

Sollten Sie mit einer Fehlermeldung trotz einhergehender Prüfung nicht weiterkommen, können Sie diese auch in ein KI-Tool Ihrer Wahl (bspw. ChatGPT oder Claude) eingeben und sich bei der Analyse und Fehlerbehebung unterstützen lassen.

# Teil B: GAMS

## B.1 GAMS installieren

1. Öffnen Sie die Downloadseite: **<https://www.gams.com/download/>**
2. Wählen Sie das Installationspaket für Ihr Betriebssystem (Windows 64 Bit, macOS mit Apple Silicon oder Intel, Linux). Für die Arbeit mit GAMS wird empfohlen, möglichst die aktuellste verfügbare Version herunterzuladen und zu installieren.
3. Installieren Sie mit den Standardeinstellungen. **GAMS Studio**, die grafische Arbeitsumgebung, wird dabei automatisch mitinstalliert. Sie brauchen keine weitere Entwicklungsumgebung.

## B.2 Lizenz einrichten

**Kostenlose Lizenz für Studierende (empfohlen):**

1. Rufen Sie die Seite des akademischen Programms auf:
   **<https://www.gams.com/academics/>**
2. Registrieren Sie sich im GAMS-Portal (**<https://portal.gams.com>**)
   **mit Ihrer Hochschul-E-Mail-Adresse** (Adresse der FernUniversität). Die
   Prüfung der Berechtigung erfolgt über diese Adresse.
3. Bestätigen Sie die Registrierungs-E-Mail. Dieser Schritt ist zwingend.
4. Erzeugen Sie im Portal eine kostenlose Lizenz und kopieren Sie den angezeigten Zugangscode
   (Access Code).
5. Klicken Sie oben in der Menüleiste auf Help und anschließend auf GAMS Licensing. Geben Sie im sich öffnenden Fenster unter Access Code Ihren Zugangscode ein und klicken Sie anschließend auf Install License. Danach können Sie das Fenster unten rechts mit OK schließen.

**Ohne Registrierung:** Der GAMS-Distribution liegt bereits eine zeitlich
befristete **Demo-Lizenz** bei. Das Modell dieses Kurses ist mit 54
Erzeugungsvariablen sehr klein und läuft auch unter der Demo-Lizenz. Diese ist allerdings nur 5 Monate gültig.

## B.3 HiGHS als Standardsolver einstellen (wichtig)

Bitte stellen Sie vor dem ersten Modelllauf den Solver **HiGHS** ein. Sonst rechnet
GAMS mit einem anderen Solver, und Sie erhalten in Zeitschritt 2 einen anderen
Preis als im Studienbrief.

HiGHS ist ein freier Solver und in jeder GAMS-Installation bereits enthalten. Sie
brauchen dafür keine zusätzliche Lizenz.

### So stellen Sie HiGHS dauerhaft ein

Diese Einstellung müssen Sie nur einmal vornehmen. Sie gilt danach für alle Ihre
GAMS-Modelle.

1. Klicken Sie in GAMS Studio oben in der Menüleiste auf **GAMS**.
2. Wählen Sie **Default GAMS Configuration**. Es öffnet sich ein Blatt mit dem
   Namen **`gamsconfig.yaml`**.
3. Geben Sie rechts im Suchfeld **Filter Parameters** den Text **`LP`** ein.
4. Wählen Sie in der Liste den Eintrag **LP** über das Auswahlmenü (Drop-down) aus.
   Rechts erscheint nun die Liste der verfügbaren Solver.
5. Suchen Sie in der Solver-Liste nach **HIGHS** und machen Sie einen
   **Doppelklick** darauf.
6. Im Fenster, das sich daraufhin öffnet, klicken Sie auf **Replace existing entry**.
7. Schließen Sie oben das geöffnete Blatt **`gamsconfig.yaml`** über das
   Kreuz am Reiter.
8. Es erscheint eine Rückfrage. Klicken Sie dort auf **Save**.

Fertig. HiGHS ist jetzt der voreingestellte Solver für lineare Modelle.

### Alternative für den einzelnen Modelllauf

Falls die Einstellung bei Ihnen nicht funktioniert oder Sie sie nicht dauerhaft
vornehmen möchten, können Sie den Solver auch direkt im Modell festlegen. Fügen
Sie dazu in `BasisModell.gms` unmittelbar **vor** der Zeile
`Solve merit_order using LP minimizing C_op;` diese Zeile ein:

```gams
option LP = HiGHS;
```

Diese Angabe im Modell hat Vorrang vor der Voreinstellung.

## B.4 Modell öffnen und starten

1. GAMS Studio starten.
2. **File > Open** und die Datei `BasisModell.gms` auswählen. Studio legt dafür
   automatisch ein Projekt an.
3. Modell starten: Button **Run** oder Taste **F9**.
4. Im Fenster **Process Log** (rechter Bereich) den Ablauf verfolgen. Der Lauf
   muss mit der Meldung **`Normal completion`** enden. Er dauert höchstens wenige Sekunden.

## B.5 Ergebnisse ansehen: GDX, Listing, Excel

Am Ende des Laufs schreibt das Modell die Zeile

```gams
execute_unload 'results_unitcommitment.gdx'
```

Damit landen **alle** Mengen, Parameter, Variablen und Gleichungen in der Datei
`results_unitcommitment.gdx` im Modellordner. Die GDX-Datei ist das eigentliche
Ergebnisformat von GAMS.

### B.5.1 Die GDX-Datei in GAMS Studio öffnen (Hauptweg, alle Betriebssysteme)

1. Nach erfolgreichem Lauf erscheint `results_unitcommitment.gdx` im
   `Project Explorer` links. **Doppelklicken** Sie die Datei. Studio öffnet den
   eingebauten **GDX-Viewer**.
2. Links sehen Sie die Liste aller Symbole (`i`, `t`, `D`, `y_max`, `c_var`,
   `y`, `C_op`, `objfunc`, `loadserve`, `maxcap`).
3. Klicken Sie auf ein Symbol, um seine Werte zu sehen. Für dieses Kapitel sind
   zwei Symbole entscheidend:

   | Symbol | Spalte | Bedeutung |
   |---|---|---|
   | `y` (Variable) | **Level** | Erzeugungsleistung je Kraftwerk und Zeitschritt in MW |
   | `loadserve` (Gleichung) | **Marginal** | Schattenpreis der Lastdeckung, also der Marktpreis in €/MWh |

### B.5.2 Einzelne Ergebnisse in ein Tabellenprogramm übernehmen

Wenn Sie mit einzelnen Ergebnissen aus der GDX-Datei weitere Auswertungen machen möchten, also
selbst summieren, sortieren, Differenzen bilden oder eigene Diagramme zeichnen,
übertragen Sie die Werte in ein Tabellenkalkulationsprogramm (Excel, LibreOffice
Calc, Google Tabellen):

- **Kopieren und einfügen:** Im GDX-Viewer die gewünschten Zeilen markieren, mit
  `Strg + C` (macOS: `Cmd + C`) kopieren und im Tabellenblatt einfügen. Achten
  Sie beim Einfügen auf die Dezimaltrennzeichen: GAMS gibt Punkte aus, deutsche
  Excel-Installationen erwarten Kommata. Um dies zu umgehen über *Daten > Text in Spalten* korrigieren.

### B.5.3 Die Listing-Datei

Unabhängig davon schreibt GAMS immer eine Listing-Datei `BasisModell.lst`. Sie
enthält den Solver-Bericht, den Zielfunktionswert sowie Level- und Marginalwerte
aller Variablen und Gleichungen. In Studio öffnen Sie sie mit einem Doppelklick
im Projektbaum. Für die Fehlersuche ist sie die erste Anlaufstelle.

## B.6 Häufige Fehlermeldungen in GAMS

| Meldung im Process Log | Ursache | Lösung |
|---|---|---|
| `*** No license found` | Keine oder abgelaufene Lizenz, oder der gewählte Solver ist nicht lizenziert | Lizenz nach Abschnitt B.2 einrichten; HiGHS nach B.3 einstellen |
| `Cannot execute gdxxrw.exe` oder Rückgabewert ungleich 0 am Ende | Kein Windows oder kein Excel installiert | Kein Fehler, siehe B.5.3. Mit der GDX-Datei weiterarbeiten |
| `Error 140`, `Unknown symbol` | Beim Bearbeiten des Codes ist ein Tippfehler entstanden | Zeilennummer im Log ansteuern; Original aus dem Repository erneut herunterladen |
| `Error 257`, `Solve statement not checked` | Ein Kompilierfehler weiter oben verhindert den Lauf | Erste Fehlermeldung im Log zuerst beheben, die folgenden sind meist Folgefehler |
| Lauf endet mit `Infeasible` | Nachfrage übersteigt die verfügbare Gesamtleistung; tritt nach eigenen Änderungen an `D(t)` oder `y_max(i)` auf | Werte prüfen |

## 5. Welche Abschnitte wann bearbeitet werden

Der Studienbrief enthält an den passenden Stellen Aufforderungsboxen. Sie geben
jeweils an, welche Abschnitte des Notebooks oder welche Modelldateien auszuführen
sind. Zur Orientierung:

| Studienbrief | Material | Abschnitte |
|---|---|---|
| Einstieg in Abschnitt 2.2, Grenzkosten (2.2.1) | Notebook | 1 bis 3 |
| Angebotskurve und Preisbildung (2.2.2, 2.2.3) | Notebook | 4 und 5 |
| Inframarginale Renten (2.2.4) | Notebook | 6 |
| Optimierungsproblem und Schattenpreis (2.2.5) | GAMS | `BasisModell.gms`, Schritt 1 |
| Merit-Order-Effekt (2.3.1, 2.3.2) | Notebook | 7 und 8 |
| CO₂-Preis und Brennstoffwechsel (2.3.3) | Notebook | 9 |
| Selbstkannibalisierung und Wertverfall (2.3.4) | Notebook | 10 |
| Zusammenfassung und Modellgrenzen | Notebook | 11 |

Die Übungsaufgaben in Abschnitt 2.4 und die Lösungshinweise in Kapitel 3 des
Studienbriefs setzen keine der beiden Dateien voraus, lassen sich mit ihnen aber
gut überprüfen.
