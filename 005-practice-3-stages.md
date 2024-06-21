# Die 3 Stages in einem Git-Repository

Wie zuvor erfahren gibt es folgende 3 Stages:

- Working-Directory
- Staging-Area
- lokales Git-Repository

Lasst uns jetzt üben wie unsere Files durch die einzelnen Stages wandern.

# Initialer Stand

Dafür schauen wir uns zuerst den aktuellen Stand an:

Working-Directory:
```bash
$ ls
dasisteinfile.txt
```

Staging-Area:
```bash
$ git ls-files -s
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0       dasisteinfile.txt
```

Git-Repository:
```bash
$ git ls-tree -r main
100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391    dasisteinfile.txt
```

# Neues File in Working-Directory anlegen

entweder über VSCode oder direkt in der Commandline:
```bash
$ echo "hallo ich bin da" > neues-file.txt
```

Auflisten der Files im Working-Directories:
```bash
$ ls
dasisteinfile.txt  neues-file.txt
```

In Staging-Area:
```bash
$ git ls-files -s
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0       dasisteinfile.txt
```

In Git-Repository:
```bash
$ git ls-tree -r main
100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391    dasisteinfile.txt
```
Weder in Staging-Area noch im Git-Repository ist das neues-file.txt vorhanden.

`git status` zeigt an, dass ein File "untracked" ist:

```bash
$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        neues-file.txt

nothing added to commit but untracked files present (use "git add" to track)
```

# File in Staging-Area hinzufügen

Jetzt machen wir genau das, was uns `git status` vorschlägt, wie fügen mit `git add` das neue File in die Staging-Area hinzu.

```bash
$ git add neues-file.txt
warning: in the working copy of 'neues-file.txt', LF will be replaced by CRLF the next time Git touches it
```
Warning kann ignoriert werden.

Status in Staging-Area und Repository. neues-file.txt in Staging-Area, aber noch nicht in Repository:
```bash
$ git ls-files -s
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0       dasisteinfile.txt
100644 29c1016321ac936c486d845bb52c0084b8626717 0       neues-file.txt

$ git ls-tree -r main
100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391    dasisteinfile.txt
```

`git status` zeigt an, dass sich ein File in der Staging-Area befindet das man committen könnte.<br>
Außerdem wird ausgegeben, wie man das File wieder von der Staging-Area entfernt (unstaged).

```bash
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   neues-file.txt
```

Unstagen und Added können wir jetzt nochmal üben:

```bash
$ git restore --staged neues-file.txt
```
gern auch selbständig dazwischen mit `git status` und `git ls-files -s` den aktuellen Zustand der Staging-Area kontrollieren
```bash
$ git add neues-file.txt
```

# File commiten

Jetzt wollen wir das File endlich commitieren.

```bash
$ git commit -m "Jetzt aber ab ins Git-Repo mit dir!"
[main d0adc99] Jetzt aber ab ins Git-Repo mit dir!
 1 file changed, 1 insertion(+)
 create mode 100644 neues-file.txt
```

Und jetzt nochmal alle Stages vergleichen:

Working-Directory:
```bash
$ ls
dasisteinfile.txt  neues-file.txt
```

Staging-Area:
```bash
$ git ls-files -s
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0       dasisteinfile.txt
100644 29c1016321ac936c486d845bb52c0084b8626717 0       neues-file.txt
```

Git-Repository:
```bash
$ git ls-tree -r main
100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391    dasisteinfile.txt
100644 blob 29c1016321ac936c486d845bb52c0084b8626717    neues-file.txt
```

# Commit-Historie ausgeben lassen

Jetzt gibt es zwei Commits im Git-Repository. So werden sie chronologisch (neuester ganz oben) angezeigt:

```bash
$ git log
$ git log
commit d0adc9941b14d0c9b8f6b5f5fbdc25b57850d26b (HEAD -> main)
Author: Johannes Kleinlercher <johannes.kleinlercher@suxess-it.com>
Date:   Thu Jun 20 15:55:54 2024 +0200

    Jetzt aber ab ins Git-Repo mit dir!

commit decece91d0e30c918b723cc9984597aa9d75d0ff
Author: Johannes Kleinlercher <johannes.kleinlercher@suxess-it.com>
Date:   Thu Jun 20 15:04:40 2024 +0200

    das ist mein erstes file
```

# Bereits getracktes File ändern

Jetzt wissen wir wie man neue Files erstellen, der Staging-Area hinzufügen und im Git-Repo commitieren kann.<br>
Bereits vorhandene (getrackte) Files verändern geht genau gleich. Auch sie müssen zuerst mit `git add` in die Staging-Area gebracht werden und können dann mit `git commit -m <message>` commitiert werden.

Du kannst ganz einfach ein bestehendes File ändern indem du so in der Bash einen Inhalt ergänzt:

```bash
$ echo "das ist noch ein test" >> neues-file.txt
```

Die nächsten Befehle um das File bis in das Git-Repository zu bringen, darfst du jetzt selbst herausfinden.


# Bereits getrackte Files löschen

Um Files im Git-Repository zu löschen, kann man mit folgendem Befehl das File gleichzeitig aus dem Working-Directory und der Staging-Area löschen:

```bash
$ git rm dasisteinfile.txt
rm 'dasisteinfile.txt'
```

Dann zeigt `git status` bereits an, dass man diese Änderungen committen kann.

```bash
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    dasisteinfile.txt
```

Alternative:
Man kann das File aber auch zuerst im Working-Directory löschen (mit normalen `rm` Befehl) 
und erst wenn man sich sicher ist, dass man das File wirklich löschen will, mit `git rm <file>` auch aus der Staging-Area löschen.


Auch im Working-Directory und in der Staging-Area ist das File nicht mehr vorhanden:

Working-Directory:
```bash
$ ls
neues-file.txt
```

Staging-Area:
```bash
$ git ls-files -s
100644 d01e542adf015d6e7eaca9a08812a8f6b0ba7f24 0       neues-file.txt
```

Im Git-Repository allerdings schon:
```bash
$ git ls-tree -r 5f30ae453b691182
100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391    dasisteinfile.txt
100644 blob d01e542adf015d6e7eaca9a08812a8f6b0ba7f24    neues-file.txt
```

Jetzt kann die Änderung committiert werden, damit das File auch im Git-Repository verschwinden.

```bash
$ git commit -m "das file gefällt mir nicht mehr"
[main 21dd03d] das file gefällt mir nicht mehr
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 dasisteinfile.txt
```

Kontrolle:
```bash
$ git ls-tree -r main
100644 blob d01e542adf015d6e7eaca9a08812a8f6b0ba7f24    neues-file.txt
```

Natürlich ist das File nur im aktuellsten Commit verschwunden. In den früheren Commits ist es natürlich noch vorhanden.
