# Das erste GitLab-Projekt anlegen

siehe interne Confluence-Seite

`git clone`: Klont ein Remote-Repository in ein lokales Verzeichnis


# Lokales git-Projekt mit dem Remote-GitLab-Projekt verbinden

Anstatt das Remote-Repository zu klonen, können wir auch lokal ein Git-Reposiotry initialisieren und mit dem Remote-Repository verbinden.

Dazu löschen wir jetzt wieder das davor durch `git clone` erstellte Verzeichnis und legen selbst ein neues git-Repository an.
ACHTUNG: Befehle unten genau so befolgen, nicht dass ihr versehentlich ein anderes Verzeichnis mit `rm -rf` löscht!
```
$ cd ~

$ pwd
/c/Users/u004843

$ cd git-schulung

$ rm -rf first-gitlab-project
$ mkdir first-gitlab-project

$ cd first-gitlab-project

$ ls
```

Remote-Repository als `origin` vom lokalen Repository angeben (u004843 entsprechend anpassen):
```
$ git remote add origin https://gitlab.aws.sopra.cloud/u004843/first-gitlab-project.git
fatal: not a git repository (or any of the parent directories): .git
```

Wie man sieht, schlägt dieser Befehl fehl, weil wir lokal noch kein Git-Repository initialisiert haben. Was fehlt noch?

Git-Repository initialisieren, dann kann man das Remote-Repository als `origin` vom lokalen Repository angeben:
```
$ git init
Initialized empty Git repository in C:/Users/u004843/git-schulung/first-gitlab-project/.git/
```

Jetzt nochmal Remote-Repository als `origin` vom lokalen Repository angeben (u004843 entsprechend anpassen):
```
$ git remote add origin https://gitlab.aws.sopra.cloud/u004843/first-gitlab-project.git
```
Jedes Remote-Repository hat einen sogenannten Alias, in diesem Fall `origin`. Man könnte ihn aber genauso `Hubert` nennen.
Außerdem kann man auch mehrere Remote-Repositories angeben.

Mit welchen Remote-Repositories das git-Repo verknüpft ist, sieht man mit `git remote -v`:
```
$ git remote -v
origin  https://gitlab.aws.sopra.cloud/u004843/first-gitlab-project.git (fetch)
origin  https://gitlab.aws.sopra.cloud/u004843/first-gitlab-project.git (push)
```

Mit `git push` kann man den aktuellen Stand vom lokalen git-Repo auf das Remote-Repository schieben:
```
$ git push --set-upstream origin main
error: src refspec main does not match any
error: failed to push some refs to 'https://gitlab.aws.sopra.cloud/u004843/first-gitlab-project.git'
```

Was fehlt jetzt noch?

Ohne Commits im lokalen Repository kann man nichts pushen. 
```
$ touch README.md

$ git add README.md

$ git commit -m "initial commit"

$ git log
commit d545fe06f90bf00bb873b87673df18e1b2b7290d (HEAD -> main)
Author: Johannes Kleinlercher <johannes.kleinlercher@suxess-it.com>
Date:   Thu Jul 25 11:06:38 2024 +0200

    initial commit
```

Jetzt können wir `git push` nochmal ausprobieren:

```
$ git push --set-upstream origin main
```

Funktioniert leider wieder nicht. Warum? Weil sich im Remote-Repository bereits Commits befinden die man so überschreiben würde.

Lösung: wenn man, wie wir jetzt in diesem Fall, die Commits im Remote-Repository wirklich überschreiben will,
muss man den Parameter `--force` oder kurz `-f` ergänzen:

```
$ git push --set-upstream -f origin main
```

Leider geht das aber wieder nicht :(

```
git push --set-upstream -f origin main
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 232 bytes | 232.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
remote: GitLab: You are not allowed to force push code to a protected branch on this project.
To https://gitlab.aws.sopra.cloud/u004843/first-gitlab-project.git
 ! [remote rejected] main -> main (pre-receive hook declined)
error: failed to push some refs to 'https://gitlab.aws.sopra.cloud/u004843/first-gitlab-project.git'
```

Standardmäßig ist in Eurem Gitlab der main-Branch protected, d.h. man darf auf den main-Branch nichts direkt pushen.


# Git-Projekt im VSCode weiter bearbeiten

TODO:

- VSCode starten
- im VSCode zurecht finden
- Neues File im VSCode erstellen
- Wie macht man im VSCCode "git diff", "git add" "git commit", "git restore --staged", "git checkout"
- Welche neuen Commands kommen mit einem Remote-Repository dazu?
    - git push
    - git clone
    - git fetch

# Git-Projekt im GitLab bearbeiten

TODO:

- Wo sieht man die gepushten Commits (Source Control View, Source Control Graph links unten)
- GitLab Plugins? (checken welche defaultmäßig installiert sind, und welche man braucht)
- Feature-Branches
- Erstellen von Merge-Requests

# Wichtige Git-Projekt Einstellungen im GitLab

TODO:

- protected branches
- Merge Request Einstellungen
