# ConFlow — Update-Kanal

Dieses Repository enthält ausschließlich den **Update-Kanal** der Mac-Anwendung ConFlow:

- `latest.json` — die Liste der jeweils aktuellen Version
- die signierten Update-Pakete als Release-Anhänge

Der **Quellcode liegt hier nicht** — er befindet sich in einem separaten, privaten Repository.

## Warum öffentlich?

Damit die Anwendung Updates laden kann, ohne einen Zugangsschlüssel mitzuliefern. Ein in der
Anwendung eingebauter Schlüssel wäre aus jeder ausgelieferten Kopie auslesbar und müsste
regelmäßig erneuert werden — läuft er unbemerkt ab, bricht die Update-Kette bei allen
Installationen ab, ohne dass es jemandem auffällt.

## Ist das sicher?

Ja. Die Sicherheit beruht nicht darauf, dass die Dateien schwer erreichbar sind, sondern auf
einer **kryptografischen Signatur**: Jedes Paket ist mit einem privaten Schlüssel signiert, der
den Rechner des Herausgebers nie verlässt. Die Anwendung prüft jede Signatur gegen den in ihr
hinterlegten öffentlichen Schlüssel und weist alles zurück, was nicht passt. Ein verändertes
oder untergeschobenes Paket wird dadurch abgelehnt.

## Aufbau von `latest.json`

Der Updater fragt nach einem exakten Stichwort, das davon abhängt, auf welchem Prozessor die
Anwendung läuft — `darwin-x86_64` auf Intel-Macs, `darwin-aarch64` auf Apple Silicon. Ein
Fallback gibt es nicht: Fehlt das passende Stichwort, erhält die Anwendung kein Update.

Ausgeliefert wird ein **Universal-Paket**, das beide Prozessortypen bedient. Es ist deshalb
unter **beiden** Stichwörtern eingetragen und verweist jeweils auf dieselbe Datei mit derselben
Signatur.
