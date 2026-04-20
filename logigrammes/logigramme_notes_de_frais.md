# Logigramme — Notes de frais (NDF)

> Fiche associée : [notes_de_frais.md](../notes_de_frais.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none
    classDef ok fill:#27ae60,color:#fff,stroke:none
    classDef ref fill:#e8967a,color:#333,stroke:#c0502b

    VALID0["⚠️ Validation préalable obligatoire\nAVANT que le membre avance la dépense\n< 150 € → trésorier ou président\n> 150 € → vote en CA + budget"]:::step

    START([Réception de la demande\nvia le Google Form NDF]):::se

    CTRL["Contrôle des justificatifs\nValidation préalable obtenue\nFacture conforme au nom de TE\nPreuve du débit bancaire\nJustificatif spécifique si transport ou voiture\nRIB du membre"]:::step

    DEC_OK{"Justificatifs\ncomplets et conformes ?"}:::dec

    RETOUR["Revenir vers le membre\npour régularisation"]:::step

    DEC_REG{"Régularisable ?"}:::dec

    REFUS([NDF refusée\nExpliquer le motif au membre]):::ok

    DEC_BENEF{"Qui est\nle bénéficiaire ?"}:::dec

    subgraph SIGN_STD["Membre classique"]
        direction TB
        S1["Signataires :\nTrésorier + Président + Bénéficiaire"]:::step
    end

    subgraph SIGN_PRES["Le Président est bénéficiaire"]
        direction TB
        S2["Signataires :\nVPI + Trésorier + Bénéficiaire (Président)"]:::step
    end

    subgraph SIGN_TRES["Le Trésorier est bénéficiaire"]
        direction TB
        S3["Signataires :\nPrésident + VPI + Bénéficiaire (Trésorier)"]:::step
    end

    EDIT["Dupliquer le template GDocs NDF\nNDF-XXX-AAMMJJ-Nom fournisseur\nCompléter toutes les informations\nExporter en PDF"]:::step

    YOUSIGN["Déposer la NDF sur YouSign\nInviter les signataires dans l'ordre approprié\nMettre les justificatifs en pièces jointes"]:::step

    PAY["Une fois la NDF signée par tous :\nRéaliser le virement au bénéficiaire (montant TTC)\nEnvoyer la NDF signée au bénéficiaire"]:::step

    TS["Mettre à jour l'onglet Factures d'achats du TS\nNomenclature, lien Drive, type NDF, libellé,\ndate de pièce (date NDF pas date dépense),\nmontant HT, TVA, budget, date de paiement"]:::step

    VT["Transmettre au VT\nArchiver NDF et justificatifs\nDrive Trésorerie > Achats-NDF > NDF 202X-202Y"]:::step

    RECT[["📎 Erreur sur la NDF\n→ logigramme_ndf_rectificative.md"]]:::ref
    FIN([NDF émise, signée et archivée]):::se

    VALID0 --> START --> CTRL --> DEC_OK
    DEC_OK -->|Non| RETOUR --> DEC_REG
    DEC_REG -->|Non| REFUS
    DEC_REG -->|Oui| CTRL
    DEC_OK -->|Oui| DEC_BENEF
    DEC_BENEF -->|Classique| SIGN_STD --> EDIT
    DEC_BENEF -->|Président| SIGN_PRES --> EDIT
    DEC_BENEF -->|Trésorier| SIGN_TRES --> EDIT
    EDIT --> YOUSIGN --> PAY --> TS --> VT --> FIN
    FIN -.->|Si erreur| RECT
```

## ⚠️ Points sensibles

- Toujours valider avant l'avance — une dépense engagée sans validation préalable peut légitimement être refusée
- Ne jamais rembourser sans NDF signée — le virement intervient après la signature complète, pas avant
- Surveiller les signataires — appliquer scrupuleusement la procédure de surveillance dès que le bénéficiaire est président ou trésorier
- Pas de ticket de caisse sauf exception restaurant < 150 €

## ❓ Précisions

- La date de pièce dans le TS est la date de la NDF, pas la date de la dépense
- Si le trésorier est bénéficiaire, c'est le président qui réalise le virement
- Détailler l'objet de la NDF pour montrer le lien avec l'objet social de la JE
- La TVA est déductible uniquement si la facture est au nom de Telecom Etude avec le détail des taux
