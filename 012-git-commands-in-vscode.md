# Die wichtigsten Git-Befehle im VSCode

Hier schauen wir uns nochmal genauer an was im VSCode der entsprechende Ersatz für die git-Befehle in der git-Bash sind.
Wenn ihr wollt könnte ihr im VSCode dazu auch ein Terminal öffnen und die früher erlernten Befehle parallale dazu aufrufen (Menüpunkt "Terminal" -> "New Terminal"):

![image](https://github.com/user-attachments/assets/d5acd4c1-8a06-45e5-8566-be3dc9c8f35a)

Es spricht auch absolut nichts dagegen weiterhin im Terminal die Command-Line-Befehle zu verwenden, anstatt im VSCode zu klicken.


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

Mehrzeilige Commits: einfach mit Enter neue Zeile hinzufügen. Nur `STRG+ENTER` führt den Commit aus (bzw. der Button "Commit")

## git diff

Ändert ein bestehendes File, und lasst euch dann die Änderungen so anzeigen:

Direkt im Explorer:

![image](https://github.com/user-attachments/assets/42cfd755-43de-44bd-9b78-728304826efa)

In Source-Control View auf das jeweilige File klicken:

![image](https://github.com/user-attachments/assets/da95fcd4-7275-403c-a5da-cd3505bb3876)

oder für alle Änderungen in allen Files auf "View Changes":

![image](https://github.com/user-attachments/assets/ea50bb52-e4cf-4bc2-8664-7a5ac6c62035)


## Commit Historie anzeigen und darin enthaltene Änderungen

![image](https://github.com/user-attachments/assets/543e429e-ace7-4ebc-a5a9-757b9e96af03)

## Einen bestimmten Commit auschecken

![image](https://github.com/user-attachments/assets/4d03c187-edba-4c75-a777-1d79d6ea74ba)

und wieder zurück auf den main-Branch:

![image](https://github.com/user-attachments/assets/588c4343-c6d7-4c1b-a8cf-d81ebe98c1e5)

## Änderungen im Working-Directory rückgängig machen

Änderungen in einem File rückgängig machen, d.h. den Stand auf den letzten Commit zurücksetzen, macht man über den Button "Discard Changes":

![image](https://github.com/user-attachments/assets/26deb930-6f2b-4bfa-8a3d-46689e5dd424)

## Letzte Commit-Message korrigieren

Analog zu `git commit --amend -m "neue commit message` in der Command-Line:

![image](https://github.com/user-attachments/assets/5556f665-f3a4-4ad7-8668-2aedfeebab8d)

## Zusätzliche Änderungen beim letzten Commit ergänzen

Änderungen beim letzten Commit noch ergänzen kann man, indem die neue Änderung gestaged wird und dann "Commit (Amend)" ausgewählt wird.

![image](https://github.com/user-attachments/assets/a5d74f9f-4486-4b6d-97c1-38407812573e)

ACHTUNG: nur lokale Commits ergänzen, die noch nicht ins Remote-Repo gepusht wurden, weil man die Commit-History verändert!

## Letzten Commit rückgängig machen

mit `<STRG> + <SHIFT> + P` die Command-Palette starten und dann `Git: Undo Last Commit` auswählen (bzw. schreiben)

## Command-Palette in VSCode aufrufen

mit `<STRG> + <SHIFT> + P`

und dann beginnen "Git:" zu schreiben zeigt alle Git-Befehle an.
