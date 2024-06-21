# Was ist ein Commit

Ein Commit ist ein Snapshot zu einem bestimmten Zeitpunkt vom Working-Directory.

Erstellen wir jetzt nochmal einen neuen Commit und schauen im Detail was passiert ist.

```bash
$ echo "ich bin die datei 2" > file2.txt

$ git add file2.txt

$ git commit -m "ich möchte nochmal commits erklären"
```

Jetzt schauen wir uns im git log nochmal die letzten zwei Commits an:

```bash
$ git log
commit 90c41286e4687cb13d0c3e36584f958f90a638d4 (HEAD -> main)
Author: Johannes Kleinlercher <johannes.kleinlercher@suxess-it.com>
Date:   Fri Jun 21 11:09:57 2024 +0200

    ich möchte nochmal commits erklären

commit 21dd03dc2d43468a27d42dc9cf97a2f2ba189078
Author: Johannes Kleinlercher <johannes.kleinlercher@suxess-it.com>
Date:   Thu Jun 20 16:54:47 2024 +0200

    das file gefällt mir nicht mehr
```

Lasst uns jetzt den Inhalt der beiden Commits nochmal anzeigen:

Commit 21dd03:
```bash
$ git ls-tree -r 21dd03
100644 blob d01e542adf015d6e7eaca9a08812a8f6b0ba7f24    neues-file.txt
```

Commit 90c412:
```bash
$ git ls-tree -r 90c412
100644 blob 634bb07288a6406463ebbc3f75d1423eac1958e9    file2.txt
100644 blob d01e542adf015d6e7eaca9a08812a8f6b0ba7f24    neues-file.txt
```
Format: `<mode> <type> <object>	<name>`

Ihr seht dass der Blob für die Datei `neues-file.txt` in beiden Commits die gleiche ID hat.

Man kann sich übrigens mit diesem Befehl auch den Inhalt des Blobs (also den Dateiinhalt) anzeigen lassen:

```bash
$ git cat-file -p d01e54
hallo ich bin da
das ist noch ein test
```

# Schematische Darstellung der beiden Commits im Git-Repository

Im Git-Repository sind diese beiden Commits und ihre Daten dann so gespeichert (schematisch):

![image](https://github.com/suxess-it/git-gitlab-gitops-schulung/assets/11465610/4dd7a864-8adf-4ead-82b9-a25c99b42162)


# Unterschied zwischen den beiden Commits anzeigen lassen

Mit `git diff` kann man sich die Änderungen zwischen zwei Commits anzeigen lassen:

```bash
$ git diff 21dd03..90c412
diff --git a/file2.txt b/file2.txt
new file mode 100644
index 0000000..634bb07
--- /dev/null
+++ b/file2.txt
@@ -0,0 +1 @@
+ich bin die datei 2
```

Wie erwartet wird ausgegeben, dass das file2.txt hinzugekommen ist und den neuen Inhalt vom file2.txt.

Das geht übrigens nicht nur zwischen zwei Commits die direkt hintereinander gemacht wurden, sondern auch zwischen dem 1. und 10. Commit!

# Einen bestimmten Commit auschecken

Man kann sich auch den Zustand eines bestimmten Commits nochmal in das Working-Directory holen - also auschecken.
Der Befehl dazu lautet `git checkout <commit-id>`

```bash
$ git log --oneline
90c4128 (HEAD -> main) ich möchte nochmal commits erklären
21dd03d das file gefällt mir nicht mehr
5f30ae4 nochmal
d6b4c14 noch eine aenderung
d0adc99 Jetzt aber ab ins Git-Repo mit dir!
decece9 das ist mein erstes file

$ git checkout decece9
# jede Menge Warnhinweise werden jetzt angezeigt - aktuell können wir das noch ignorieren
HEAD is now at decece9 das ist mein erstes file

$ ls
dasisteinfile.txt
```

Jetzt ist also im Working-Directory der Stand vom ersten Commit.

Um wieder auf den aktuellen Stand zurückzukommen, gebt statt der Commit-ID den Referenznamen `main` ein:

```bash
$ git checkout main
Switched to branch 'main'

$ ls
file2.txt  neues-file.txt
```

Zu Referenzen (Tags/Branches) kommen wir noch später, aber ihr könnt schon mal folgendes probieren:

```bash
$ cat .git/refs/heads/main
90c41286e4687cb13d0c3e36584f958f90a638d4
```

Was fällt euch auf?
