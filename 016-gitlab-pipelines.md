# GitLab Pipelines

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
