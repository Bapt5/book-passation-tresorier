# Logigramme — Emission d'un chèque

> Fiche associée : [cheque_emission.md](../cheque_emission.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none
    classDef ref fill:#e8967a,color:#333,stroke:#c0502b

    START([Fournisseur n'accepte ni CB ni virement\nChèque nécessaire en dernier recours]):::se

    VALID["Validation préalable\ncomme pour tout achat\n< 150 € → trésorier ou président\n> 150 € → vote en CA + inscription au budget"]:::step

    WRITE["Rédiger le chèque du carnet Telecom Etude\nBénéficiaire : raison sociale exacte du fournisseur\nMontant en chiffres et en lettres\nDate du jour\nSignature du trésorier (seul habilité)"]:::step

    PHOTO["Photographier avant remise :\n1. Le chèque recto complet et lisible\n2. Le talon correspondant dans le carnet"]:::step

    GIVE["Remettre le chèque\nen main propre au bénéficiaire"]:::step

    ARCHIVE["Renommer les photos\nCHQ-NOMENCLATURE_PIECE_COMPTABLE\n(ex: CHQ-ACH-012-260415-FAC Promocash)\nArchiver dans Drive Trésorerie > Chèques > Mandat 202X-202Y > Emis"]:::step

    TS["Une fois le chèque encaissé :\nRelever la date comptable sur le relevé bancaire\nMettre à jour le TS (date de paiement)\ncf. factures_achat.md Etape 6"]:::step

    VT["Transmettre au VT\nfacture + photos chèque et talon\npour comptabilisation"]:::step

    FAC_ACH[["📎 Procédure achat standard\n→ logigramme_factures_achat.md"]]:::ref
    FIN([Chèque émis et archivé]):::se

    START --> VALID --> WRITE --> PHOTO --> GIVE --> ARCHIVE --> TS --> VT --> FIN
    FIN -.-> FAC_ACH
```

## ⚠️ Points sensibles

- Le chèque est un moyen de paiement de dernier recours — toujours privilégier la carte bancaire ou le virement
- Seul le trésorier peut signer — aucun autre membre n'est habilité à signer un chèque de Telecom Etude
- Photographier avant de remettre — une fois le chèque donné, il n'est plus disponible pour archivage
- Photographier aussi le talon — c'est la seule trace physique restante une fois le chèque remis

## ❓ Précisions

- La date à saisir dans le TS est la date comptable du relevé bancaire, pas la date d'émission ni de remise
- La nomenclature du fichier archive reprend la nomenclature de la facture d'achat associée (ACH-XXX...)
