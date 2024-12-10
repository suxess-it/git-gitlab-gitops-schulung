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

### .gitlab-ci.yml erstellen

Es gibt mehrere Arten wie ein `.gitlab-ci.yml` erstellt werden kann. Da es einfach ein ganz normales File ist, kann es in eurem lokalen Repo im VSCode erstellt werden.

Man kann aber auch den Pipeline-Editor direkt im Gitlab verwenden.

![image](https://github.com/user-attachments/assets/5814f8fa-9dd2-4878-953b-9a43a00c3317)

Details zu Jobs siehe https://docs.gitlab.com/ee/ci/jobs/
