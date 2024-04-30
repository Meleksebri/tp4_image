# Sécurité Logicielle
## Analyse des dépendances
### Dependabot
Dependabot est un outil intégré dans GitHub qui permet d'analyser les dépendances vulnérables automatiquement.
Voici les résultats obtenus lors de l'analyse :
<br />
<img src="images/dependabot.png">
<br />
L'ensemble des vulnérabilités trouvées sont dans le pom.xml.

Voici les CVE recueillis par dependabot :
```
CVE-2022-42003
CVE-2021-46877
CVE-2022-42004
CVE-2020-36518
CVE-2020-15250
```
---
### Dependency Review
Afin d'avoir une autre perspective sur les vulnérabilités de dépendance, nous avons utilisé
un autre outil : dependancy-review. Cet outil est configuré de manière à ce qu'il s'exécute lors
automatiquement d'un push et manuellement par un développeur.
<br />
<img src="images/dependency-review-findings.png">
<br />
Tel qu'on peut voir, l'outil a trouvé deux failles de dépendances lors d'un pull request.
---
### Analyse du code
D'un autre côté, nous avons analysé le code afin d'y trouvé de potentielles failles
de sécurité. Pour se faire, nous avons utilisé CodeQL, un outil disponible sur GitHub,
et nous l'avons intégré à notre Workflow. Lors d'un push dans main, cet outil est lancé automatiquement
et fait un balayage de vulnérabilités sur notre branch main. À des fins de tests, nous l'avons
lancé manuellement. Voici les résultats :
<br />
<img src="images/file_scanned.png">
<img src="images/scanning.png">
<br />
Tel qu'on peut le remarqué, tous nos fichiers ont été analysés et aucune vulnérabilité
n'a été trouvé.

Voici la configuration pour le lancement automatique des analyses de CodeQL et de
dependency-review :
<br />
<img src="images/workflow-codeql.png"/>
<img src="images/workflow-dependency-review.png"/>

---
## Pratiques sécuritaires
Afin d'améliorer l'aspect sécurité de notre logiciel, nous pourrions adopter une approche
DevSecOps. En effet, cette approche encourage la collaboration entre les membres des équipes de
développement, de sécurité et d'opération et prône l'automatisation. La force du DevSecOps est
la rapidité de la détection et de la correction des vulnérabilités. Cela a pour effet de réduire
les coûts de correction, d'améliorer la qualité logiciel et finalement, de livrer le produit plus
rapidement.

Une autre pratique cruciale à la sécurité de notre projet serait celle de la gestion des vulnérabilités.
En effet, celle-ci cherche à classer les vulnérabilités et à garder un suivi de celles-ci.
Une gestion des vulnérabilités est importante lorsqu'un projet devient gros et que de multiples
vulnérabilités sont découvertes. Cette gestion permet de savoir quelle faille priorisé et comment la régler.

D'un autre côté, nous pourrions effectué plus de test. En effet, nous pourrions utiliser des solutions de
test statique du code (CodeQL), utiliser des outils qui test dynamiquement les appels API de notre application et/ou
faire appel à un pentester pour tester notre projet. Cela permettrait de couvrir tous les angles de notre projet
et ainsi être sûr d'avoir trouvé le maximum de vulnérabilités exposées.