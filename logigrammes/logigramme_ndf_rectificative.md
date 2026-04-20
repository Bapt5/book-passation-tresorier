# Logigramme — Rectification d'une note de frais

> Fiche associée : [ndf_rectificative.md](../ndf_rectificative.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none
    classDef ok fill:#27ae60,color:#fff,stroke:none
    classDef ref fill:#e8967a,color:#333,stroke:#c0502b

    START([Erreur détectée sur une NDF émise]):::se

    EDIT["Générer une nouvelle NDF depuis le template\nMention 'annule et remplace'\nIndication du numéro de la NDF initiale\nProchain numéro d'incrément disponible"]:::step

    SIGN["Même circuit de signature\nque pour toute NDF\n(procédure de surveillance des signataires)"]:::step

    DEC_MONTANT{"L'erreur porte-t-elle\nsur un montant ?"}:::dec

    DEC_DIFF{"Différentiel\nsignificatif ?"}:::dec

    subgraph REG_VIR["Régularisation par virement"]
        direction TB
        V1["Telecom Etude doit de l'argent :\nvirement complémentaire au membre\ncomptabiliser en compte 512"]:::step
        V2["Le membre doit de l'argent :\nlui demander de rembourser le trop-perçu\ncomptabiliser la réception en compte 512"]:::step
    end

    subgraph REG_ECR["Régularisation par écriture\n(différentiel faible)"]
        direction TB
        E1["TE a trop payé et renonce au remboursement :\ncharge de gestion courante\n658 au débit, 4681 membre au crédit"]:::step
        E2["Le membre renonce au montant dû :\nproduit de gestion courante\n758 au crédit, 4681 membre au débit"]:::step
    end

    TS["Mettre à jour l'onglet Factures d'achats du TS\nDocumenter le lien avec la NDF initiale dans le libellé"]:::step

    VT["VT comptabilise la NDF rectificative\net les écritures de régularisation\nArchive les deux NDF (initiale + rectificative)\ndans le même dossier"]:::step

    NDF[["📎 Emission d'une NDF standard\n→ logigramme_notes_de_frais.md"]]:::ref
    FIN([NDF rectifiée et archivée]):::se

    START --> EDIT --> SIGN --> DEC_MONTANT
    DEC_MONTANT -->|Non| TS
    DEC_MONTANT -->|Oui| DEC_DIFF
    DEC_DIFF -->|Significatif| REG_VIR --> TS
    DEC_DIFF -->|Faible| REG_ECR --> TS
    TS --> VT --> FIN
    FIN -.-> NDF
```

## ⚠️ Points sensibles

- "Annule et remplace" couvre tous les types d'erreurs — il n'y a pas de distinction de procédure selon la nature de l'erreur
- Les mêmes règles de surveillance des signataires s'appliquent à la NDF rectificative qu'à la NDF initiale
- Ne pas oublier de virer ou récupérer la différence si l'erreur porte sur un montant — même petite, elle doit être traitée explicitement
- Archiver les deux NDF ensemble pour que le VT puisse reconstituer l'historique

## ❓ Précisions

- Le compte du membre est le 4681, à ne pas confondre avec le 468 utilisé pour les intervenants (BV)
- La NDF rectificative prend le prochain numéro d'incrément disponible, pas le même numéro que la NDF initiale
