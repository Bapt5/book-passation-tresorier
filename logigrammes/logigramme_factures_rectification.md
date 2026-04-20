# Logigramme — Rectification d'une facture émise

> Fiche associée : [factures_rectification.md](../factures_rectification.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none
    classDef ok fill:#27ae60,color:#fff,stroke:none
    classDef ref fill:#e8967a,color:#333,stroke:#c0502b

    START([Erreur détectée sur une facture émise]):::se

    DEC_ENVOI{"La facture a-t-elle\ndéjà été envoyée\nau tiers ?"}:::dec

    subgraph CAS1["Cas 1 — Facture non envoyée"]
        direction TB
        A1["Modifier directement\nle Google Docs de la facture"]:::step
        A2["Corriger l'écriture dans Cegid Loop\nsi elle a déjà été saisie"]:::step
        A1 --> A2
    end

    DEC_MONTANT{"L'erreur porte-t-elle\nsur un montant ?"}:::dec

    subgraph CAS2["Cas 2 — Envoyée, erreur sans impact montant"]
        direction TB
        B1["Corriger la facture dans le GDocs\nen conservant le même numéro d'incrément"]:::step
        B2["Mentionner 'annule et remplace'\nla version précédente"]:::step
        B3["Envoyer la version corrigée au tiers\nen précisant que les montants sont inchangés"]:::step
        B1 --> B2 --> B3
    end

    subgraph CAS3["Cas 3 — Envoyée, erreur sur le montant"]
        direction TB
        C1["Emettre une facture d'avoir\nqui neutralise la facture initiale\n(montants en négatif, référence à la facture initiale)"]:::step
        C2["Emettre une nouvelle facture corrigée\navec le bon montant\nau prochain numéro d'incrément disponible"]:::step
        C3["Envoyer les deux documents au tiers"]:::step
        DEC_PAY{"Le tiers a-t-il déjà\npayé la facture\ninitiale ?"}:::dec
        C4["Rembourser la différence\npar virement sortant classique"]:::step
        C5["VT comptabilise l'avoir\net la nouvelle facture\nCorrige les écritures dans Cegid Loop"]:::step
        C1 --> C2 --> C3 --> DEC_PAY
        DEC_PAY -->|Oui| C4 --> C5
        DEC_PAY -->|Non| C5
    end

    FAC_CLI[["📎 Emission de factures clients\n→ logigramme_factures_clients.md"]]:::ref
    FIN([Facture rectifiée et archivée]):::se

    START --> DEC_ENVOI
    DEC_ENVOI -->|Non| CAS1 --> FIN
    DEC_ENVOI -->|Oui| DEC_MONTANT
    DEC_MONTANT -->|Non| CAS2 --> FIN
    DEC_MONTANT -->|Oui| CAS3 --> FIN
    FIN -.-> FAC_CLI
```

## ⚠️ Points sensibles

- Ne jamais supprimer une facture envoyée — une fois transmise au tiers, elle doit être neutralisée par un avoir, jamais effacée
- Une erreur dans le BC ou la CE ne se corrige pas par un avoir — le contrat signé fait foi, c'est un sujet juridique à traiter avec le VPO ou le CdP
- Après signature du PVRF, un avoir ne modifie pas les JEH — il ne porte que sur les montants en euros de la facture

## ❓ Précisions

- La facture d'avoir doit comporter : le terme "avoir" dans le titre, la référence à la facture initiale, la mention "net à déduire" au lieu de "net à payer", les montants en négatif, et les modalités de remboursement si applicable
- La nomenclature de l'avoir suit le format standard avec le prochain numéro d'incrément disponible
- Pour plus de détails, consulter le tutoriel CNJE sur Kiwi Légal : Rectification de facture
