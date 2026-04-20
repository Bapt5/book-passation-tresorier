# Logigramme — Versement d'une subvention à une association

> Fiche associée : [subvention_asso.md](../subvention_asso.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none
    classDef ok fill:#27ae60,color:#fff,stroke:none
    classDef ref fill:#e8967a,color:#333,stroke:#c0502b

    START([Subvention à une association identifiée]):::se

    subgraph COND["🗓 Vérification des conditions préalables"]
        direction TB
        C1["Subvention inscrite au budget courant\n(onglet Budget du TS)"]:::step
        C2["Vote explicite du CA acté\ndans le Compte Rendu de CA\n(montant + association mentionnés)"]:::step
        C3["Association loi 1901 de Télécom Paris\nLien démontrable avec l'objet social TE\nContrepartie concrète :\nvisibilité TE (logo, mention, événement, défi,\ncommunication WhatsApp)\nou promotion des enseignements de l'école"]:::step
        C1 --> C2 --> C3
    end

    DEC_COND{"Toutes les conditions\nsont réunies ?"}:::dec

    STOP(["Ne pas procéder\nRégulariser d'abord\nréactualisation budget en CA si nécessaire"]):::ok

    CONV["Rédiger la convention de partenariat\ndepuis le template Drive Trésorerie > Template GDocs\n> Template convention asso école\nParties, objet, montant, date de versement,\ndescription explicite de la contrepartie"]:::step

    SIGN_CONV["Mise en signature de la convention\nDeux présidents :\nPrésident Telecom Etude\n+ Président de l'association bénéficiaire"]:::step

    FAC["Réceptionner la facture de subvention\némise par l'association\n(raison sociale, montant, référence convention,\nTVA à 20 % ou mention art. 293 B CGI)"]:::step

    DEC_FAC{"Facture\nconforme ?"}:::dec

    CORRECT["Demander à l'association\nde corriger la facture\nNe pas verser avant d'avoir\nla facture conforme"]:::step

    VIR["Effectuer le virement\ndu montant vers l'IBAN de l'association\ndepuis l'interface bancaire"]:::step

    TS["Mettre à jour le TS\ncf. factures_achat.md Etape 6\nArchiver convention signée et facture\nDrive Partenariat > Partenaires Ecole/Associatifs > NOM_ASSOCIATION"]:::step

    VT["Transmettre au VT\npour comptabilisation et archivage"]:::step

    FIN([Subvention versée et archivée]):::se

    START --> COND --> DEC_COND
    DEC_COND -->|Non| STOP
    DEC_COND -->|Oui| CONV --> SIGN_CONV --> FAC --> DEC_FAC
    DEC_FAC -->|Non| CORRECT --> FAC
    DEC_FAC -->|Oui| VIR --> TS --> VT --> FIN
```

## ⚠️ Points sensibles

- Pas de versement sans vote CA explicite — une décision informelle (message, mail) ne suffit pas
- Pas de versement hors budget — si la subvention n'était pas prévue, faire d'abord une réactualisation budgétaire votée en CA
- Vérifier le lien avec l'objet social — la contrepartie doit être concrète et formulée clairement dans la convention
- La facture de l'asso est obligatoire — ne pas verser sur simple demande ou convention seule
- La convention doit précéder le versement — ne pas payer avant que les deux présidents aient signé

## ❓ Précisions

- La plupart des assos étudiantes ne sont pas assujetties à la TVA mais doivent le mentionner explicitement (art. 293 B CGI)
- Une subvention sans contrepartie claire et rattachable à l'objet social expose Telecom Etude à un risque de requalification fiscale
- Pour aller plus loin sur le cadre légal, consulter Kiwi Légal : kiwi légal — verser une subvention
