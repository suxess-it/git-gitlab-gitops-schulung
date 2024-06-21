# Git-Ignore File erstellen

Wie wir schon erfahren haben sollte man einige Files nicht in einem Git-Repository speichern.
Um das automatisch zu verhindern, empfiehlt es sich eine .gitignore File zu erstellen

Im Internet gibt es unzähle typische [gitignore-Files](https://github.com/github/gitignore).
Meistens hängt es von der Art des Projekts ab, welches gitignore-File passend ist.

Wie legen als Beispiel ein .gitignore File an, das alle Files mit der Endung ".tar.gz" ignoriert.

```bash
$ echo "*.tar.gz" > .gitignore
$ touch bla.tar.gz

$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        ../.gitignore

nothing added to commit but untracked files present (use "git add" to track)
```

Hier sieht man, dass zwar das .gitignore File selbst als neues File erkannt wird,
das bla.tar.gz wird aber bereits ignoriert.

Man kann unterschiedlichste Pattern angeben, am besten im [offiziellen Handbuch](https://git-scm.com/docs/gitignore) nachlesen.

# Mehrere Files gleichzeitig der Staging-Area hinzufügen

Wir kennen ja schon den Befehl `git add <file>` um einzelne Files in die Staging-Area (= Index) zu befördern.
Man kann auch gleichzeitig alle oder mehrere Files angeben.

Alle neuen Files gleichzeitig "stagen":
```bash
$ touch blub ; touch ok ; mkdir bla ; touch bla/test
$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        bla/
        blub
        ok

nothing added to commit but untracked files present (use "git add" to track)

AzureAD+JohannesKleinlercher@HP860G9-JOHNNY MINGW64 ~/git-schulung/projekt1 (main)

$ git add -A

AzureAD+JohannesKleinlercher@HP860G9-JOHNNY MINGW64 ~/git-schulung/projekt1 (main)
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   bla/test
        new file:   blub
        new file:   ok
```

Man kann aber auch mehrere Files hintereinander angeben oder mit "*" arbeiten, z.B. `git add test1.txt test2.txt` oder `git add *.txt` .

# Alle bereits getrackten Files sofort committen

Wenn man nur bereits getrackte Files verändert hat und diese sofort committen will,
kann man auch den Zwischenschritt mit der Staging-Area implizit durchführen.

```bash
$ echo "noch eine änderung" >> neues-file.txt
$ git status
$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   neues-file.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Bevor man jetzt `git add neues-file.txt` ausführt und dann `commit -a -m <message>` geht das in einem:

```bash
$ git commit -a -m "the stage is yours"
warning: in the working copy of 'neues-file.txt', LF will be replaced by CRLF the next time Git touches it
[main 22e7ead] the stage is yours
 1 file changed, 1 insertion(+)
```

# Mehrzeilige Commit-Messages

Best-Practices sagen, man soll in der ersten Zeile einer Commit-Message eine kurze Zusammenfassung schreiben, WAS man gemacht hat
und nach einer Leerzeile dann noch Details und WARUM die Änderung erfolgt.
Mehrzeilige Commit-Messages können in der git-bash so erstellt werden. Nach dem `-m` mit einem Anführungszeichen den Text beginnen und dann mit ENTER Leerzeichen anfangen. 
Erst mit einem abschließenden Anführungszeichen wird die Commit-Messages beendet.

```bash
$ touch file42
$ git add file42
$ git commit -a -m "JIRA-345: Zwei-Faktor-Auth implementiert
>
> Wegen Compliance-Richtlinien wurde die Software um Zwei-Faktor-Auth erweitert."
[main 7cb263b] JIRA-345: Zwei-Faktor-Auth implementiert
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file42
```

Mehrzeilige Commits haben den Vorteil dass im Oneline-Commmit-Log nur die erste Zeile ausgegeben wird:

```bash
$ git log --oneline
7cb263b (HEAD -> main) JIRA-345: Zwei-Faktor-Auth implementiert
22e7ead the stage is yours
0f3d2dd Ich habe Bug xy gefixed.
```


