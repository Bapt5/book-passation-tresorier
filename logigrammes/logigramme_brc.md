# Logigramme — Déclaration BRC

> Fiche associée : [brc.md](../brc.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none
    classDef ref fill:#e8967a,color:#333,stroke:#c0502b

    START([Début du mois N+1]):::se

    subgraph GEN["🗓 Premières semaines du mois N+1"]
        direction TB
        G1{"BV émis\nsur le mois N ?"}:::dec
        G2["Générer le sheet BRC via AppScript\nMenu Déclaratif > Générer BRC\n⏱ 5 min"]:::step
        G3["Déplacer le fichier dans\nDrive > Déclaratifs > BRC+TR > AAAA-MM"]:::step
        G0["Préparer une déclaration à zéro"]:::step
        G1 -->|Oui| G2 --> G3
        G1 -->|Non| G0
    end

    subgraph CTRL["🗓 Vérification du sheet"]
        direction TB
        C1["Vérifier la Base URSSAF\n= 4 × SMIC horaire au 1er janvier"]:::step
        C2["Vérifier le taux AT\n→ lettre CARSAT ou net-entreprise.fr"]:::step
        C3["Vérifier l'assiette de cotisations\n= Base URSSAF × total JEH du mois"]:::step
        C4["Vérifier les effectifs\net les salaires arrondis"]:::step
        C5["Supprimer les lignes inutiles\n900T, 236D, 772D, 937D, 400D, 671P"]:::step
        C6["Double contrôle avec le VT\ncomptes 6226 et 431"]:::step
        C1 --> C2 --> C3 --> C4 --> C5 --> C6
    end

    subgraph DECL["🗓 Avant le 15 du mois N+1"]
        direction TB
        D1["Déclarer sur urssaf.fr\nRetranscrire le sheet case par case\n⏱ 30 min"]:::step
        D2["Valider — prélèvement automatique déclenché"]:::step
        D3["Télécharger et archiver le récapitulatif\nNomenclature : BRC-AAAA-MM"]:::step
        D4["Mettre à jour le TS\nOnglet Déclaratifs mensuels\n→ Date déclaration BRC"]:::step
        D1 --> D2 --> D3 --> D4
    end

    ERR[["📎 Erreur détectée sur un BRC passé\n→ logigramme_brc_rectification.md"]]:::ref
    FIN([BRC du mois N déclaré et archivé]):::se

    START --> GEN
    G3 --> CTRL
    G0 --> CTRL
    CTRL --> DECL --> FIN
    DECL -.->|Si erreur détectée ultérieurement| ERR
```

## ⚠️ Points sensibles

- Respecter l'échéance du 15 du mois — un retard entraîne des pénalités URSSAF
- Vérifier la Base URSSAF chaque 1er janvier — elle change avec le SMIC, une mauvaise base fausse tous les calculs de l'année
- Même sans BV sur le mois, la déclaration est obligatoire (déclaration à zéro)
- Arrondir les salaires à l'unité — jamais de centimes dans un BRC
- Supprimer les lignes inutiles (772D, 937D, 671P...) — elles ne s'appliquent pas aux JE

## ❓ Précisions

- L'assiette de cotisations des JE est dérogatoire : Base URSSAF × nombre de JEH, pas les rétributions brutes réelles
- Effectif au dernier jour : 0 si aucun BV, 1 sinon (quel que soit le nombre d'intervenants)
- Effectif rétribué : nombre d'intervenants différents ayant reçu au moins un BV sur le mois
- La colonne "Effectifs" est toujours à 0 — les intervenants JE ne sont pas des salariés
