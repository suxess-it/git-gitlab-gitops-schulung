# Befehlsglossar

In folgender Tabelle werden nochmal die wichtigsten Befehle erklärt, die in diesem Scriptum verwendet werden.

| Befehl  | Erklärung |
| ------------- | ------------- |
| `mkdir <verzeichnis>` | "make directory" - erstellt ein Verzeichnis mit den Namen `<verzeichnis>`, Beispiel: mkdir project1 |
| `cd <verzeichnis>`   | "change directory" - wechselt in das Verzeichnis `<verzeichnis>`, Beispiel: cd project1  |
| `cd ~` | wechselt in das Home-Directory des Users |
| `pwd` | "print working directory" - gibt den aktuellen Pfad aus, ind dem man sich befindet |
| `touch <datei>` | legt eine leere Datei mit dem Namen `<datei>` an, Beispiel: touch dasisteinfile.txt |
| `rm <datei>` | löscht die Datei mit dem Namen `<datei>` |
| `echo "<text>" > <datei>` | schreibt den Text `<text>` in die Datei `<datei>` |
| `ls` | listet alle Dateien in diesem Verzeichnis auf |
| `git init` | initialisiert ein git-Repository in diesem Verzeichnis |
| `git status` | gibt aus, ob neue Files im Working-Directory oder Staging-Area liegen. Oder Unterschiede zum Remote-Repository |
| `git add <datei>` | fügt das File in die Staging-Area hinzu |
| `git add -A` | fügt alle neuen Files, alle geänderten Files, alle gelöschten Files (inkl. aller Unterverzeichnisse) in die Staging-Area |
| `git rm <datei>` | löscht die Datei im Working-Directory und in der Staging-Area |
| `git commit -m "<message>"` | committiert alles von der Staging-Area in das git-Repository mit der angegebenen Commit-Message |
| `git log` | gibt alle Commits inkl. Metadaten aus |
| `git log --oneline`| gibt alle Commits mit git-Hash und erster Zeile der Commit-Message aus |
| `git diff` | gibt alle Änderungen zwischen Working-Directory und Staging-Area aus |
| `git ls-files -s` | gibt alle Files in der Staging-Area aus |
| `git ls-tree -r main` | gibt alle Files im git-Repository aus im Branch `main` aus |
| `git cat-file -p <object>` | gibt den Inhalt oder Details zu einem git Objekt aus |
| `git checkout <commit>` | lädt den Stand des angegebenen Commits in das Working-Directory |
| `git restore --staged <datei>` | setzt die Änderungen von diesem File in der Staging-Area wieder zurück |
| `git restore <datei>` | setzt die Datei im Working-Directory wieder auf den Zustand in der Staging-Area zurück |
| `git restore --source=<commit> <datei>` | setzt die Datei im Working-Directory wieder auf den Zustand von Commit `<commit>` zurück |
| `git commit -a --amend --no-edit` | ersetzt den letzten Commit mit diesem neuen Commit und belässt die ursprüngliche Commit-Message |
| `git commit --amend -m "<message>"` | ersetzt die Commit-Message des letzten Commits mit der neuen Message |
| `git reset main~` | den letzten Commit aus dem git-Repository entfernen, die Änderungen aber im Working-Directory belassen |
| `git reset main~ --hard` | den letzten Commit im git-Repository und diese Änderungen auch im Working-Directory entfernen |
| `git revert <commit> --no-edit` | den Commit `<commit>` durch einen neuen Commit rückgängig machen, die Commit-Message soll `revert <old commit message>` lauten |
| `git rebase main~5 -i` | die letzten 5 Commits interaktiv verändern (löschen, umsortieren, Commit-Message ändern, ...) |
| `git checkout -b <branch>` | erstelle einen neuen Branch mit dem Namen `<branch>` und wechsle gleich auf den neuen Branch |
| `git branch <branch>` | erstelle einen neuen Branch mit dem Namen `<branch>` - bleibe aber in dem aktuellen Branch|
| `git switch <branch>` | wechsle in den Branch mit dem Namen `<branch>`|
| `git branch -d <branch>` | lösche den Branch mit dem Namen `<branch>`|
| `git rebase <branch1> <branch2>` | setze alle Commits vom Branch `<branch2>` auf den Branch `<branch1>` |
| `git merge <branch> --no-edit` | Merge die Änderungen vom Branch `<branch>` in deinen aktuell ausgecheckten Branch und verwenden die Default-Commit-Message für einen Merge-Commit |
| `git clone <Remote-Git-Repo-URL>` | Klont ein Remote-Repository in ein lokales Verzeichnis |
