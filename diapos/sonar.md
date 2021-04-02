# Sonarqube

## Rappel Qualité d'un produit logiciel:

Norme ISO 25010 :
Adéquation fonctionnelle, Efficience des performances, Compatibilité, Facilité d'utilisation, Portabilité
Fiabilité (sans bug), Maintenabilité (facilité de modification, testabilité, audit qualité logicielle),  sécurité (audit de code)

La qualité du code peut être notamment mesurée au regard :
•De mesures des taux de couverture du code 
•De métriques relatives à la lisibilité du code et à sa complexité
•Du respect d’un ensemble de pratiques définies dans un référentiel de règles de codage.

## Sonarqube

Le logiciel open source de mesure de la qualité du code source d'un produit (en développement ,en maintenance), analyse statique.
Se base sur le code source (Java, Python, PHP, JavaScript...) ainsi que sur les tests automatisés et le taux de couverture associés

Schéma sonar 
https://docs.sonarqube.org/latest/setup/install-server/

https://sonar.insee.fr/
https://sonar.recette.insee.fr/

## Scanner:

Gradle - SonarScanner for Gradle
Maven - use the SonarScanner for Maven
Jenkins - SonarScanner for Jenkins
Ant - SonarScanner for Ant
SonarScanner (pour le reste)

## Métrique de SonarQube

Système de note de A (Très bien) à E (à très mauvais)
Dépendant des règles du profil qualité (par défaut sonar-way), règle classé par catégorie, niveau de sévérité, temps de remédiation

L'important est d'améliorer la qualité petit à petit. La note est là pour encourager au progrès

### Catégorie

Bug, Vulnérabilité, Mauvaise pratique (code smells), Sécurité

### Niveau

Bloquant : Risque opérationnel ou de sécurité, pouvant provoquer une instabilité globale de l'application en production.
Critique : Risque opérationnel ou de sécurité, provoquer un comportement inattendu de l'application en production
Majeur : Risque d'impact conséquent sur la productivité des développements. Par exemple trop de niveau d'héritage
Mineur : Risque d'impact mineur sur la productivité des développements.Par exemple: règle de nommage des variables locales.

### Notation

A : 0 bug, 0 vulnérabilité, 0,00 ≤ ratio dette technique ≤ 0,05
B : au moins 1 bug mineur, au moins 1 vulnérabilité mineur, 0,05 < ratio dette technique ≤ 0,1
C : au moins 1 bug majeur, au moins 1 vulnérabilité majeur, 0,1 < ratio dette technique ≤ 0,2
D : au moins 1 bug critique, au moins 1 vulnérabilité critique, 0,2 < ratio dette technique ≤ 0,5
E : au moins 1 bug bloquant, au moins 1 vulnérabilité bloquante, 0,5 < ratio dette technique ≤ 1

Le ratio de la dette technique est le rapport entre le coût pour remédier aux problèmes de maintenabilité 
et le coût de développement de l’application. Bornes des intervalles configuré dans l'instance

### Mesure

Couverture de code (pour Java issue de l'outil Jacoco)
La complexité cyclomatique: donne un niveau de complexité permettant de déduire le nombre de cas de tests requis pour couvrir tous les cas (à rapporter avec le nombre de tests exécutés)
La complexité cognitive est la mesure de la difficulté à comprendre l’application

## Barrière qualité (quality gate)

La barrière qualité répond à la question: mon projet est-il prêt pour une livraison?
Si oui elle peut être livré en QF , en production.

## Clean as you code

Se focaliser sur le nouveau code(ajouté ou modifié), pour prendre en compte le contexte applicatif
Moyen d'améliorer la qualité petit à petit (et ne pas régresser)

## Etape pour l'analyse SonarQube - cas avec Maven

1 - Génération d'un token à partir de son compte Sonarqube
Token personnel ou un token dédié projet

2 - Scanner maven: 
Configuration du pom.xml (notamment pour le plugin jacoco)
Commande maven minimale
mvn clean verify sonar:sonar -Dsonar.login=myAuthenticationToken
	1 Tester sur l'environnement de recette http://sonar.recette.insee.fr/ (en mode anonyme authorisé)
	2 Intégration à un pipeline

3. Gestion des branches (Philippe)
Long live branch, Short live branch

4. Lancement du pipeline (facultatif)

5. visualisation du rapport SonarQube

## Faux positif

Analyse statique du code source donc des défauts (bogue, vulnérabilité ou mauvaise pratique) peuvent être trouvés
Mais est-ce réellement un défaut?
Un faux positif est un défaut qui n'en est pas un.

Déclarer les faux positifs permet d’obtenir des métriques plus représentatif de la qualité du produit
Liste des moyens: dans le code (par exemple par //NOSONAR), via l'interface de sonarqube

## Ressource documentaire

https://docs.sonarqube.org/7.9/
Pour le scanner Maven: 
https://docs.sonarqube.org/7.9/analysis/scan/sonarscanner-for-maven/

Les paramètres de l'analyseur:
https://docs.sonarqube.org/7.9/analysis/analysis-parameters/

https://github.com/SonarSource/sonar-scanning-examples/tree/master/sonarqube-scanner-maven
Projet maven simple (sans module)

Projet multimodule (gestion de l'agrégation des rapports de la couverture de code de chaque module)
https://github.com/SonarSource/sonar-scanning-examples/tree/master/sonarqube-scanner-maven/maven-multimodule

La couverture de code de Java avec le plugin Maven Jacoco est intégré aux deux exemples
  

