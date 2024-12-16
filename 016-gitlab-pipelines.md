# GitLab Pipelines

In der GitLab UI sind alle wesentlichen Informationen zu Pipelines unter dem Menüpunkt "Build" zu finden:

![image](https://github.com/user-attachments/assets/dfc376db-d48a-4208-b694-ac432fc08fea)

* Pipelines: alle Pipelines die in diesem Projekt gelaufen sind
* Jobs: alle Jobs die in diesem Repository gelaufen sind (mit Referenz zur jeweiligen Pipeline)
* Pipeline-Editor: siehe weiter unten
* Pipeline schedules: Aufruf zyklisch einplanen
* Artifacts: jede Pipeline erzeugt Artefakte, die man sich im Nachhinein anschauen kann

## Erstes .gitlab-ci.yml

Ein Grundbaustein jeder Pipeline ist ein `Job`. Jobs werden einfach so im .gitlab-ci.yml definiert:

In diesem Fall lautet mein Job `mein_job`, die Namen sind aber frei wählbar (außer bestimmte [Keywords](https://docs.gitlab.com/ee/ci/yaml/index.html#keywords)).
Ein Job benötigt zumindest das Attribut `script`, um zu beschreiben welchen Befehl dieser Job ausführen soll.

```
mein-job:
  script:
    - echo "hallo welt!"
```
Dieser Job würde jetzt auf einem GitLab-Runner im Default-Container von GitLab ausgeführt werden.

Details zu Jobs siehe https://docs.gitlab.com/ee/ci/jobs/

### .gitlab-ci.yml erstellen

Wie erstellt man ein .gitlab-ci.yml?

Es gibt mehrere Arten wie ein `.gitlab-ci.yml` erstellt werden kann. Da es einfach ein ganz normales File wie jedes andere im Git-Repo ist,
kann es in eurem lokalen Repo im VSCode erstellt werden.

Man kann aber auch den Pipeline-Editor direkt im Gitlab verwenden. Wichtig: auch hier zuerst in einem Feature-Branch die Pipeline entwickeln!

![image](https://github.com/user-attachments/assets/5814f8fa-9dd2-4878-953b-9a43a00c3317)

Sobald dieser Job am GitLab-Server in irgendeinem Branch committed wurde, wird er schon ausgeführt:

![image](https://github.com/user-attachments/assets/6b9af8c3-467b-4eb5-82cc-fa153b425240)

## Pipelines mit definiertem Workflow

Erstellt diese Pipeline im GitLab Pipeline-Editor. Versucht mal einen Job einer Stage zuzuweisen die es nicht gibt. Welche Information bekommt ihr vom Pipeline-Editor?

```
stages:
  - lint
  - build
  - test
  - deploy
  - post-deploy

format-check-job:
  stage: lint
  script:
    - echo "ich checke die formatierung"

syntax-check-job:
  stage: lint
  script:
    - echo "ich checke den syntax"

code-analyse-job:
  stage: lint
  script:
    - echo "ich mache statische code-analyse"

build-job:
  stage: build
  script:
    - echo "ich baue die software"

test-job:
  stage: test
  script:
    - echo "ich teste die software"

deploy-job:
  stage: deploy
  script:
    - echo "ich deploye die software"

post-deploy-test-job:
  stage: post-deploy
  script:
    - echo "ich teste die applikation nach dem deployment"
```

Weitere Details und Beispiele: https://docs.gitlab.com/ee/ci/pipelines/pipeline_architectures.html#basic-pipelines


## Status von Jobs und Pipelines checken

Wenn wir im Gitlab-Projekt links auf "Build" --> "Pipelines" klicken sehen wir alle Pipelines die gerade laufen bzw. schon beendet worden sind:

![image](https://github.com/user-attachments/assets/0355ae20-b08b-4c06-b2b7-15c497269f7c)

Was sieht man in diesem Bild?

* Status: wartet die Pipeline (Pending), läuft sie (Running), erfolgreich abgeschlossen (Passed) oder mit Fehler abgebrochen (Failed)
* Pipeline:
    * Commit-Message (erste Zeile)
    * Pipeline-ID (in unserem Fall `#23429`): klicke darauf um Details zur Pipeline zu sehen
    * Branch (`feat/create-pipeline`)
    * Commit (`dc81136e`)
    * Committer-Avatar
    * Latest ( ? )
* Created by: Wer hat die Pipeline gestartet? (meistens der Committer)
* Stages: erfolgreich oder nicht

Wenn man auf die Pipeline klickt (Status-Symbol in erster Spalte oder auf die Pipeline-ID) dann kann man sich mehr Details zur Pipeline anschauen.

## Wann werden Pipelines aufgerufen

### Manuell


### Gescheduled


### Getriggered bei Git-Events


Wenn Pipelines bei Merge-Requests aufgerufen werden, wird die Pipeline direkt beim MR anzeigt:

![image](https://github.com/user-attachments/assets/894d3d06-adc6-4fc8-81f7-627803182143)


### Pipelines und Jobs restarten 

z.B. bei Fehlern ...

## Pipeline weiter konfigurieren

### Images

### Variablen

#### Predefined Variables

siehe 

### Abhängigkeiten definieren ("needs")

### ?

### Artifacts und Cache

Mit [Artifacts](https://docs.gitlab.com/ee/ci/yaml/index.html#artifacts) kann man Files erstellen, die dann in der GitLab-UI zu dem Job/Pipeline heruntergeladen werden können.

Mit [Caches](https://docs.gitlab.com/ee/ci/yaml/index.html#cache) kann man Daten zwischen Jobs und Pipelines wiederverwenden. siehe auch https://docs.gitlab.com/ee/ci/caching/index.html

## GitLab-Runner

Runner werden üblicherweise von den GitLab-Administratoren zur Verfügung gestellt und registriert. Wenn man wissen will welche Runner im Projekt zur Verfügung stehen, kann man unter "Settings" --> "CI/CD" --> "Runners" nachschauen:

![image](https://github.com/user-attachments/assets/b26eef8f-39e6-4a48-b5aa-f7512078b725)


## Pipeline Syntax Referenz

siehe https://docs.gitlab.com/ee/ci/yaml/index.html

