# Logigramme — Emission des bulletins de versement (BV)

> Fiche associée : [bulletins_de_versement.md](../bulletins_de_versement.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none
    classDef ref fill:#e8967a,color:#333,stroke:#c0502b

    START([Encaissement du paiement client reçu]):::se

    subgraph VERIF["🗓 Vérifications préalables"]
        direction TB
        V1{"PVRF ou PVRI signé\npar toutes les parties ?"}:::dec
        V2["Vérifier le dossier intervenant\nRM, avenants, CNI, carte étudiante,\ncarte vitale, BA"]:::step
        V3{"Dossier intervenant\ncomplet et valide ?"}:::dec
        V4["Signaler les pièces manquantes\nà l'intervenant ou au Secrétaire Général"]:::step
        V1 -->|Oui| V2 --> V3
        V3 -->|Non| V4 --> V2
    end

    subgraph PREP["🗓 Préparation du BV"]
        direction TB
        P1["Contacter l'intervenant\n→ IBAN si non renseigné\n→ Questionnaire de satisfaction"]:::step
        P2["Compléter l'onglet BV & RM du TS\nNuméro BV, JEH, montant brut,\ninfos intervenant, référence RM"]:::step
        P1 --> P2
    end

    subgraph SIGN["🗓 Surveillance des signataires"]
        direction TB
        S1{"Le trésorier\nest-il intervenant ?"}:::dec
        S2["Trésorier vire la rétribution nette\nà l'IBAN de l'intervenant"]:::step
        S3["Président vire la rétribution nette\nVT émet le BV à la place du trésorier"]:::step
        S1 -->|Non| S2
        S1 -->|Oui| S3
    end

    subgraph EMIT["🗓 Emission et transmission"]
        direction TB
        E1["Compléter le TS\nDate et référence du virement"]:::step
        E2["Générer le BV depuis le template\nVérifier les montants\nExporter en PDF\n⏱ 30 min"]:::step
        E3["Envoyer le BV PDF + tuto BNC\nà l'intervenant uniquement — RGPD\n📅 Sous 30 jours après PVRF"]:::step
        E4["Transmettre au VT\npour comptabilisation et archivage"]:::step
        E1 --> E2 --> E3 --> E4
    end

    BRC[["📎 Les cotisations calculées dans le BV\nsont déclarées mensuellement → BRC"]]:::ref
    FIN([BV émis et rétribution versée]):::se

    START --> VERIF
    V1 -->|Non| START
    V3 -->|Oui| PREP --> SIGN
    S2 --> EMIT
    S3 --> EMIT
    E4 --> BRC
    BRC --> FIN
```

## ⚠️ Points sensibles

- Ne jamais émettre un BV avant l'encaissement client — même si le PVRF est signé depuis longtemps, le BV attend le virement
- Le BV est un document RGPD — ne jamais le transmettre à quelqu'un d'autre que l'intervenant, même au chef de projet
- La numérotation XXX repart au 1er janvier, pas au 1er mai comme les factures
- Si le trésorier est intervenant : ne pas gérer son propre BV, passer la main au VT pour l'émission et au président pour le virement
- Les charges sociales ne sont pas virées à l'intervenant — elles sont calculées dans le TS et payées à l'URSSAF via le BRC mensuel

## ❓ Précisions

- Le modèle de BV est fourni chaque année par la CNJE (nouveau modèle avec taux à jour) — ne pas réutiliser un ancien modèle
- Vérifier chaque 1er janvier que la Base URSSAF (4 × SMIC horaire) et le taux AT sont à jour dans l'onglet Paramétrage du TS
- Un intervenant avec plusieurs BV sur la même étude : incrémenter le N dans la nomenclature BV-XXX-CODE_ETUDE-N
