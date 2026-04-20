# Logigramme — Suivi et réactualisation du budget

> Fiche associée : [budget.md](../budget.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none

    START([Début de mandat — mai]):::se

    subgraph DEBUT["🗓 Début de mandat"]
        direction TB
        A1["Participer à l'exercice budget du RFP\navec le trésorier sortant"]:::step
        A2["Construire le budget prévisionnel\n3 scénarios : bas / moyen / haut\nAvec le président et les respos de pôle\n⏱ 1-2 semaines"]:::step
        A3["Faire voter le budget initial en CA"]:::step
        A1 --> A2 --> A3
    end

    subgraph MENSUEL["🗓 En cours de mandat — mensuel"]
        direction TB
        B1["Surveiller l'onglet Budget du TS\nVérifier le réalisé vs prévisionnel\nen continu"]:::step
        B2["Présenter le réalisé au CA\n📅 1 fois par mois"]:::step
        B3{"Réalisé significativement\nécarté du prévisionnel ?"}:::dec
        B1 --> B2 --> B3
    end

    subgraph REACTU["🗓 Réactualisation — si nécessaire"]
        direction TB
        C1["Calculer le réalisé à date\ndepuis l'onglet Budget du TS"]:::step
        C2["Consulter le président et les respos de pôle\nsur les prévisions restantes"]:::step
        C3["Mettre à jour les 3 scénarios\nArchiver l'ancienne version"]:::step
        C4["Présenter et faire voter\nle budget réactualisé en CA"]:::step
        C1 --> C2 --> C3 --> C4
    end

    FIN([Fin de mandat — Atterrissage budgétaire]):::se

    START --> DEBUT --> MENSUEL
    B3 -->|Non — tous les 2-3 mois| B1
    B3 -->|Oui| REACTU
    C4 --> B1
    B1 -.->|Fin de mandat| FIN
```

## ⚠️ Points sensibles

- Budget en HT — ne jamais saisir du TTC
- Archiver chaque version réactualisée pour garder l'historique des décisions
- Impliquer les respos de pôle — un budget sans eux sera contesté ou ignoré
- Ne pas attendre une dérive importante pour réactualiser
- Le résultat visé est une contrainte sauf décision explicite du CA de le réviser

## ❓ Précisions

- Le réalisé se met à jour automatiquement dans l'onglet Budget du TS
- Les prévisions restent à réviser manuellement lors des réactualisations
- Impliquer le trésorier entrant ET sortant lors de la construction initiale (retours sur les enjeux budgétaires de chaque pôle)
