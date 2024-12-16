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

Pipelines können durch unterschiedliche Events getartet werden.

### Manuell

Pipelines können manuell gestartet werden über den Menüpunkt "Build" --> "Pipelines -- "Run Pipeline"

![image](https://github.com/user-attachments/assets/5740685b-0c55-4dcc-9e32-1ccca6337d24)

Dann den Branch auswählen und ggf. Variablen definieren:

![image](https://github.com/user-attachments/assets/0b060dcc-5880-4226-9c9a-6c4d66be13fe)

### Gescheduled

Im Menü über "Build" --> "Pipeline Schedules" --> "New Schedule" 

![image](https://github.com/user-attachments/assets/c7336fd5-5b57-4421-ac73-7003ec13ecb0)

### Bei Git-Events

Standardmäßig werden Pipelines bei jeder Änderung in Git getriggert. Das führt dazu, dass Pipelines standardmäßig sehr oft ausgeführt werden.
Bei einer "normalen" Code-Änderung über einen Feature-Branch z.B. mindestens 3 mal:

* beim Git Push auf den Feature-Branch
* Beim Erstellen vom Merge-Request
* Beim Merge-Commit auf den main-Branch

![image](https://github.com/user-attachments/assets/a360fa98-a7a2-41f7-91e8-4cc6141559e7)


Wenn man hier expliziertere Regeln anwenden will, muss man Rules definieren.
Dann werden die Pipelines und Jobs nur mehr ausgeführt, wenn die  jeweilige Regel erfüllt ist.

#### Workflow-Rules

Mit sog. Workflow-Rules bestimmt man, ob die Pipeline überhaupt erstellt wird.

Beispiele:

```
workflow:
  rules:
    - if: $CI_PIPELINE_SOURCE == "web"
      when: never
    - when: always
```
Was bedeutet diese Rule? Probiers aus!

Sollte dasselbe sein wie:

```
workflow:
  rules:
    - if: $CI_PIPELINE_SOURCE != "web"
```

Pipeline soll nur bei Merge-Request laufen:

```
workflow:
  rules:
    - if: '$CI_PIPELINE_SOURCE == "merge_request_event"'
```

siehe https://docs.gitlab.com/ee/ci/yaml/workflow.html
[weitere CI_PIPELINE_SOURCE Möglichkeiten](https://docs.gitlab.com/ee/ci/jobs/job_rules.html#ci_pipeline_source-predefined-variable)

#### Job-Rules

Mit sog. Job-Rules bestimmt man, ob der Job in dieser Pipeline aufgerufen wird.
Das kommt häufiger vor als das deaktivieren der ganzen Pipeline, weil man unterschiedliche Jobs bei unterschiedlichen Git-Events ausführen will.

Beispiel:

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
  rules:
  - if: '$CI_PIPELINE_SOURCE == "merge_request_event"'
  - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
  script:
    - echo "ich baue die software"

test-job:
  stage: test
  rules:
  - if: '$CI_PIPELINE_SOURCE == "merge_request_event"'
  - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
  script:
    - echo "ich teste die software"

deploy-job:
  stage: deploy
  rules:
  - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
  script:
    - echo "ich deploye die software"

post-deploy-test-job:
  stage: post-deploy
  rules:
  - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
  script:
    - echo "ich teste die applikation nach dem deployment"
```

Wann werden hier welche Jobs ausgeführt? Probiere es aus!

![image](https://github.com/user-attachments/assets/d4caedcb-04eb-41b6-92cc-8f73fe4ae8a6)

siehe https://docs.gitlab.com/ee/ci/jobs/job_rules.html
und https://docs.gitlab.com/ee/ci/yaml/index.html#rules

Keyword `only` und `except` sind legacy. Können weiterhin verwendet werden, aber nicht in Kombination mit `rules`.

#### Pipelines direkt in Merge-Requests ersichtlich

Wenn Pipelines bei Merge-Requests aufgerufen werden, wird die Pipeline direkt beim MR anzeigt:

![image](https://github.com/user-attachments/assets/894d3d06-adc6-4fc8-81f7-627803182143)

### Durch einen GitLab API-Call

siehe https://docs.gitlab.com/ee/ci/triggers/

### Durch eine andere Pipeline

siehe https://docs.gitlab.com/ee/ci/pipelines/downstream_pipelines.html

### Pipelines und Jobs restarten 

Wenn Pipelines oder einzelne Jobs fehlgeschlagen sind, können sie auch wiederholt werden:

![image](https://github.com/user-attachments/assets/d4548c09-50bb-4188-acb1-7f8cca134813)

### Pipelines Status in Commits-Übersicht

Auch in der Commits-Übersicht sieht man ob die Pipelines erfolgreich waren:

![image](https://github.com/user-attachments/assets/e2b2df99-d176-4aab-969c-91a42386df14)

## Pipeline weiter konfigurieren

### Defaults

Klassische Default sind die Definition eines Container-Images das in jedem Job verwendet werden soll oder Pre- und Post-Scripts für jeden Job.

Beispiel:

```
default:
  image: alpine:latest
  before_script:
    - echo "Starte Job ..."
  after_script:
    - echo "Beende Job ..."
```

siehe https://docs.gitlab.com/ee/ci/yaml/index.html#default

### Manuelle Bestätigung einbauen

siehe manual_confirmation: 'Are you sure you want to delete this environment?'

```
deploy-job:
  stage: deploy
  rules:
  - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
    when: manual
  manual_confirmation: "Are you sure you want to deploy?"
  script:
    - echo "ich deploye die software"
```

Führt dazu dass jemand manuell den Step nochmal bestätigen muss:

![image](https://github.com/user-attachments/assets/431ced15-0988-479b-8b78-77889cc9167a)

### Variablen

Über Variablen kann der Ablauf von Pipelines gesteuert werden und auch die Tools / Scripts innerhalb eines Job können diese Variablen einlesen.
Unkritische Variablen können direkt in der .gitlab-ci.yml definiert werden, siehe https://docs.gitlab.com/ee/ci/variables/ .
Diese Variablen können auch bei manuellem starten der Pipeline überschrieben werden.

Beispiel: meine Scripts haben alle ein Debug-Flag und dieses möchte ich zentral in allen Jobs setzen

```
variables:
  DEBUG_ON: true
```

Achtung: Sicherheitskritische Variablen, z.B. Access-Tokens zu seiner Cloud-Infrastruktur, sollen nicht im .gitlab-ci.yml setzen sondern in der [GitLab UI](https://docs.gitlab.com/ee/ci/variables/#define-a-cicd-variable-in-the-ui).

![image](https://github.com/user-attachments/assets/152d8046-3688-4773-b284-6b1ba9a055c8)

"Protect variables" sind nur in "protected Branches" verfügbar, damit niemand diese Variablen in einem Feature-Branch auslesen und bei sich lokal verwenden kann!

Wichtig: Änderungen an .gitlab-ci.yml Files immer speziell beim Merge-Request-Review beachten und auf Zugriff und Weitergabe von kritischen Variablen prüfen.

#### Predefined Variables

siehe https://docs.gitlab.com/ee/ci/variables/predefined_variables.html

### Abhängigkeiten definieren ("needs")

Mit dem `needs` Keyword kann man explizit definieren welche Jobs vor diesem Job ausgeführt sein müssen, um diesen dann eventuell schneller starten zu lassen aber trotzdem alle Vorbedingungen zu erfüllen. (startet dann früher als die gesamte Stage)
siehe https://docs.gitlab.com/ee/ci/yaml/needs.html

### Includes

Gewisse Teile eines .gitlab-ci.yml können auch in andere Files (in anderen Repos) ausgelagert werden und eingebunden werden.
Das können nur Variablen sein, aber auch ganze Jobs.

Aufgabe: einer von euch erstellt eine Pipeline und die anderen includen sie, und fügen nur bei einer gewissen Stage einen zusätzlichen Job hinzu.

siehe https://docs.gitlab.com/ee/ci/yaml/includes.html

### Artifacts und Cache

Mit [Artifacts](https://docs.gitlab.com/ee/ci/yaml/index.html#artifacts) kann man Files erstellen, die dann in der GitLab-UI zu dem Job/Pipeline heruntergeladen werden können.

Mit [Caches](https://docs.gitlab.com/ee/ci/yaml/index.html#cache) kann man Daten zwischen Jobs und Pipelines wiederverwenden. siehe auch https://docs.gitlab.com/ee/ci/caching/index.html

## GitLab-Runner

Runner werden üblicherweise von den GitLab-Administratoren zur Verfügung gestellt und registriert. Wenn man wissen will welche Runner im Projekt zur Verfügung stehen, kann man unter "Settings" --> "CI/CD" --> "Runners" nachschauen:

![image](https://github.com/user-attachments/assets/b26eef8f-39e6-4a48-b5aa-f7512078b725)

## Pipeline Components

Man kann auch Logik von Pipelines in sogenannten Components wiederverwendbar machen: https://docs.gitlab.com/ee/ci/components/

## Pipeline Syntax Referenz

siehe https://docs.gitlab.com/ee/ci/yaml/index.html
Predefined Variables: https://docs.gitlab.com/ee/ci/variables/predefined_variables.html
Kubernetes Executor als Pipeline Runner: https://docs.gitlab.com/runner/executors/kubernetes/

