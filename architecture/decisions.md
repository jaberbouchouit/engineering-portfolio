# Arbitrages techniques

Ces décisions synthétisent les systèmes décrits dans les études de cas. Elles ne constituent pas des mesures de performance ni une promesse de disponibilité.

| Sujet | Réalité observée / choix | Compromis à rendre explicite |
|---|---|---|
| Périmètre | Domaines métier et contrats avant ratios | Plus de préparation ; moins d'ambiguïté dans les résultats |
| SQLite | Utilisé par les systèmes de reporting et supply | Exploitation simple ; concurrence d'écriture et croissance à surveiller |
| PostgreSQL | Utilisé par les workflows Studio et leurs tests d'intégration | Plus de travail d'exploitation ; cohérence et migrations à organiser |
| Frontend | React/TypeScript pour analytics et Studio ; templates pour supply | Interfaces adaptées à des usages différents ; pas une pile uniforme inventée |
| Montants | Calculs déterministes et précision contrôlée | Règles d'arrondi et bases HT/TTC à définir dans chaque contrat |
| Instantanés | Sources stockées et clôtures protégées | Fraîcheur visible ; correction historique gouvernée |
| IA | Interprétation créative et commandes structurées | Sorties validées avant effet métier ou paiement |
| Intégrations | Opérations identifiées, reprises et contrôle des sources | Une API disponible ne garantit ni donnée complète ni absence de doublon |
| Déploiement | Comparaison locale/distante, copie de validation, sauvegarde | Un déploiement bloque si la fusion ou la restauration est incertaine |

## Question structurante

Avant de remplacer une technologie, identifier le problème observable : débit, concurrence, reprise, coût, délai de livraison ou capacité d'un développeur à reprendre le système. Un changement de pile n'est pas, à lui seul, un résultat métier.
