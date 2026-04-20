# Logigramme — Suivi des créances et procédure de relance

> Fiche associée : [suivi_creances.md](../suivi_creances.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none
    classDef warn fill:#922b21,color:#fff,stroke:none

    START([Surveillance quotidienne\nde l'onglet Factures ventes du TS]):::se

    DEC0{"Facture impayée\ndépassant l'échéance ?"}:::dec
    WAIT["Continuer la surveillance\nen continu"]:::step
    DEC1{"Type de facture ?"}:::dec

    START --> DEC0
    DEC0 -->|Non| WAIT --> DEC0
    DEC0 -->|Oui| DEC1

    subgraph CLIENT["🗓 Relance — Client d'étude"]
        direction TB
        C1["J — Relance douce\nCdP contacte le client\npar téléphone / mail / courrier"]:::step
        C2["J+15 — Relance répétée\nTrésorier contacte le client\nMentionner numéro FAC, montant, échéance"]:::step
        C3["J+30 — Lettre amiable recommandée AR\nTrésorier + Président\nConserver l'accusé de réception"]:::step
        C4["J+45 — Mise en demeure\nContacter la CNJE\nNe pas improviser"]:::warn
        C1 --> C2 --> C3 --> C4
    end

    subgraph PART["🗓 Relance — Partenaire"]
        direction TB
        P1["J — Relance douce\nResponsable partenariat\npar téléphone / mail / courrier"]:::step
        P2["J+30 — Relance répétée\nResponsable partenariat"]:::step
        P3["J+60 — Lettre amiable recommandée AR\nTrésorier + Président\nConserver l'accusé de réception"]:::step
        P4["J+90 — Mise en demeure\nContacter la CNJE"]:::warn
        P1 --> P2 --> P3 --> P4
    end

    ENC["Encaissement reçu\nNoter la date de virement dans le TS\nNotifier le CdP ou resp. partenariat"]:::step
    FIN([Créance soldée]):::se

    DEC1 -->|Client d'étude| CLIENT
    DEC1 -->|Partenaire| PART
    CLIENT --> ENC
    PART --> ENC
    ENC --> FIN
```

## ⚠️ Points sensibles

- C'est le trésorier qui pilote — ne pas attendre que le CdP signale un retard
- Conserver tous les accusés de réception des lettres recommandées, indispensables en cas de contentieux
- Ne pas dépasser J+45 sans contacter la CNJE pour les clients
- Pour une facture État : ne pas décompter en jours, attendre la fin de procédure sur Chorus Pro

## ❓ Précisions

- Délais de paiement : 30 jours pour les clients d'études, 60 jours pour les partenaires — les délais de relance se calculent depuis l'échéance réelle, pas depuis la date d'émission
- Les deux premières relances partenaires sont portées par le responsable partenariat qui entretient la relation commerciale — le trésorier entre en jeu à partir de J+60
- Présenter les créances en cours au CA pour informer les membres
