# Logigramme — Emission de factures clients

> Fiche associée : [factures_clients.md](../factures_clients.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none
    classDef ref fill:#e8967a,color:#333,stroke:#c0502b

    START([Notification de mise en signature\nCE ou BC reçue sur YouSign]):::se

    subgraph PREP["🗓 Dès mise en signature — avant même la signature"]
        direction TB
        P1["Créer la ligne de l'étude dans\nl'onglet Suivi des études du TS\nsi elle n'existe pas"]:::step
        P2["Générer le sheet de facturation\ndepuis le TS — Menu Suivi d'étude"]:::step
        P3["Compléter le sheet de facturation\nRaison sociale, SIRET, adresse,\nmontant HT, répartition par phases"]:::step
        P1 --> P2 --> P3
    end

    SIGN([Notification YouSign — document signé]):::se

    DEC_TYPE{"Type de document signé ?"}:::dec

    subgraph ACOMPTE["Facture d'acompte — après CE ou BC"]
        direction TB
        FA["Générer la facture d'acompte\ndepuis l'onglet Facture du sheet\n30 à 50 % du total — recommandée"]:::step
    end

    subgraph INTER["Facture intermédiaire — après PVRI"]
        direction TB
        FI["Générer la facture intermédiaire\ndepuis l'onglet Facture du sheet\nFacture les phases validées"]:::step
    end

    subgraph SOLDE["Facture de solde — après PVRF"]
        direction TB
        FS["Générer la facture de solde\ndepuis l'onglet Facture du sheet\nSolde le montant restant"]:::step
    end

    subgraph VERIF["🗓 Vérification et envoi"]
        direction TB
        V1["Vérifier les mentions légales\net les montants\nExporter en PDF"]:::step
        V2["CdP envoie la facture au client\ntresorier@telecom-etude.fr en copie"]:::step
        V3["Mettre à jour l'onglet Factures ventes du TS\nNuméro, client, type, lien Drive,\ndate émission, date échéance — 30 jours"]:::step
        V4["Transmettre au VT\npour contrôle, comptabilisation, archivage"]:::step
        V1 --> V2 --> V3 --> V4
    end

    CREANCES[["📎 Suivi du paiement\n→ logigramme_suivi_creances.md"]]:::ref
    RECT[["📎 Erreur sur la facture\n→ logigramme_factures_rectification.md"]]:::ref
    BV[["📎 Encaissement reçu → émission BV\n→ logigramme_bv.md"]]:::ref
    FIN([Facture émise et archivée]):::se

    START --> PREP --> SIGN --> DEC_TYPE
    DEC_TYPE -->|CE ou BC| ACOMPTE --> VERIF
    DEC_TYPE -->|PVRI| INTER --> VERIF
    DEC_TYPE -->|PVRF| SOLDE --> VERIF
    VERIF --> FIN
    FIN --> CREANCES
    FIN -.->|Si erreur| RECT
    FIN -.->|Paiement reçu| BV
```

## ⚠️ Points sensibles

- Ne pas émettre une facture avant que tous les signataires aient signé le document déclencheur
- Remplir le sheet de facturation dès la mise en signature de la CE — ne pas attendre la signature effective
- Mettre à jour le sheet à chaque avenant, même si seule la nomenclature change
- Vérifier le SIRET — une facture avec un SIRET erroné est non conforme
- Toujours être en copie de l'envoi pour assurer le suivi de réception

## ❓ Précisions

- La facture d'acompte ne permet pas de rétribuer un intervenant — attendre la facture intermédiaire ou de solde
- Délai de paiement : 30 jours date de facture pour les clients standard (vérifier les conditions générales en cas de doute)
- TVA toujours à 20 % pour les clients français, sans exception
- Pour les avoirs et les factures clients étrangers : ne pas improviser, consulter Kiwi Légal ou la CNJE
