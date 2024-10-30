# Das erste GitLab-Projekt anlegen

TODO

# Lokales git-Projekt mit dem Remote-GitLab-Projekt verbinden

Wir erstellen ein neues lokales Verzeichnis und versuchen wie in der README.md unseres GitLab-Projektes die ersten Schritte durchzuführen.

Projektverzeichnis anlegen:
```
$ cd ~

$ pwd
/c/Users/u004843

$ cd git-schulung

$ mkdir first-gitlab-project

$ cd first-gitlab-project
```

Remote-Repository als `origin` vom lokalen Repository angeben:
```
$ git remote add origin https://gitlab.aws.sopra.cloud/u004843/first-gitlab-project.git
fatal: not a git repository (or any of the parent directories): .git
```

Wie man sieht, schlägt dieser Befehl fehl, weil wir lokal noch kein Git-Repository initialisiert haben. Was fehlt noch?

Git-Repository initialisieren, dann kann man das Remote-Repository als `origin` vom lokalen Repository angeben:
```
$ git init
Initialized empty Git repository in C:/Users/u004843/git-schulung/first-gitlab-project/.git/

$ git remote add origin https://gitlab.aws.sopra.cloud/u004843/first-gitlab-project.git

$ git remote -v
origin  https://gitlab.aws.sopra.cloud/u004843/first-gitlab-project.git (fetch)
origin  https://gitlab.aws.sopra.cloud/u004843/first-gitlab-project.git (push)
git branch -M main

$ git push -uf origin main
error: src refspec main does not match any
error: failed to push some refs to 'https://gitlab.aws.sopra.cloud/u004843/first-gitlab-project.git'
```

Was fehlt jetzt noch? 

Ohne Commits im lokalen Repository kann man nichts pushen. 

```
$ touch README.md

$ git add -A

$ git commit -m "initial commit"

$ git log
commit d545fe06f90bf00bb873b87673df18e1b2b7290d (HEAD -> main)
Author: Johannes Kleinlercher <johannes.kleinlercher@suxess-it.com>
Date:   Thu Jul 25 11:06:38 2024 +0200

    initial commit

$ git push -uf origin main
```

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
