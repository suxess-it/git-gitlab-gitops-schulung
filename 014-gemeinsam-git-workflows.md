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

1) In der git-Bash das Repository klonen und dann den Folder im VSCode öffnen
2) Direkt im VSCode das Repository klonen

Darauf achten dass der main-Branch ausgecheckt ist und mit aktuellen Stand vom `origin/main` hat. Wie macht man das?


## Git-Projekt weiterentwickeln

Wie im Gitlab-Flow definiert werden Änderungen immer über einen Feature-Branch gemacht. 
Deshalb muss jetzt vom main-Branch aus ein neuer Feature-Branch abgezweigt werden.

Aufgabe: Jeder Schulungsteilnehmer erstellt in seinem Feauture-Branch ein neues File mit dem Namen "<Vorname>_<Nachname>.txt" und ergänzt im README.md in der Mitglieder-Liste deinen Namen.



Erstellen von Branches

Updaten von Branches (git rebase)
Auflösen von Merge-Konflikten
Merge-Requests erstellen
Zusammen in eine Feature-Branch arbeiten (zweite checkt Feature-Branch aus, fügt Commits hinzu) ... was ändert sich im Merge-Request?
MR Review und Approve

Welche andere Dinge sieht man bei Merge-Requests noch? Was sind Best-Practices?

Merge-Request Möglichkeiten (Merge-Commit, Squash and Merge, Fast-Forward, ... in Merge-Request den Feature-Branch updaten? geht das?)




Namenskonventionen für Branches und Commits (conventional commits, conventional branches?)


Best Pratices kurz gemeinsam durchgehen: https://about.gitlab.com/topics/version-control/what-are-gitlab-flow-best-practices/


