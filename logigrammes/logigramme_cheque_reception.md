# Logigramme — Réception d'un chèque

> Fiche associée : [cheque_reception.md](../cheque_reception.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none
    classDef ref fill:#e8967a,color:#333,stroke:#c0502b

    START([Chèque reçu en main propre\nou au siège — 19 place Marguerite Perey]):::se

    VERIF["Vérifier que le chèque est libellé\nà l'ordre de Telecom Etude\net que le montant correspond à l'attendu"]:::step

    PHOTO1["Photographier le chèque recto\navant tout dépôt\n(pièce justificative archivée)"]:::step

    DEPOT["Se rendre en agence BNP\nRemplir le bordereau de remise de chèque\nDéposer le chèque et récupérer la copie du bordereau"]:::step

    PHOTO2["Photographier le bordereau"]:::step

    ARCHIVE["Renommer les deux photos\nCHQ-AAMMJJ Tiers\n(AAMMJJ = date du dépôt en agence)\nArchiver dans Drive Trésorerie > Chèques > Mandat 202X-202Y > Reçus"]:::step

    TS["Relever la date comptable\nsur le relevé bancaire BNP\n(disponible quelques jours après le dépôt)\nMettre à jour le TS en conséquence"]:::step

    VT["Informer le VT du dépôt\nLui transmettre les pièces archivées\npour comptabilisation"]:::step

    CREANCES[["📎 Suivi du paiement associé\n→ logigramme_suivi_creances.md"]]:::ref
    FIN([Chèque déposé et archivé]):::se

    START --> VERIF --> PHOTO1 --> DEPOT --> PHOTO2 --> ARCHIVE --> TS --> VT --> FIN
    FIN -.-> CREANCES
```

## ⚠️ Points sensibles

- Photographier le chèque avant de le déposer — une fois remis en agence, il n'est plus récupérable
- Vérifier que le chèque est libellé à l'ordre de Telecom Etude — un chèque à un autre nom ne peut pas être déposé
- La date à saisir dans le TS est la date comptable du relevé bancaire, pas la date de réception ni la date de dépôt

## ❓ Précisions

- La date comptable est disponible dans l'interface BNP quelques jours après le dépôt en agence
- La nomenclature CHQ-AAMMJJ Tiers s'applique aux deux photos (chèque et bordereau)
- Les chèques sont rares à Telecom Etude — en cas de doute sur la procédure, consulter le VT
