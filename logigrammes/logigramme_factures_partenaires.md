# Logigramme — Emission de factures partenaires

> Fiche associée : [factures_partenaires.md](../factures_partenaires.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none
    classDef ref fill:#e8967a,color:#333,stroke:#c0502b

    START([Subvention partenaire prévue au budget\nou cloture comptable approche]):::se

    subgraph RELANCE["🗓 Proactivité — avant toute demande"]
        direction TB
        R1["Si la facture n'est pas encore émise\net que la cloture approche\nRelancer le responsable du partenariat"]:::step
    end

    REC["Réception de la demande du responsable\nContrat de partenariat, montant HT,\ncoordonnées de facturation (raison sociale, adresse, SIRET)"]:::step

    DEC_INFO{"Informations\ncomplètes ?"}:::dec

    DEMAND["Demander les informations\nmanquantes avant de procéder"]:::step

    subgraph EDIT["🗓 Edition de la facture"]
        direction TB
        E1["Dupliquer le template GDocs\nfacture subvention depuis\nDrive Trésorerie > Template GDocs"]:::step
        E2["Renommer selon la nomenclature\nFAC-XXX-NOM_PARTENAIRE"]:::step
        E3["Compléter : raison sociale, SIRET,\nnum de facture, date émission,\ndate échéance J+60, objet (reprendre\nformulation du contrat), montant HT,\nTVA 20 %, total TTC"]:::step
        E4["Vérifier les mentions légales\nen-tête TE, mention TVA encaissements,\nmodalités de paiement, escompte"]:::step
        E5["Exporter la facture au format PDF"]:::step
        E1 --> E2 --> E3 --> E4 --> E5
    end

    SEND["Responsable du partenariat\nenvoie la facture au partenaire\ntresorier@telecom-etude.fr en copie"]:::step

    TS["Mettre à jour l'onglet Factures ventes du TS\nNuméro, partenaire, type Subvention C,\nlien Drive, date émission, date échéance J+60, montant HT"]:::step

    VT["Transmettre au VT\npour contrôle, comptabilisation, archivage\nDrive Trésorerie > Ventes (Factures) > Mandat 202X-202Y"]:::step

    CREANCES[["📎 Suivi du paiement\n→ logigramme_suivi_creances.md"]]:::ref
    RECT[["📎 Erreur sur la facture\n→ logigramme_factures_rectification.md"]]:::ref
    FIN([Facture partenaire émise et archivée]):::se

    START --> RELANCE --> REC --> DEC_INFO
    DEC_INFO -->|Non| DEMAND --> REC
    DEC_INFO -->|Oui| EDIT --> SEND --> TS --> VT --> FIN
    FIN --> CREANCES
    FIN -.->|Si erreur| RECT
```

## ⚠️ Points sensibles

- Ne pas attendre que le responsable du partenariat prenne l'initiative — si la cloture approche, relancer proactivement
- Toujours vérifier les coordonnées du partenaire, même pour les partenaires récurrents (elles peuvent changer d'une année sur l'autre)
- Le délai de paiement est de 60 jours, pas 30 — ne pas paramétrer la mauvaise date d'échéance
- Ne pas oublier la TVA à 20 % — les subventions partenaires sont des prestations commerciales, pas des dons
- Toujours être en copie de l'envoi pour assurer le suivi de réception

## ❓ Précisions

- La numérotation globale est partagée avec les factures d'étude — ne pas réinitialiser le compteur
- Pour BearingPoint, l'adresse d'envoi spécifique est supplierinvoice@bearingpoint.com
- En cas d'erreur sur une facture déjà émise, suivre la procédure de rectification dédiée
