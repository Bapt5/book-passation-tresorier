# Logigramme — Rectification d'une déclaration de TVA

> Fiche associée : [tva_rectification.md](../tva_rectification.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none
    classDef ref fill:#e8967a,color:#333,stroke:#c0502b

    START([Erreur détectée sur une déclaration de TVA passée]):::se

    DEC_TYPE{"Nature de l'erreur ?"}:::dec

    subgraph CAS_A["Cas a — Trop de TVA déductible déclarée"]
        direction TB
        A1["Lors de la prochaine déclaration\nRemplir la ligne 15\n'TVA antérieurement déduite à reverser'\navec le montant déduit en trop"]:::step
    end

    subgraph CAS_B["Cas b — Oubli de TVA déductible"]
        direction TB
        B1["Lors de la prochaine déclaration\nInscrire le montant omis\nen ligne 21\n'Autre TVA à déduire'"]:::step
    end

    subgraph CAS_C["Cas c — Trop de TVA collectée déclarée"]
        direction TB
        C1["Lors de la prochaine déclaration\nInscrire le montant collecté en trop\nen ligne 21\n'Autre TVA à déduire'"]:::step
    end

    subgraph CAS_D["Cas d — Oubli de TVA collectée"]
        direction TB
        D1["Lors de la prochaine déclaration\nAjouter le montant HT omis\nen ligne A1 et en ligne 8\navec la TVA collectée du mois courant"]:::step
    end

    CORR["Dans tous les cas :\nExpliquer l'erreur dans le champ\n'Correspondance' de la déclaration corrective\nNature de l'erreur, mois concerné, montant"]:::step

    CTRL["Double contrôle avec le VT\nComptes 44566, 44571, 44577"]:::step

    TVA[["📎 Procédure déclaration mensuelle\n→ logigramme_tva.md"]]:::ref
    FIN([Erreur régularisée sur la prochaine déclaration]):::se

    START --> DEC_TYPE
    DEC_TYPE -->|Trop de déductible| CAS_A --> CORR
    DEC_TYPE -->|Oubli de déductible| CAS_B --> CORR
    DEC_TYPE -->|Trop de collectée| CAS_C --> CORR
    DEC_TYPE -->|Oubli de collectée| CAS_D --> CORR
    CORR --> CTRL --> FIN
    FIN -.-> TVA
```

## ⚠️ Points sensibles

- La correction se fait toujours sur la déclaration du mois suivant — il n'y a pas de déclaration rectificative séparée
- Toujours remplir le champ correspondance — un écart inexpliqué peut poser problème lors d'un contrôle fiscal
- Les cas b et c utilisent tous les deux la ligne 21, mais dans des sens opposés — bien vérifier la cohérence de la case 28 après correction
- Ne pas attendre plusieurs mois pour régulariser une erreur identifiée

## ❓ Précisions

- Le champ correspondance sert à deux fins : tracer le contexte pour le trésorier lui-même (notamment pour expliquer l'écart lors d'un audit) et informer l'administration fiscale
- Exemple de formulation : "Régularisation d'une TVA déductible omise sur la déclaration de MM-AAAA : facture ACH-XXX non incluse, montant de TVA concerné : XX,XX €"
