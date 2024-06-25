# Oh Shit, Git?! - Wie korrigiere ich Änderungen?

## File versehentlich schon in der Staging-Area, nochmal raus damit!

Wenn man ein File versehentlich in die Staging-Area geschoben hat, das man aber gar nicht committen will. Kann man es mit `git restore --staged <file>` wieder unstagen.
Dieser Befehl wird auch in `git status` schön angezeigt.

```bash
$ touch vielleicht
$ git add vielleicht
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   vielleicht
$ git restore --staged vielleicht
$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        vielleicht
```

## Ich hab Änderungen in einem File im Working-Directory gemacht, die will ich rückgängig machen

Der Befehl `git status` zeigt gottseidank schon den Befehl an, den man dafür benötigt:

```bash
$ echo "ein bloedsinn" >> neues-file.txt
$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   neues-file.txt
$ git restore neues-file.txt
$ git status
On branch main
nothing to commit, working tree clean
```

Damit ist der Stand des Files wieder vom aktuellen Commit.

## Ein File im Working-Directory auf den Stand von einem früheren Commit bringen

Um da File `neues-file.txt` auf den Stand von der Commit-ID `4fd6d3456`zu bringen:

```bash
$ git restore --source=4fd6d3456 neues-file.txt
```

Das File ist somit verändert worden und muss wieder neu committed werden:

```bash
 git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   file3
```


## Noch Kleinigkeiten beim letzten Commit ergänzen (amend .. abändern)

Man hat gerade committiert und kommt drauf dass man entweder
ein File vergessen hat zu "stagen", ein kleiner Typo den man noch korrigieren möchte o.ä.
Dann kann man nach den "fehlerhaften" Commit nochmal wiefolgt korrigieren.

```bash
$ echo "das ist falsc" > neues-file.txt

$ git diff
warning: in the working copy of 'neues-file.txt', LF will be replaced by CRLF the next time Git touches it
diff --git a/neues-file.txt b/neues-file.txt
index df7df0c..dc18990 100644
--- a/neues-file.txt
+++ b/neues-file.txt
@@ -1,2 +1 @@
-hallo ich bin da
-noch eine änderung
+das ist falsc

$ git commit -a -m "das schaut ja gut ausss"
```

Ich komm erst jetzt drauf dass bei "falsc" noch das "h" fehlt ...:

```bash
$ echo "das ist falsch" > neues-file.txt

$ git diff
warning: in the working copy of 'neues-file.txt', LF will be replaced by CRLF the next time Git touches it
diff --git a/neues-file.txt b/neues-file.txt
index dc18990..c2d1ca7 100644
--- a/neues-file.txt
+++ b/neues-file.txt
@@ -1 +1 @@
-das ist falsc
+das ist falsch

$ git commit -a --amend --no-edit
```

## Die letzte Commit-Message austauschen mit "amend"

Jetzt erst sehe ich dass ja die Commit-Message auch noch fehlerhaft ist (wohl nicht so mein Tag),
also nochmal:

```bash
$ git commit --amend -m "das schaut ja gut aus"
```

Files wurden jetzt keine geändert, sondern nur die Commit-Message.

## Den letzten Commit rückgängig machen, aber die Änderungen im Working-Directory behalten

Der letzte Commit war ein kompletter Topfen - ich will ihn so nicht mehr in der Commit-History haben.
Aber die Änderungen sollen im Working-Directory noch bestehen bleiben, vielleicht will ich an den Files noch weiterarbeiten.

```bash
$ git reset main~
Unstaged changes after reset:
M       neues-file.txt

$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   neues-file.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git log
commit 7cb263b91b6b0a1285f34bb8fd2088b4cc812cc9 (HEAD -> main)
Author: Johannes Kleinlercher <johannes.kleinlercher@suxess-it.com>
Date:   Fri Jun 21 16:37:55 2024 +0200

    JIRA-345: Zwei-Faktor-Auth implementiert

    Wegen Compliance-Richtlinien wurde die Software um Zwei-Faktor-Auth erweitert.
```

Man sieht im Git-Log ist der letzte Commit verschwunden, aber lt. `git status` sind die Änderungen noch im Working-Directory.

Das `<rev>~<n>` steht für gehe n-Schritte ab dem Referenznamen zurück. Ohne Nummer entspricht dem `~1`. In unserem Fall war die Referenz `main`, der Name unseres Branches.

Preisfrage: sind die Änderungen noch in der Staging-Area?



Wenn man 3 Commits zurückgehen will, dann kann man folgendes aufrufen:

```bash
$ git reset main~3
```

## Den letzten Commit rückgängig machen und die Änderungen auch im Working-Directory entfernen

Wenn man die Änderungen durch den letzten Commit sowohl im Git-Repository als auch im Working-Directory rückgängig machen will,
muss man die Option `--hard` ergänzen.

```bash
$ git reset main~4 --hard
HEAD is now at 90c4128 ich möchte nochmal commits erklären
```

Wichtig: `HEAD` ist auch eine Referenz und zeigt auch auf `main`

Das ist euch vlt beim `git log` bereits aufgefallen:

```bash
$ git log
commit 90c41286e4687cb13d0c3e36584f958f90a638d4 (HEAD -> main)
```

## Einen früheren Commit rückgängig machen, aber nachvollziehbar in der Commit-Historie

Mit folgendem Befehl kann man einen bestimmten Commit (muss nicht der letzte sein!) rückgängig machen,
indem einfach in einem neuen Commit die "Rückgängig-Änderungen" durchgeführt werden.

```bash
$ git revert 0e3d42a2 --no-edit
```

Wichtig: hier wird kein alter Commit gelöscht, sondern ein neuer Commit erstellt, der die Änderungen rückgängig macht. Die Korrektur ist also in der Commit-History nachvollziehbar.
Achtung: das ganze wird kompliziert wenn man einen Commit reverted der Files anlegt, die in einem späteren Commit geändert werden. (Wenn wir Zeit haben können wir das in einem neuen Git-Repo kurz ausprobieren).

## Einen früheren Commit rückgängig machen, aber in der Commit-Historie verschwinden lassen

Mit `git rebase <ref>~<n> -i` für interaktiv, kann ich mir die letzten <n> Commits anzeigen lassen und die Commits löschen oder auch umsortieren.
Ziemlicher git-Kungfu - aber wer weiß was er tut, soll ruhig machen ...

Zuerst Git-Log, um die Frage unten beantworten zu können:
```bash
$ git log
```

Und jetzt gehts mit dem Kungfu lost:
```bash
$ git rebase main~5 -i
```

Hat jemand eine Idee was mit den Commits nach dem gelöschten Commit passiert?
