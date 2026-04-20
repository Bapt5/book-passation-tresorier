# Logigramme — Refacturation

> Fiche associée : [refacturation.md](../refacturation.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none
    classDef ref fill:#e8967a,color:#333,stroke:#c0502b

    START([Trésorier constate une dépense avancée\npour le compte d'un tiers]):::se

    DEC_TYPE{"Type de\nrefacturation ?"}:::dec

    subgraph FRAIS_ETUDE["Frais d'étude hors CE"]
        direction TB
        F1["Vérifier que la validation préalable\ndu client a bien été obtenue\net que les justificatifs sont disponibles"]:::step
    end

    subgraph AUTRES["Autres refacturations\n(congrès, places, etc.)"]
        direction TB
        O1["Vérifier que la dépense est\njustifiée et traçable\n(facture fournisseur, reçu, relevé)"]:::step
    end

    ID["Identifier l'identité exacte\net les coordonnées de facturation\ndu destinataire"]:::step

    subgraph EDIT["🗓 Edition de la facture"]
        direction TB
        E1["Dupliquer le template GDocs\nrefacturation depuis\nDrive Trésorerie > Template GDocs"]:::step
        E2["Renommer selon la nomenclature\nFAC-XXX-NOM_PERSONNE_OU_ENTREPRISE"]:::step
        E3["Compléter : nom et adresse destinataire,\nSIRET si entreprise, numéro de facture,\ndates émission et échéance,\nobjet précis avec référence justificatif,\nmontant HT, TVA (taux de la dépense avancée), TTC"]:::step
        E4["Vérifier les mentions légales\nen-tête TE, mention TVA encaissements,\nmodalités de paiement, escompte"]:::step
        E5["Joindre les justificatifs si pertinent\nExporter la facture au format PDF"]:::step
        E1 --> E2 --> E3 --> E4 --> E5
    end

    SEND["Trésorier envoie directement\nla facture au destinataire\ndepuis tresorier@telecom-etude.fr"]:::step

    TS["Mettre à jour l'onglet Factures ventes du TS\nNuméro, destinataire, type Refac Client ou Refac Etudiant,\nlien Drive, dates, montant HT,\nTVA si différent de 20 %"]:::step

    VT["Transmettre au VT\npour contrôle, comptabilisation, archivage\nDrive Trésorerie > Ventes (Factures) > Mandat 202X-202Y"]:::step

    CREANCES[["📎 Suivi du paiement\n→ logigramme_suivi_creances.md"]]:::ref
    FIN([Refacturation émise et archivée]):::se

    START --> DEC_TYPE
    DEC_TYPE -->|Frais étude hors CE| FRAIS_ETUDE --> ID
    DEC_TYPE -->|Autre| AUTRES --> ID
    ID --> EDIT --> SEND --> TS --> VT --> FIN
    FIN --> CREANCES
```

## ⚠️ Points sensibles

- Pour les frais d'étude hors CE, ne jamais refacturer sans validation préalable écrite du client — la base légale est dans les conditions générales d'étude
- La TVA est au taux de la dépense avancée, pas nécessairement 20 % — vérifier le justificatif
- Ne pas oublier de facturer — surveiller activement les dépenses avancées pour ne pas laisser passer une refacturation
- Toujours conserver les justificatifs de la dépense avancée en cas de contrôle ou de contestation

## ❓ Précisions

- C'est le trésorier qui envoie directement la facture (contrairement aux factures d'étude envoyées par le CdP)
- Si le destinataire est un particulier, il ne pourra pas déduire la TVA, mais celle-ci reste obligatoire
- La numérotation globale est partagée avec toutes les autres factures
