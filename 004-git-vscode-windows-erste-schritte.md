# Erstes Git-Repo erstellen


Falls das Verzeichnis "projekt1" im git-schulung Ordner noch existiert, löschen wir es nochmal gleich, damit wir es nochmal anlegen können :)

```bash
$ cd ~
$ pwd
/c/Users/johannes
$ cd git-schulung
$ rm -r projekt1/
```

Und wieder anlegen in der git-bash:

```bash
$ cd ~

$ pwd
/c/Users/johannes

$ mkdir git-schulung

$ cd git-schulung/

$ mkdir projekt1

$ cd projekt1/

$ git init
Initialized empty Git repository in C:/Users/johannes/git-schulung/projekt1/.git/

$ code .
```

Jetzt sollte VSCode starten.

Wir werden zu Beginn VSCode nur verwenden, um Dateien zu erstellen und zu schreiben. Die git-Befehle führen wir in der Command-Line aus, um git und seine Befehle besser kennenzulernen.

Mit "code ." im Repository-Verzeichnis in der git-bash oder git-cmd VSCode starten.

Für alle, denen VSCode noch nicht vertraut ist, werden hier nochmal detaillierte erste Schritte erklärt.

# Files in VSCode anlegen

Wie erstellt man Files im VSCode:

![image](https://github.com/suxess-it/git-gitlab-gitops-schulung/assets/11465610/19ca6893-eac6-4ca6-81d7-554a815a9875)

Filenamen eingeben:

![image](https://github.com/suxess-it/git-gitlab-gitops-schulung/assets/11465610/92f0eac9-e2bd-4384-a697-bd6680769404)

Und dann rechts einen Text im File schreiben und mit Ctrl+S speichern (File → Save).

# git-bash als Terminal anzeigen

Anschließend öffnen wir das Terminal innerhalb von VSCode:

![image](https://github.com/suxess-it/git-gitlab-gitops-schulung/assets/11465610/b378f5c2-a47a-4564-88fe-da533dc5734b)

und wechseln auf die "git bash":

![image](https://github.com/suxess-it/git-gitlab-gitops-schulung/assets/11465610/8decb013-6b39-401a-aa74-2ba7c01b655d)

# Erster git-Commit 

Dann führen wir das erste Mal "git status" aus:

```bash
$ git status
```

![image](https://github.com/suxess-it/git-gitlab-gitops-schulung/assets/11465610/a55caf16-23ea-4283-a910-3aef16bdabe8)

Wir fügen mit "git add" das neu erstellte File dem Repository hinzu (wir "stagen" das File), und werden anschließend diesen Stand "commitieren".

```bash
$ git add dasisteinfile.txt
$ git commit
```

Jetzt startet sich ein Editor ("vi") wo man 

- mit "i" in den INSERT-Mode wechseln muss
- seine Commit-Message eingeben muss
- dann mit [ESC] in den Command-Modus gehen muss
- und dann mit ":x" und [ENTER] den Editor beenden:

![image](https://github.com/suxess-it/git-gitlab-gitops-schulung/assets/11465610/29f76202-64f9-477d-b9cb-ebff5a16357c)

Weil das relativ mühsam ist so, werden wir in Zukunft bei jedem "git commit" auch gleich die Commit-Message mitangeben:

```bash
$ git commit -m "dieses file ist enorm wichtig!"
```

Jetzt kann man wieder "git status" eingeben um den Zustand des Repositories zu sehen:

```bash
$ git status

On branch main
nothing to commit, working tree clean
```

Bravo! Der erste Commit ist geschafft! Lasst uns jetzt mal schauen was wir gemacht haben.
