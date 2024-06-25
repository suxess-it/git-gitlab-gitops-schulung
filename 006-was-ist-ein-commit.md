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

# Schematische Darstellung der beiden Commits im Git-Repository

Im Git-Repository sind diese beiden Commits und ihre Daten dann so gespeichert (schematisch):

![image](https://github.com/suxess-it/git-gitlab-gitops-schulung/assets/11465610/4dd7a864-8adf-4ead-82b9-a25c99b42162)

# Was ist der Inhalt des Commits

Lasst uns jetzt den Inhalt der beiden Commits nochmal durchforsten.<br>
Dazu brauchen wir nur einen Command, nämlich `git cat-file -p`

Commit 21dd03:

```bash
$ git cat-file -p 21dd03
tree bb1f5f12fc3e728e05c6f151615d7adef8f9c19b                                             # root tree des Root-Verzeichnisses des git-Projekts
parent 5f30ae453b691182449371eb95fd7c2304f60f12                                           # Parent Commit dieses Commits.
author Johannes Kleinlercher <johannes.kleinlercher@suxess-it.com> 1718895287 +0200       # Author
committer Johannes Kleinlercher <johannes.kleinlercher@suxess-it.com> 1718895287 +0200    # Committer

das file gefällt mir nicht mehr                                                           # Commit-Message
```

Und dann kann man sich auch die Files/Directorys in diesem Commit anschauen, indem man den SHA1-Hash des tree Objekts angibt:
```bash
$ git cat-file -p bb1f5f
100644 blob d01e542adf015d6e7eaca9a08812a8f6b0ba7f24    neues-file.txt
```
Format: `<mode> <type> <object>	<name>`

Und dann kann man sich noch den Inhalt des Files anschauen:

```bash
$ git cat-file -p d01e54
hallo ich bin da
das ist noch ein test
```

Das ganze jetzt mit dem nächsten Commit.

Commit 90c412:
```bash
$ git cat-file -p 90c412
tree 0cb430b69b864e989da70cca98ea19054c46d76f
parent 21dd03dc2d43468a27d42dc9cf97a2f2ba189078
author Johannes Kleinlercher <johannes.kleinlercher@suxess-it.com> 1718960997 +0200
committer Johannes Kleinlercher <johannes.kleinlercher@suxess-it.com> 1718960997 +0200

ich möchte nochmal commits erklären
```

Und wieder den Inhalt des tree-Objekts (also alle Files und Directories die sich im Basisverzeichnis des git-Projektes befinden):

```bash
$ git cat-file -p 0cb430
100644 blob 634bb07288a6406463ebbc3f75d1423eac1958e9    file2.txt
100644 blob d01e542adf015d6e7eaca9a08812a8f6b0ba7f24    neues-file.txt
```
Format: `<mode> <type> <object>	<name>`

Was fällt auf? Ihr seht dass der Blob für die Datei `neues-file.txt` in beiden Commits die gleiche ID hat.<br>
Warum? Weil sich dieses File nicht geändert hat. Es wird deshalb nicht nochmal gespeichert.

Mit `git ls-tree` kann man sich auch direkt die Files des Commits anzeigen lassen:
```bash
$ git ls-tree 21dd03
100644 blob d01e542adf015d6e7eaca9a08812a8f6b0ba7f24    neues-file.txt
```

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
