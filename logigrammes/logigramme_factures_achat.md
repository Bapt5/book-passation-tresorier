# Logigramme — Réception et traitement des factures d'achat

> Fiche associée : [factures_achat.md](../factures_achat.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none
    classDef ref fill:#e8967a,color:#333,stroke:#c0502b

    START([Facture d'achat à traiter]):::se

    DEC_SOURCE{"Canal de réception ?"}:::dec

    subgraph MAIL["Par mail"]
        direction TB
        M1["Télécharger la facture\ndepuis la boite tresorier@telecom-etude.fr"]:::step
    end

    subgraph PLATFORM["Sur plateforme"]
        direction TB
        P1["Se connecter à la plateforme\n(Google Cloud Console, site Promocash...)\nTélécharger la facture du mois"]:::step
    end

    subgraph DIRECT["Achat direct par CB TE"]
        direction TB
        D1["Facture obtenue à l'achat\nou reçue par mail peu après\nPaiement déjà effectué"]:::step
    end

    CTRL["Contrôle de conformité\nAu nom de Telecom Etude\nAdresse 19 place Marguerite Perey 91120 Palaiseau\nDétail des taux de TVA\nNuméro TVA intracommunautaire si fournisseur étranger"]:::step

    DEC_CONF{"Facture\nconforme ?"}:::dec

    CONTACT["Contacter le fournisseur\npour obtenir une facture rectifiée\nNe pas payer avant d'avoir\nla facture conforme"]:::step

    DEC_MONTANT{"Montant\nde l'achat ?"}:::dec

    VALID_PRES["Validation trésorier\nou président"]:::step
    VALID_CA["Validation en CA\nAchat inscrit au budget obligatoire"]:::step

    DEC_PAY{"Paiement\ndéjà effectué ?"}:::dec

    VIR["Effectuer le virement\ndepuis l'interface bancaire\nConserver la preuve du virement"]:::step

    ARCHIVE["Renommer la facture\nACH-XXX-AAMMJJ-FAC Nom du fournisseur\nArchiver dans Drive Trésorerie > Achats-NDF > Achats 202X-202Y"]:::step

    TS["Mettre à jour l'onglet Factures d'achats du TS\nNomenclature, lien Drive, fournisseur, type,\nlibellé, date de pièce, montant HT, TVA,\nbudget concerné, date de paiement"]:::step

    VT["Transmettre au VT\npour contrôle, comptabilisation, archivage"]:::step

    FIN([Facture d'achat traitée et archivée]):::se

    START --> DEC_SOURCE
    DEC_SOURCE -->|Mail| MAIL --> CTRL
    DEC_SOURCE -->|Plateforme| PLATFORM --> CTRL
    DEC_SOURCE -->|CB TE| DIRECT --> CTRL
    CTRL --> DEC_CONF
    DEC_CONF -->|Non| CONTACT --> DEC_CONF
    DEC_CONF -->|Oui| DEC_MONTANT
    DEC_MONTANT -->|< 150 €| VALID_PRES --> DEC_PAY
    DEC_MONTANT -->|> 150 €| VALID_CA --> DEC_PAY
    DEC_PAY -->|Non| VIR --> ARCHIVE
    DEC_PAY -->|Oui| ARCHIVE
    ARCHIVE --> TS --> VT --> FIN
```

## ⚠️ Points sensibles

- Seul le trésorier est autorisé à utiliser la carte bancaire TE — si un membre souhaite faire un achat, il doit passer par le trésorier
- Bon de livraison ≠ facture — chez Promocash notamment, le document remis en magasin n'est pas une facture, toujours aller chercher la vraie facture sur le site
- Ne pas payer une facture non conforme — demander une facture rectifiée même si cela prend du temps
- Surveiller les montants des prélèvements automatiques — un changement de tarif peut passer inaperçu

## ❓ Précisions

- La date à retenir est la date d'émission de la facture (inscrite sur la facture), pas la date de réception ni de paiement
- Pour les prélèvements automatiques récurrents déjà inscrits au budget (Cegid, Google), la validation a eu lieu lors de l'adoption du budget — vérifier seulement que le montant prélevé correspond à l'attendu
- Traiter chaque facture dès réception pour éviter les retards de comptabilisation
