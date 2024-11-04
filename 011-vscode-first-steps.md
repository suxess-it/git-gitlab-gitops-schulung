# VSCode starten

Es gibt verschiedene Möglichkeiten wie man VCode starten und ein Git-Repo darin öffnen kann.

## Über die git-Bash im bereits geklonten git-Repository

In der git-Bash in das entsprechende git-Verzeichnis wechseln und dort VSCode starten:

```
$ cd ~
$ cd git-schulung
$ cd first-gitlab-project
$ code . 
```

Das enstprechende git-Verzeichnis sollte im VSCode geöffnet sein.

## Über das Windows-Startmenü und bereits geklontes git-Repository öffnen

VSCode über das Startmenü starten (Suche nach "VSCode") und lokales git-Verzeichnis öffnen:

![image](https://github.com/user-attachments/assets/15f7b355-dce7-4399-88c3-6ee42a070d58)

Euer git-Verzeichnis liegt unter "C:\Benutzer\<User-ID>\git-schulung\first-gitlab-project".

## Über das Windows-Startmenü ein Remote-Repository klonen

Wie oben VSCode übers Startemnü starten und Remote-Repository klonen:

![image](https://github.com/user-attachments/assets/717619eb-5fad-4430-90f2-06879e9c8cf2)

Anschließend

- Git-URL des Remote-Repositories eingeben, z.B. "https://gitlab.aws.sopra.cloud/u004843/first-gitlab-project.git"
- und lokalen Ordner auswählen, indem dann das git-Verzeichnis erstellt wird, z.B. "C:\Users\u004843\git-schulung"

# Im VSCode zurecht finden

![image](https://github.com/user-attachments/assets/625731c2-9e1e-4c9d-bc7f-f1c7ad87b6ed)

Oben in der Mitte seht ihr ein oder zwei Tabs: "Welcome" und "Release Notes". Beide können geschlossen werden.

Wichtige Bereiche im Editor für uns:

- Editor
- Activity Bar: Hier kann zwischen unterschiedlichen Views gewechselt werden (Explorer und Source-Control ist für uns das wichtigste)

Weitere nützliche Dokumentation zu VSCode:

- https://code.visualstudio.com/docs/introvideos/basics
- https://code.visualstudio.com/docs/getstarted/userinterface

# Neue Files anlegen

Über das Context-Menü im Explorer (rechte Maustaste):

![image](https://github.com/user-attachments/assets/74b9262c-9429-42b3-933b-a91a4a099468)

Files löschen und umbenennen ebenfalls über rechte Maustaste auf das entsprechende File.

# Änderungen in einem File speichern

<CTRL+S> oder Menü "File" -> "Save"

# Die wichtigsten Git-Befehle im VSCode

## git add (Files stagen)

![image](https://github.com/user-attachments/assets/02173725-327b-4176-8674-1deaf98ff0f0)

## git commit

![image](https://github.com/user-attachments/assets/2186d94d-abce-4805-a474-2594640952ff)

man kann sich auch das vorige "stagen" sparen und direkt commiten, dann wird man gefragt ob man alle Änderungen stagen will (auch neue Files!)

## git push (Files aufs Remote-Repository pushen)

![image](https://github.com/user-attachments/assets/78ca1a82-7db5-4a4f-9fa0-4528e0dfdaa9)

## git diff

Ändert ein bestehendes File, und lasst euch dann die Änderungen so anzeigen:

Direkt im Explorer:

![image](https://github.com/user-attachments/assets/42cfd755-43de-44bd-9b78-728304826efa)

In Source-Control View:

![image](https://github.com/user-attachments/assets/da95fcd4-7275-403c-a5da-cd3505bb3876)

## Commit Historie anzeigen und darin enthaltene Änderungen:

![image](https://github.com/user-attachments/assets/a48bb046-93e0-4d85-aa66-e5878ce0ff12)

Commitet und synct jetzt nochmal die Änderungen und schaut euch die Source-Control View an.

oh shit, git! Szenarien in VSCode?

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
