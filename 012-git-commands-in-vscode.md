# Die wichtigsten Git-Befehle im VSCode

Hier schauen wir uns nochmal genauer an was im VSCode der entsprechende Ersatz für die git-Befehle in der git-Bash sind.
Wenn ihr wollt könnte ihr im VSCode dazu auch ein Terminal öffnen und die früher erlernten Befehle parallale dazu aufrufen (Menüpunkt "Terminal" -> "New Terminal"):

![image](https://github.com/user-attachments/assets/d5acd4c1-8a06-45e5-8566-be3dc9c8f35a)


## git status

`git status` zeigt "modified" und "untracked" Files an. Im VSCode sieht man das direkt im Explorer:

![image](https://github.com/user-attachments/assets/92105327-2499-47ef-83b2-b7b96bf4e82a)

bzw. in der "Source-Control"-View:

![image](https://github.com/user-attachments/assets/b89da7e9-0584-4a5c-b2d0-62ee5c78314f)


## git add (Files stagen)

`git add` fügt Files in die Staging-Area hinzu:

![image](https://github.com/user-attachments/assets/02173725-327b-4176-8674-1deaf98ff0f0)

Frage: sieht schon jemand wie man die Files wieder aus der Staging-Area entfernt? (`git restore --staged <file>`)

Versucht auch mal Files zu löschen. Wie wird das im Explorer bzw. der Source-Control-View dargestellt?

## git commit

![image](https://github.com/user-attachments/assets/2186d94d-abce-4805-a474-2594640952ff)

man kann sich auch das vorige "stagen" sparen und direkt commiten, dann wird man gefragt ob man alle Änderungen stagen will (auch neue Files!)

## git diff

Ändert ein bestehendes File, und lasst euch dann die Änderungen so anzeigen:

Direkt im Explorer:

![image](https://github.com/user-attachments/assets/42cfd755-43de-44bd-9b78-728304826efa)

In Source-Control View:

![image](https://github.com/user-attachments/assets/da95fcd4-7275-403c-a5da-cd3505bb3876)

## Commit Historie anzeigen und darin enthaltene Änderungen

![image](https://github.com/user-attachments/assets/a48bb046-93e0-4d85-aa66-e5878ce0ff12)


## git push (Files aufs Remote-Repository pushen)

![image](https://github.com/user-attachments/assets/78ca1a82-7db5-4a4f-9fa0-4528e0dfdaa9)

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
