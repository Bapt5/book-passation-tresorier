# Logigramme — Rectification d'un bulletin de versement

> Fiche associée : [bv_rectificatif.md](../bv_rectificatif.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none
    classDef ref fill:#e8967a,color:#333,stroke:#c0502b
    classDef ok fill:#27ae60,color:#fff,stroke:none

    START([Erreur détectée sur un BV émis]):::se

    DEC_TYPE{"Nature de l'erreur ?"}:::dec

    NOTHING["Aucune action comptable requise"]:::ok
    REPLACE["Emettre un nouveau BV\navec la mention 'annule et remplace'\n→ uniquement pour le numéro de sécu"]:::step

    subgraph MONTANT["🗓 Procédure erreur sur montant ou JEH"]
        direction TB
        M1["Emettre le BV rectificatif\navec la mention 'Rectificatif'\nNomenclature standard BV-XXX-CODE_ETUDE-N\nEnvoyer à l'intervenant — RGPD"]:::step
        M2["VT : comptabiliser l'écriture inverse\ndu BV erroné — crédit/débit inversés"]:::step
        M3["VT : comptabiliser le BV rectificatif\ncomme un BV normal"]:::step
        M4{"Différentiel de net\nsignificatif ?"}:::dec
        M5["Virer ou récupérer la différence\nComptabiliser en compte banque 512"]:::step
        M6{"TE a trop payé\net renonce ?"}:::dec
        M7["Passer en perte\n658 débit / 468 intervenant crédit"]:::step
        M8["Passer en gain\n758 crédit / 468 intervenant débit"]:::step
        M1 --> M2 --> M3 --> M4
        M4 -->|Oui| M5
        M4 -->|Non — quelques euros| M6
        M6 -->|Oui| M7
        M6 -->|Non — intervenant renonce| M8
    end

    subgraph COTIS["🗓 Gestion des cotisations sociales"]
        direction TB
        CO1{"Cotisations du BV initial\ndéjà déclarées au BRC ?"}:::dec
        CO2["Déclarer uniquement le BV rectificatif\nNe pas déclarer le BV initial"]:::step
        CO3{"BV initial de\nl'année civile précédente ?"}:::dec
        CO4["Régulariser au TR annuel\nNe pas redéclarer un BRC corrigé"]:::step
        CO5["Réaliser un TR rectificatif\npour l'année civile concernée"]:::step
        CO1 -->|Non| CO2
        CO1 -->|Oui| CO3
        CO3 -->|Non| CO4
        CO3 -->|Oui| CO5
    end

    BV[["📎 Procédure BV standard\n→ logigramme_bv.md"]]:::ref
    FIN([BV rectifié — cotisations régularisées]):::se

    START --> DEC_TYPE
    DEC_TYPE -->|Infos personnelles hors numéro de sécu| NOTHING
    DEC_TYPE -->|Numéro de sécurité sociale| REPLACE
    DEC_TYPE -->|Montant ou JEH| MONTANT
    MONTANT --> COTIS
    M5 --> COTIS
    M7 --> COTIS
    M8 --> COTIS
    COTIS --> FIN
    NOTHING --> FIN
    REPLACE --> FIN
    FIN -.-> BV
```

## ⚠️ Points sensibles

- Bien identifier la nature de l'erreur avant d'agir — une erreur sur les infos personnelles (hors numéro de sécu) ne nécessite aucune action comptable
- Le BV rectificatif porte la mention "Rectificatif", pas "annule et remplace" — cette mention est réservée aux erreurs sur le numéro de sécurité sociale
- Ne pas déclarer le BV rectificatif au BRC si le BV initial a déjà été déclaré — la régularisation se fait au TR
- Si le BV initial date de l'année civile précédente, un TR rectificatif est indispensable — ne pas l'ignorer
- Documenter le lien entre le BV erroné et le BV rectificatif dans le TS pour que le VT puisse reconstituer l'historique

## ❓ Précisions

- Les petits différentiels peuvent être passés en perte (658) ou en gain (758), mais cette décision doit être explicite et documentée
- Pour les procédures TR et TR rectificatif, consulter le [tutoriel CNJE sur Kiwi Légal](https://legal.junior-entreprises.com/knowledge-base/tableau-recapitulatif-tr/)
