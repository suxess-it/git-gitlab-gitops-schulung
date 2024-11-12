# Gemeinsam an Git-Projekten arbeiten

Gewöhnlich arbeitet man an Git-Projekten gemeinsam mit mehreren Leuten. Damit jeder für sich effizient arbeiten kann und gleichzeitig ein funktionierender gemeinsamer Software-Stand entwickelt wird, bedarf es einem im Team (oder in der gesamten Organisation) standardisierten Workflows, an den sich jeder hält.

Wir lernen hier einen vereinfachten [GitLab-Flow](https://about.gitlab.com/topics/version-control/what-is-gitlab-flow/) kennen.

Wichtigste Eigenschaften dieses Workflows:

* der main-Branch beinhaltet den aktuellen produktiven Stand
* neue Features / Fixes werden in kurzlebigen Feature-Branches entwickelt und anschließend in den main-Branch über Merge-Requests gemerged
* es wird nichts direkt in den main-Branch commitiert, sondern immer über Feature-Branches

Dieser Workflow entspricht also 1:1 den bisher bekannten Methoden in diesem Skriptum.

## In VSCode das Git-Projekt lokal öffnen

Das in der Präsentation angegebene GitLab-Projekt soll lokal im VSCode geöffnet werden. Mittlerweile kennen wir zwei Varianten wie das möglich ist.

Variante 1: In der git-Bash das Repository klonen und dann den Folder im VSCode öffnen

```
git clone <git-repo>
cd <git-repo-verzeichnis>
```

Variante 2: Direkt im VSCode das Repository klonen

siehe [First Steps](011-vscode-first-steps.md#%C3%BCber-das-windows-startmen%C3%BC-und-bereits-geklontes-git-repository-%C3%B6ffnen)

## main-Branch aktualisieren

Darauf achten dass der main-Branch ausgecheckt ist und mit dem aktuellen Stand vom `origin/main` hat. Wie macht man das?

```
git checkout main
git pull
```

## Im Git-Projekt weiterentwickeln

Aufgabe: Jeder Schulungsteilnehmer erstellt in seinem Feauture-Branch ein neues File mit dem Namen "<Vorname>_<Nachname>.txt" und ergänzt im README.md in der Mitglieder-Liste deinen Namen.

Wie im Gitlab-Flow definiert, werden Änderungen immer über einen Feature-Branch gemacht. 
Deshalb muss jetzt vom main-Branch aus ein neuer Feature-Branch abgezweigt werden.

Im Terminal mit `git checkout -b feat/add-<vorname>` oder [in VSCode GUI](013-vscode-branches.md#branches-erstellen-und-auf-gitlab-pushen).

Dann die Änderungen wie in der Aufgabenbeschreibung durchführen und commitieren.

```
git add .
git commit -a -m "feat: add <vorname>"
git push
```

oder [in VSCode commitieren](012-git-commands-in-vscode.md#git-add-files-stagen) und [auf das Remote-Repository pushen](013-vscode-branches.md#und-auf-gitlab-pushen).

Welcher Hinweis kommt nach dem `git push`? Git weiß noch nicht wohin dieser Branch gepusht werden soll, deshalb ist einmalig

```
git push --set-upstream origin feat/add-<vorname>
```

notwendig. D.h. jeder Branch in einem lokalen Git-Repo könnte rein theoretisch mit unterschiedliche Remote-Repositories verbunden sein!

Seht ihr jetzt den Hinweis, wie ihr den Merge-Request erstellen könnt?


## Merge-Request erstellen

Mit dem vorherigen `git push` Befehl wurde vermutlich bereits ein Link ausgegeben wie man einen Merge-Request erstellen kann. Entweder kann dieser geklickt werden oder im GitLab der [Merge-Request erstellt werden](013-vscode-branches.md#merge-request-in-gitlab-erstellen)

## Merge-Requests sind Team-Arbeit

Merge-Requests können dazu verwendet werden über ein neues Feature im Team zu diskutieren, eine Kollegin das Feature reviewen und approven zu lassen oder auch gemeinsam neue Commits in dem Feature-Branch zu erstellen.

### Code-Review

Man kann den Merge-Request einer anderen Person zuweisen, einen Reviewer eintragen oder konfigurieren dass der MR approved werden muss.

![image](https://github.com/user-attachments/assets/fc1274d6-8ca8-4028-99e4-1e6f995b3ad6)

Probiert es gleich aus: 

* wenn man bei "Approval required" eine Zahl größer 0 angibt, müssen andere Kollegen den Merge-Request approven, damit gemerged werden kann.
* tragt einen Reviewer ein, die Person sollte dann links bei "Merge Requests" auch "Review requests" sehen und einen Review starten können.

Ein Reviewer kann den Code commentieren, approven oder eine Änderung verlangen.

![image](https://github.com/user-attachments/assets/972d8f9c-0f8e-4303-9f3a-17af5f8e935e)

Man kann auch direkt im Tab "Changes" seine Kommentare bei der jeweiligen Code-Zeile ergänzen:

![image](https://github.com/user-attachments/assets/38c280e2-a7c9-4104-ad34-156070ad5d40)

oder in der Overview ein Kommentar abgeben:

![image](https://github.com/user-attachments/assets/aaacbc9d-6e05-4f40-909c-c97be86d6341)

### Approval Rules

Approval Rules können pro Merge-Request gesetzt werden, oder standardmäßig auf Projektebene. Auf Projektebene ist es sinnvoller, um einen Approve zu erzwingen.

### Git-Pipelines als Quality-Gates

Man kann auch konfigurieren dass alle Git-Pipelines erfolgreich ("grün") sein müssen, bevor der Merge-Request gemerged werden kann.

## Merge-Konflikt auflösen

Wann entstehen Merge-Konflikte:

Merge-Konflikte entstehen, wenn in der gleichen Zeile derselben Datei von verschiedenen Personen konkurrierende Änderungen vorgenommen werden oder wenn eine Person eine Datei bearbeitet und eine andere Person die Datei löscht. 

Wichtig: die gleiche Datei an einer anderen Stelle editieren resultiert im Normalfall nicht in einem Merge-Konflikt!

Im Merge-Request schaut das dann so aus:

![image](https://github.com/user-attachments/assets/1db6e3a3-d2fa-46a3-98f0-11ad6163fdf1)

TODO: wie auflösen?



Updaten von Branches (git rebase)
Auflösen von Merge-Konflikten
Merge-Requests erstellen
Zusammen in eine Feature-Branch arbeiten (zweite checkt Feature-Branch aus, fügt Commits hinzu) ... was ändert sich im Merge-Request?
MR Review und Approve

Welche andere Dinge sieht man bei Merge-Requests noch? Was sind Best-Practices?

Merge-Request Möglichkeiten (Merge-Commit, Squash and Merge, Fast-Forward, ... in Merge-Request den Feature-Branch updaten? geht das?)




Namenskonventionen für Branches und Commits (conventional commits, conventional branches?)


Best Pratices kurz gemeinsam durchgehen: https://about.gitlab.com/topics/version-control/what-are-gitlab-flow-best-practices/


