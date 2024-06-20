# Globale Konfiguration

## Deine Identität

Nachdem du Git installiert hast, solltest du als allererstes deinen Namen und deine E-Mail-Adresse in Git konfigurieren. Das ist insofern wichtig, da jeder Git-Commit diese Informationen verwendet und sie unveränderlich in die Commits eingearbeitet werden, die du erstellst:

```bash
$ git config --global user.name "Erika Musterfrau"
$ git config --global user.email erika@musterfrau.com
```

Wichtig: es hindert dich niemand daran hier irgeneinen x-beliebigen Namen einzugeben. Er muss auch nicht mit dem Namen übereinstimmen, der sich dann im Gitlab anmeldet.
Um die Identität wirklich nachzuweisen können die Commits mit einem GPG-Schlüssel signiert werden, dazu aber erst später.

## Konfigurationsebenen

Konfigurationen können auf unterschiedlichen Ebenen gesetzt werden.

- Global für den User: in .gitconfig im Home-Verzeichnis (Parameter `--global`)
- Pro Repository (default): im .git/config im Repository (Parameter `--local`)
- Systemweit: in etc/gitconfig der Git-Installation (Parameter `--system`)
- Worktree: kann ignoriert werden (Spezialfall)
  
## Konfigurationen ansehen

Mit folgendem Befehl sieht man welche Konfigurationen gesetzt sind und wo sie gesetzt wurden (auf welcher Ebene):

```bash
$ git config --list --show-origin
```

oder nur die Konfigurationen:

```bash
$ git config --list
```

oder ein bestimmter Wert:

```bash
$ git config user.name
```


# Hilfe zur Selbsthilfe

## Autovervollständigung

Wie bei vielen Befehlen üblich, sollte auch für git eine Autovervollständigung automatisch zur Verfügung stehen.<br>
Dazu einfach mal mit <tab><tab> probieren.

```bash
$ git <tab><tab>

Display all 70 possibilities? (y or n)
add                          clean                        gitk                         pull                         send-email
am                           clone                        grep                         push                         shortlog
apply                        commit                       gui                          range-diff                   show
archive                      config                       help                         rebase                       show-branch
askpass                      credential-helper-selector   init                         reflog                       sparse-checkout
askyesno                     credential-manager           instaweb                     remote                       stage
bisect                       describe                     lfs                          repack                       stash
blame                        diff                         log                          replace                      status
branch                       difftool                     maintenance                  request-pull                 submodule
bundle                       fetch                        merge                        reset                        switch
checkout                     flow                         mergetool                    restore                      tag
```

Die Autovervollständigung funktioniert auch innerhalb eines bestimmten Befehls.
Wenn ihr z.B. Dateien habt, die noch nicht getrackt werden, werden  euch bei "git add <tab><tab>" genau diese Dateien vorgeschlagen.

```bash
$ touch neuesfile1
$ touch neuesfile2
$ git add <tab><tab>
neuesfile1  neuesfile2
```

## Hilfe anzeigen lassen

Mit "--help" als Command-Parameter wird die entsprechende Hilfe angezeigt. "git --help" zeigt die gängisten Commands", mit "git <command> --help" wird die Hilfe für den Command angezeigt (direkt in der Shell oder eine Webseite geöffnet).
