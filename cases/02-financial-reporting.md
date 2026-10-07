# Reporting financier — une clôture qu'on peut expliquer

## Besoin métier

Construire des exports de ventes exploitables par la finance, en distinguant encaissement, expédition, remboursement et période de clôture. Deux fichiers peuvent avoir le même total tout en contenant des commandes différentes : un contrôle de somme seul est insuffisant.

## Architecture

Connecteurs et données stockées alimentent des calculs Python déterministes, des instantanés et des exports. Une API FastAPI sert le dashboard React/TypeScript ; les traitements récurrents génèrent les fichiers et les notifications. Les règles de population sont versionnées avec des tables de décision.

```mermaid
flowchart LR
    A[Données e-commerce stockées] --> B[Population et période explicites]
    B --> C[Calculs et ventilation]
    C --> D[Rapprochement ligne par ligne]
    D --> E[Instantané de clôture]
    E --> F[Export / dashboard]
    E --> G[Historique protégé]
```

## Décisions qui changent la fiabilité

- **Distinguer les axes de temps.** Une commande payée en fin de mois et expédiée au mois suivant n'appartient pas aux mêmes périodes selon l'axe retenu. Le contrat précise aussi les événements absents.
- **Conserver les flux.** Un remboursement ultérieur ne supprime pas la trace de l'encaissement initial.
- **Geler une clôture seulement quand elle est complète.** Une ventilation manquante bloque le gel ; une correction d'un mois clos demande une décision explicite.
- **Refuser les faux zéros.** Une source marketing en erreur reste indisponible. Les ratios partiels sont étiquetés ou masqués selon la règle approuvée.
- **Nommer les indicateurs selon leur périmètre.** Un résultat sans tous les postes comptables ne devient pas une marge nette par changement de libellé.

## Vérifications et résultat technique

Les preuves décrivent des tests de décision, des rapprochements par commande et par composante, ainsi que des générations sur copie avant publication. Les flux mensuels et quotidiens sont déployés ; une partie des exports historiques a une validation utilisateur documentée.

La clôture devient reconstructible depuis ses règles, sa population et son instantané. Aucun gain financier ou temps économisé n'est chiffré dans cette étude faute de mesure publiée.

## Limites

Les états de validation diffèrent selon la marque et la fonction. L'acceptation d'un email par SMTP ne prouve pas sa lecture ni sa remise en boîte. Certaines dépenses restent déclarées manuellement ; les postes comptables manquants ne sont pas estimés pour compléter un résultat.

Le démonstrateur [business-metrics-contracts](https://github.com/jaberbouchouit/business-metrics-contracts) illustre un contrat simplifié indépendant. Il ne reproduit pas les règles financières privées de production.
