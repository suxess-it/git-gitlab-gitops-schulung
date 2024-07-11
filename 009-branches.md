# Branches erstellen

Branches dienen also dazu von einem bestimmten Entwicklungszweig (meistens dem Haupt-Branch) wieder abzuzweigen.
Einen Branch kann man auf zwei unterschiedliche Arten erstellen.

Mit `git checkout -b <neuer-branch>` wird ein neuer Branch erstellt und gleich in diesen gewechselt:

```bash
$ git checkout -b feat/mfa
Switched to a new branch 'feat/mfa'
```

Mit `git branch <neuer-branch>` wird nur ein neuer Branch erstellt, aber noch nicht in diesen Branch gewechselt.<br>
Zum Wechseln muss man `git switch <branch>` ausführen.

```bash
$ git branch feat/mfa

$ git switch feat/mfa
Switched to branch 'feat/mfa'
```

In der git-bash sieht man den Branch, in dem man gerade arbeitet, auch in der Befehlszeile!

![image](https://github.com/suxess-it/git-gitlab-gitops-schulung/assets/11465610/4b11bba3-9cab-4228-b490-c04a2e9df71c)


# Branch löschen

Ein Branch kann mit `git branch -d <branch-name>` wieder gelöscht werden. Aber Achtung, nicht den Zweig abschneiden,
auf dem man sitzt ;)

```bash
$ git branch -d feat/mfa
error: cannot delete branch 'feat/mfa' used by worktree at 'C:/Users/johannes.kleinlercher@suxess-it.com/git-schulung/projekt1'
```

besser:

```bash
$ git switch main
Switched to branch 'main'
$ git branch -d feat/mfa
Deleted branch feat/mfa (was 02f7cd7).
```

# Commits im Branch erstellen

```bash
$ git checkout -b feat/mfa
$ echo "feature: 123" >> neues-file.txt
$ git add neues-file.txt
$ git commit -a -m "feat: erster versuch des neuen features"

$ git log --all --oneline --graph
* a20f10d (HEAD -> feat/mfa) feat: erster versuch des neuen features
* ae3e653 (main) Revert "das file gefällt mir nicht mehr"
* 10128d1 ich möchte nochmal commits erklären
* 0e3d42a das file gefällt mir nicht mehr
```

Im Git-Log sieht man jetzt dass der main-Branch beim Commit ae3e653 endet,
der feat/mfa-Branch gerade beim darauf folgenden Commit a20f10d steht.
Dort ist auch der HEAD, weil der aktuell ausgecheckte Branch der Branch feat/mfa ist.

Jetzt erstellen wir noch im main-Branch ein paar Commits, um die Weiterentwicklung im main-Branch zu simulieren.

Wieder in den main-Branch wechseln (kann über `git switch main` oder `git checkout main` erfolgen):

```bash
$ git checkout main
Switched to branch 'main'

$ echo "main: weiterentwicklung" >> dasisteinfile.txt
$ git add dasisteinfile.txt
$ git commit -a -m "kleine weiterentwicklung im main-Branch"

$ echo "main: weiterentwicklung teil 2" >> dasisteinfile.txt
$ git commit -a -m "noch eine weiterentwicklung im main-Branch"

$ git log --all --oneline --graph
* 3f8fb95 (HEAD -> main) noch eine weiterentwicklung im main-Branch
* e2d83b4 kleine weiterentwicklung im main-Branch
| * a20f10d (feat/mfa) feat: erster versuch des neuen features
|/
* ae3e653 Revert "das file gefällt mir nicht mehr"
* 10128d1 ich möchte nochmal commits erklären
```

Etwas schöner sieht man es im VS Code mit der [Git-Graph Extension](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph):

![image](https://github.com/user-attachments/assets/8c29481b-f893-4f34-bae7-41eb69fd485b)



# Änderungen von zwei Branches zusammenführen

Wenn ein main-Branch und ein Feature/Fix-Branch parallel weiterentwickelt werden,
gibt es zwei Gründe Änderungen von einem in den anderen Branch zu übernehmen.

## Neue Commits vom main-Branch in den Feature-Branch übernehmen

Das ist dann wichtig, wenn sich der main-Branch weiterentwickelt hat,
und man will im Feature-Branch wissen ob der aktuellste Code vom main-Branch
auch mit den Neuentwicklungen vom Feature-Branch funktioniert.

Das will man im Feature-Branch testen, bevor man das Feature im main-Branch public macht.

### Rebase

Mit `git rebase` werden die Commits vom Feature-Branch auf den letzten Commit des main-Branch gelegt.
Damit ändern sich die Commits des Feature-Branches natürlich, weil ihr Inhalt ein anderer ist. Das macht git automatisch.<br>

Vor dem Rebase:

![image](https://github.com/suxess-it/git-gitlab-gitops-schulung/assets/11465610/b147a45a-3c20-455f-b981-1b79ee7db001)

Nach dem Rebase:

![image](https://github.com/suxess-it/git-gitlab-gitops-schulung/assets/11465610/1fc2d0f9-6a56-4031-adb8-7f160c7852a8)

Hintergrund: Eigentlich macht Git für jeden Commit den er "verschieben" muss ein `git cherry-pick`.
Git schaut sich den Unterschied zwischen den Commits in der "alten" Commit-Reihe an,
und packt diese Änderungen in neuen Commits auf die neue Commit-Reihe.

Der Command um einen Rebase des Feature-Branches auf den Master-Branch zu machen:

```bash
$ git rebase main feat/mfa
Successfully rebased and updated refs/heads/feat/mfa.
```

Wenn man sich jetzt das Git-Log ansieht, sieht man dass der Commit vom Feature-Branch nach dem letzten Commit vom main-Branch erfolgt und eine neue Commit-ID bekommen hat:

```git bash
$ git log --all --oneline --graph
* b83a7e8 (HEAD -> feat/mfa) feat: erster versuch des neuen features
* 3f8fb95 (main) noch eine weiterentwicklung im main-Branch
* e2d83b4 kleine weiterentwicklung im main-Branch
* ae3e653 Revert "das file gefällt mir nicht mehr"
```

Vergleiche diesen Git-Log mit dem vorigen von oben!

Die Änderungen die im main-Branch gemacht wurden, sieht man jetzt auch im Feature-Branch:

```bash
$ git switch feat/mfa
Already on 'feat/mfa'

$ cat dasisteinfile.txt
main: weiterentwicklung
main: weiterentwicklung teil 2
```

### Merge

Statt einem Rebase kann auch ein Merge-Commit gemacht werden.

Dazu wieder ein paar Commits im main-Branch erstellen:

```bash
$ git checkout main
$ echo "main: weiterentwicklung teil 3" >> dasisteinfile.txt
$ git commit -a -m "wieder aenderungen im main-Branch"
$ echo "main: weiterentwicklung teil 4" >> dasisteinfile.txt
$ git commit -a -m "schon wieder aenderungen im main-Branch"
$ git log --all --oneline --graph
```

Jetzt ist der main-Branch wieder zwei Commits weiter als der Feature-Branch.<br>
Jetzt bringen wir diese zwei Commits vom main-Branch über einen merge-Commit in den Feature-Branch:

```bash
$ git switch feat/mfa
$ git merge main --no-edit
Merge made by the 'ort' strategy.
 dasisteinfile.txt | 2 ++
 1 file changed, 2 insertions(+)

$ git log --all --oneline --graph
*   932e922 (HEAD -> feat/mfa) Merge branch 'main' into feat/mfa
|\
| * 901eef7 (main) schon wieder aenderungen im main-Branch
| * 2958d1d wieder aenderungen im main-Branch
* | 2bf8a3f feat: erster versuch des neuen features
|/
* dbaa640 noch eine weiterentwicklung im main-Branch
* 512c2b9 kleine weiterentwicklung im main-Branch
* ae3e653 Revert "das file gefällt mir nicht mehr"
* 10128d1 ich möchte nochmal commits erklären
```

Der offensichtliche Unterschied ist, dass die Commits im Feature-Branch bei einem Merge nicht verschoben oder verändert werden. Bei einem Rebase aber schon!<br>
Außerdem wurde ein zusätzlicher Commit erzeugt um die Änderungen vom main-Branch in den Feature-Branch zu bringen.

![image](https://github.com/suxess-it/git-gitlab-gitops-schulung/assets/11465610/a70338af-1e83-4d68-8441-32ae1f5e578f)

Aber wichtig: es sind immer noch erst die Änderungen vom main-Branch im Feature-Branch:

```bash
$ cat dasisteinfile.txt
main: weiterentwicklung
main: weiterentwicklung teil 2
main: weiterentwicklung teil 3
main: weiterentwicklung teil 4
```

Aber im main-Branch sind noch keine Änderungen vom Feature-Branch:

```bash
$ git switch main
Switched to branch 'main'

$ cat neues-file.txt
hallo ich bin da
```

Wie könnte man mit `git diff` diese Unterschiede anzeigen lassen? Hat jemand eine Idee?

## Änderungen vom Feature-Branch in den main-Branch bringen

Um jetzt den Feature-Branch in den main-Branch zu mergen, kann man folgendes aufrufen:

```bash
$ git switch main
Switched to branch 'main'

$ git merge feat/mfa --no-edit
Updating 3f8fb95..5a68398
Fast-forward
 neues-file.txt | 1 +
 1 file changed, 1 insertion(+)
```

Es wird "Fast-Forward" ausgegeben (sog. "Fast-Forward"-Merge),
weil der main-Branch-Zeiger nur auf den nächsten Commit verschoben werden muss (Fast-Forward).

```bash
$ git log --all --oneline --graph
*   932e922 (HEAD -> main, feat/mfa) Merge branch 'main' into feat/mfa
|\
| * 901eef7 schon wieder aenderungen im main-Branch
| * 2958d1d wieder aenderungen im main-Branch
* | 2bf8a3f feat: erster versuch des neuen features
|/
* dbaa640 noch eine weiterentwicklung im main-Branch
* 512c2b9 kleine weiterentwicklung im main-Branch
* ae3e653 Revert "das file gefällt mir nicht mehr"
* 10128d1 ich möchte nochmal commits erklären
```

![image](https://github.com/suxess-it/git-gitlab-gitops-schulung/assets/11465610/5e40d174-378e-4257-8f94-e254cc20d49e)


# Wann macht man kein Rebase?

`git rebase` kann eine gute Wahl sein, um die neuesten Commits vom main-Branch in den Feature-Branch zu bringen.<br>
Da sich dann aber alle Commits vom Feature-Branch ändern müssen (warum eigentlich??) müssen das alle beteiligten Entwickler vom Feature-Branch wissen.<br>
Der Vorteil ist, dass kein weiterer Merge-Commit im Feature-Branch erstellt wird.

Wann man auf jeden Fall *kein* Rebase machen sollte, ist im main-Branch wo sehr sehr viele Entwickler daran arbeiten,
weil die alle andere Commits in ihrem lokalen Repository haben!

![image](https://github.com/suxess-it/git-gitlab-gitops-schulung/assets/11465610/1fd84530-e607-40b3-a524-227a5bf5f91d)

# Rebase rückgängig machen (hauptsächlich für mich um Merge statt Rebase zu zeigen)

```bash
$ git reflog
```

Dann ID lt. reflog finden

```bash
$ git reset --hard HEAD@{8}

$ git log --all --oneline --graph
* b83a7e8 (feat/mfa) feat: erster versuch des neuen features
* 3f8fb95 (HEAD -> main) noch eine weiterentwicklung im main-Branch
* e2d83b4 kleine weiterentwicklung im main-Branch
* ae3e653 Revert "das file gefällt mir nicht mehr"
```





