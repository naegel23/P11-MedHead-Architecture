# MedHead — Architecture et validation du Proof of Concept

## Présentation

MedHead étudie un système d'aide à l'orientation des interventions d'urgence vers un établissement hospitalier adapté. La preuve de concept (PoC) porte sur la recherche d'hôpitaux en fonction de la localisation d'une urgence, d'une spécialité médicale et de la disponibilité simulée de lits.

Ce dépôt centralise les exigences, la stratégie de validation, les modules de solution (Solution Building Blocks), l'évaluation des principes d'architecture et les résultats du PoC.

**Code source et application :** [P11-MedHead-PoC](https://github.com/naegel23/P11-MedHead-PoC)

## Périmètre technique

| Composant | Mise en œuvre dans le PoC |
| --- | --- |
| Interface utilisateur | Vue.js 3 : formulaire de recherche et restitution des établissements |
| API REST | Java 17, Spring Boot 3 : recherche, filtrage et recommandation hospitalière |
| Données | Base H2 alimentée par un jeu de 1 290 établissements ; spécialités et lits disponibles simulés pour les tests |
| Calcul d'itinéraires | Intégration à OpenRouteService, service externe soumis à ses propres conditions d'accès et quotas |
| Contrat d'API | OpenAPI 3 via springdoc, documentation accessible par `/v3/api-docs` et `/swagger-ui/index.html` |
| Qualité et livraison | Tests automatisés backend/frontend, GitHub Actions, conteneurisation Docker et tests de charge Apache JMeter |

Le PoC correspond à **un service backend structuré en couches et une interface frontend**. Il valide un composant fonctionnel de la plateforme envisagée, et non l'ensemble de l'architecture cible distribuée.

## Livrables du PoC

Les documents disponibles dans [`PoC/`](./PoC/) constituent le dossier de validation :

1. [Exigences de la PoC](./PoC/exigence%20de%20la%20poc.pdf) — périmètre, exigences fonctionnelles et non fonctionnelles, architecture et critères de validation.
2. [Stratégie de test](./PoC/document%20de%20strategie%20de%20test.pdf) — niveaux de test, jeux de données, scénarios, outillage et méthode d'évaluation.
3. [Solution Building Blocks](./PoC/Solution%20Building%20Blocks.pdf) — composants réutilisables, interfaces, alignement architectural et travaux restants.
4. [Validation des principes d'architecture](./PoC/validation%20des%20principes%20d%27architecture.pdf) — évaluation des principes métier, techniques et méthodologiques, preuves et écarts.
5. [Reporting des résultats du PoC](./PoC/Reporting%20resultats%20PoC%20MedHead.pdf) — résultats, limites, risques résiduels et recommandations.

## Documents d'architecture et de cadrage

Le dossier [`artefacts/`](./artefacts/) rassemble les documents de référence du projet, notamment la définition de l'architecture cible, la feuille de route, l'hypothèse de développement, les principes d'architecture, les spécialités médicales NHS, le compte rendu du comité d'architecture et le *Statement of Architecture Work*.

## Résultats et limites de validation

La campagne JMeter de référence a exécuté **100 000 requêtes**, avec **100 utilisateurs virtuels**, un débit mesuré de **998,93 requêtes/s**, **0 % d'erreur**, un **P99 à 50 ms** et un **maximum de 137 ms**. Ces mesures concernent un endpoint de recherche locale **sans appel au service de routage externe**. Elles ne garantissent pas à elles seules les performances du parcours complet ni celles d'un environnement de production.

Les données utilisées sont des données de démonstration : les informations d'établissements sont documentées comme issues d'une source NHS, et les spécialités ainsi que les disponibilités en lits ont été simulées. **Elles ne représentent pas une disponibilité hospitalière réelle et actualisée.**

Les objectifs métier de taux d'orientation et de réduction de la durée de prise en charge restent à mesurer en conditions opérationnelles. Les mécanismes de sécurité, de résilience et d'intégration événementielle nécessaires à une exploitation réelle font partie des travaux à poursuivre.

## Consultation du code

Les instructions d'exécution de l'application et la configuration des composants sont disponibles dans le [dépôt de code du PoC](https://github.com/naegel23/P11-MedHead-PoC).
