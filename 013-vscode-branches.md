# In VSCode mit Remote-Branches arbeiten

In diesem Abschnitt lernen wir wie man im VSCode mit Remote-Repositories arbeitet.

## Commits aufs Remote-Repository pushen (git push)

In Source-Control-View mit dem Button "Sync Changes".

![image](https://github.com/user-attachments/assets/8fe1f1c1-f143-404e-ac70-c5d9b907fb67)

Im Gitlab-Projekt solltet ihr diese Commits jetzt auch sehen:

![image](https://github.com/user-attachments/assets/634aedfb-cbfe-4ce0-8169-e06fcf8b68d9)

Klick mal in die Commits und lass dir die Details anzeigen.

## In VSCode Branches erstellen und auf GitLab pushen

Analog zu `git checkout -b feat/neues-feature` kann man im VSCode so einen neuen Branch erstellen:

![image](https://github.com/user-attachments/assets/969be9a8-6823-43e3-8de5-951750eb57a0)

Anschließend im Textfeld den Branch-Namen angeben, z.B. `feat/neues-feature`.

Ganz unten im VSCode solltest du jetzt auch den neuen Branch-Namen sehen.

Erstelle jetzt in diesem neuen Branch ein neues File `neues-feature.txt`.

In der Source-Control-View sieht man den neuen Branch:

![image](https://github.com/user-attachments/assets/abcbd566-4011-434a-af5a-d8679f94c407)

und mit "Publish Branch" wird der Branch auch auf das Remote-Repository in GitLab gepusht:

![image](https://github.com/user-attachments/assets/70f5a671-445e-40f4-bd1a-cefd485b0933)

Diesen neuen Feature-Branch sieht man jetzt auch im GitLab-Projekt:

![image](https://github.com/user-attachments/assets/d59ced66-28b2-473b-b5ae-b784597177e9)


## Merge-Request in GitLab erstellen

Sobald ein neuer Branch im GitLab auftaucht wird in unterschiedlichen Views schon automatisch darauf hingewiesen und die Möglichkeit einen Merge-Request zu erstellen, angeboten:

![image](https://github.com/user-attachments/assets/6faff11d-5d5c-4a99-a4ad-a80858eee835)

So kann man immer einen neuen Merge-Request im GitLab erstellen:

![image](https://github.com/user-attachments/assets/6a6f769c-52c0-4a6c-b9c5-227371feceb4)

Source-Branch: der Feature-Branch mit den neuen Commits
Target-Branch: meistens `main`, wo die neuen Commits ergänzt werden sollen.

`Create merge request` --> `Merge`

Merge-Requests bleiben im System erhalten unter `Code` --> `Merge requests`

Schaut unter `Code` --> `Commits` die neuen Commits an, und unter `Code` --> `Repository Graph` den Commit-Graphen.


## In VSCode wieder in den main-Branch wechseln und neue Commits pullen

Analog zu `git checkout main` und `git pull`

![image](https://github.com/user-attachments/assets/fa467780-9067-4d61-91fe-9828b8e7e30d)

"Synchronize Changes": ![image](https://github.com/user-attachments/assets/8a95ad84-9a2a-45c9-9fe3-3d1f7806763a)

