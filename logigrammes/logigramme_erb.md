# Logigramme — Signature de l'ERB

> Fiche associée : [erb.md](../erb.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none

    START([Début du mois N+1]):::se

    subgraph PROD["🗓 Début de mois — production VT"]
        direction TB
        A1["VT produit l'ERB dans Cegid Loop\net joint le relevé bancaire BNP\net le grand livre du compte 51240000"]:::step
        A2["Trésorier dépose l'ERB sur YouSign\npour mise en signature"]:::step
        A1 --> A2
    end

    subgraph VERIF["🗓 Vérification — trésorier"]
        direction TB
        V1["Vérifier l'écart de rapprochement\n→ doit être 0,00 €"]:::step
        V2["Vérifier la cohérence des soldes\n→ solde relevé BNP = solde ERB"]:::step
        V3["Croiser chaque opération du relevé BNP\navec le grand livre\n⏱ 10-20 min"]:::step
        V4["Vérifier les libellés du grand livre\n→ respect des nomenclatures"]:::step
        V5["Vérifier l'absence d'opérations anormales"]:::step
        V6{"Anomalie détectée ?"}:::dec
        V1 --> V2 --> V3 --> V4 --> V5 --> V6
    end

    CORR["Contacter le VT\npour correction"]:::step

    subgraph SIGN["🗓 Signature et clôture"]
        direction TB
        S1["Signer l'ERB via YouSign\n+ cosignature président"]:::step
        S2["Mettre à jour le TS\nColonne 'Date signature ERB'\nde l'onglet Déclaratifs mensuels"]:::step
        S1 --> S2
    end

    FIN([ERB du mois N signé et archivé]):::se

    START --> PROD --> VERIF
    V6 -->|Oui| CORR --> V1
    V6 -->|Non| SIGN --> FIN
```

## ⚠️ Points sensibles

- Ne jamais signer si l'écart de rapprochement n'est pas à 0,00 € — même un faible écart signifie une opération manquante ou incorrecte
- Le contrôle n'est pas une formalité — le trésorier engage sa responsabilité en cosignant
- L'ERB porte sur le mois N-1 — ne pas confondre les périodes
- Vérifier les soldes de départ : le solde initial du grand livre doit correspondre au solde final de l'ERB du mois précédent

## ❓ Précisions

- L'ERB se compose de 3 parties : l'ERB Loop, le relevé BNP, le grand livre du compte 51240000
- Exemples de correspondances attendues : un virement FAC-XXX dans le relevé doit apparaître avec la même référence et le même montant dans le grand livre ; un prélèvement URSSAF doit correspondre à une écriture "URSSAF Mois AAAA" ; un paiement CB Mailchimp doit correspondre à une écriture ACH-XXX-Mailchimp
