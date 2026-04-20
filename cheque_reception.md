# Réception d'un chèque

## Vue d'ensemble

La réception de chèques est rare à Telecom Etude. Lorsqu'un tiers (client, partenaire, association...) règle par chèque, celui-ci est remis en main propre ou envoyé au siège social. Le trésorier prend en charge la réception, l'archivage et le dépôt en agence. La date retenue pour le TS est la date comptable figurant sur le relevé bancaire, non la date de réception.

**Interlocuteurs impliqués**

- Trésorier : réception du chèque, archivage, dépôt en banque, mise à jour du TS
- VT : comptabilisation après dépôt

**Outils utilisés**

- Bordereau de remise de chèque (à récupérer en agence BNP)
- TS (Google Sheets) : mise à jour du suivi
- Google Drive : archivage (Drive Trésorerie > Chèques > Mandat 202X-202Y > Reçus)

> Logigramme : [logigramme_cheque_reception.md](logigrammes/logigramme_cheque_reception.md)

## Procédure pas à pas

### Etape 1 - Réceptionner le chèque

Le chèque est remis en main propre ou reçu au siège social de Telecom Etude (19 place Marguerite Perey, 91120 Palaiseau). S'assurer que le chèque est bien libellé à l'ordre de **Telecom Etude** et que le montant correspond à ce qui était attendu.

### Etape 2 - Photographier le chèque

Avant tout dépôt, prendre une photo lisible du chèque recto. Cette photo constitue la pièce justificative archivée.

### Etape 3 - Déposer en agence

Se rendre en agence BNP avec le chèque et remplir un **bordereau de remise de chèque**. Déposer le chèque et récupérer la copie du bordereau.

Prendre en photo le bordereau.

### Etape 4 - Nommer et archiver

Renommer les deux photos selon la nomenclature :

```
CHQ-AAMMJJ Tiers
```

- `AAMMJJ` : date du dépôt en agence
- `Tiers` : nom court du tiers émetteur du chèque

**Exemple :** `CHQ-260415 BDE Telecom Paris` pour un chèque du BDE déposé le 15 avril 2026.

Archiver dans Drive Trésorerie > Chèques > Mandat 202X-202Y > Reçus

### Etape 5 - Mise à jour du TS

Une fois le chèque encaissé, relever la **date comptable** figurant sur le relevé bancaire et mettre à jour le TS en conséquence (encaissement de la facture concernée).

### Etape 6 - Transmission au VT

Informer le VT du dépôt et lui transmettre les pièces archivées pour comptabilisation.

## Points d'attention et pièges fréquents

- **La date à saisir dans le TS est la date comptable du relevé bancaire**, pas la date de réception ni la date de dépôt. Elle est disponible dans l'interface BNP quelques jours après le dépôt.
- **Photographier le chèque avant de le déposer.** Une fois remis en agence, il n'est plus récupérable.
- **Vérifier que le chèque est à l'ordre de Telecom Etude.** Un chèque libellé à un autre nom ne peut pas être déposé sur le compte.
- **Ne pas 