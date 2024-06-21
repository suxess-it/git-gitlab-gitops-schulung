# Branches erstellen

Branches dienen also dazu von einem bestimmten Entwicklungszweig (meistens dem Haupt-Branch) wieder abzuzweigen.
Einen Branch kann man auf zwei unterschiedliche Arten erstellen.

Mit `git checkout -b <neuer-branch>` wird ein neuer Branch erstellt und gleich in diesen gewechselt:

```bash
$ git checkout -b feat/mfa
Switched to a new branch 'feat/mfa'
```

Mit `git branch <neuer-branch>` wird nur ein neuer Branch erstellt, aber noch nicht in diesen Branch gewechselt.<br>
Zum Wechseln muss man `git switch <branch>` ausführen.

```bash
$ git branch feat/mfa

$ git switch feat/mfa
Switched to branch 'feat/mfa'
```

# Branches löschen

```bash
$ git branch -d feat/mfa
Deleted branch feat/mfa (was ae3e653).
```



