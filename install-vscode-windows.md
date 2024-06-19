# VSCode unter Windows installieren

https://code.visualstudio.com/docs/setup/windows aufrufen

"Visual Studio Code installer" Link klicken, sollte File wie "VSCodeUserSetup-x64-1.90.1.exe" herunterladen (Version kann aktueller sein).

![image](https://github.com/suxess-it/git-gitlab-gitops-schulung/assets/11465610/f12728dc-c364-4ae5-ad95-e056de8b82d7)


Installations-Exe starten (installiert VSCode im User-Mode, benötigt also keine Admin-Rechte)

Anschließend "git-cmd.exe" oder "git-bash.exe" neu öffnen und einfach "code" in die Befehlszeile schreiben und schauen ob VSCode startet.

Falls sich VSCode nicht öffnen, dann vlt PC durchstarten damit VSCode im Pfad ist

# VSCode in git-bash oder git-cmd starten

Um sicherzustellen dass die Tools funktionieren bitte mal testweise folgende Befehle aufrufen.

In der git-bash (werde ich in der Schulung verwenden):

```
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


Mit git CMD (Befehle sollten identisch sein):
```
C:\Users\johannes>mkdir git-schulung

C:\Users\johannes>cd git-schulung

C:\Users\johannes\git-schulung>mkdir projekt1

C:\Users\johannes\git-schulung>cd projekt1

C:\Users\johannes\git-schulung\projekt1>git init
Initialized empty Git repository in C:/Users/u004843/git-schulung/projekt1/.git/

C:\Users\johannes\git-schulung\projekt1>code .

C:\Users\johannes\git-schulung\projekt1>
```
Jetzt sollte VSCode starten.
