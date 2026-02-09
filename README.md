# Exploiter une base de données relationnelle avec l’écosystème Spring (juin 2015)

Ce projet a pour objectif d’étudier et de comparer différentes architectures d’accès aux données dans une application Java basée sur l’écosystème **Spring**, en particulier **Spring JDBC** et **Spring JPA**, appliquées à une base de données relationnelle.

Le support théorique et pédagogique associé est disponible ici :  
👉 https://stahe.github.io/spring-database-juin-2015/

---

## Objectifs du projet

- Comprendre une **architecture applicative en couches**
- Comparer deux approches d’accès aux données :
  - JDBC « classique »
  - JPA (Java Persistence API)
- Mesurer et comparer les **performances** des deux solutions
- Étudier les enjeux de **portabilité entre SGBD**

---

## Architecture générale

L’application repose sur une architecture en couches, où le flux d’exécution va de gauche à droite :

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000007080000017A09403716.png)


### Rôle des couches

#### Couche UI
- Point d’entrée de l’application
- Reçoit les actions de l’utilisateur
- Affiche les résultats

#### Couche Métier
- Implémente les **règles de gestion**
- Traite les données issues :
  - de la base de données (via DAO)
  - de l’utilisateur (via UI)
- Peut renvoyer ou persister les résultats

#### Couche DAO (Data Access Object)
- Expose une **interface d’accès aux données métier**
- Masque les détails techniques d’accès à la base
- Dépend de la technologie utilisée (JDBC ou JPA)

#### Couche JDBC
- Interface standard d’accès aux bases relationnelles
- Indépendante du SGBD (via pilotes JDBC)
- Permet une bonne performance mais une portabilité limitée en pratique

---

## Évolution vers JPA

Depuis le milieu des années 2000, l’architecture peut évoluer ainsi :

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000006FE000001774C207100.png)

### Spécificités de JPA

- La couche **JPA** génère les requêtes SQL
- La couche DAO :
  - ne contient plus de SQL
  - manipule des objets persistants
- Avantages :
  - meilleure portabilité entre SGBD
  - abstraction du SQL propriétaire
- Inconvénient :
  - performances généralement inférieures à JDBC

JPA formalise des concepts introduits auparavant par des frameworks comme **Hibernate**.

---

## Comparaison JDBC vs JPA

Le projet met en œuvre **deux implémentations DAO distinctes** :

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000006FE000001774C207100.png)

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000006E10000016947159BE8.png)


### Contraintes communes

- `DAO1` et `DAO2` implémentent la **même interface `IDAO`**
- Les tests unitaires sont **identiques** pour les deux implémentations
- Objectif : comparer **fonctionnellement** et **en performance**

---

## Tests et performances

- Les tests sont réalisés via **JUnit**
- Une classe de test unique (`JUnitTestsDao`) est utilisée
- Les résultats permettent de :
  - vérifier la conformité fonctionnelle
  - comparer les temps d’exécution JDBC vs JPA

---

## Portabilité SGBD

Bien que JDBC vise une portabilité maximale :
- le SQL propriétaire
- les stratégies de génération de clés primaires
- les mots réservés spécifiques

limitent cette portabilité en pratique.

Dans ce projet, les architectures JDBC et JPA a été portée sur **six SGBD différents**, au prix de configurations spécifiques par SGBD.

---

## Conclusion

Ce projet illustre :
- les compromis entre **performance** et **abstraction**
- les choix architecturaux liés à l’accès aux données
- l’apport de Spring dans la structuration et la testabilité des applications

Il constitue un support pédagogique pour comprendre concrètement JDBC, JPA et leurs usages comparés dans une architecture Spring.

---
