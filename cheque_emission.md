# Emission d'un chèque

## Vue d'ensemble

L'émission de chèque est un moyen de paiement de dernier recours, utilisé uniquement lorsqu'un fournisseur n'accepte ni la carte bancaire ni le virement. La procédure de validation préalable est identique à celle de n'importe quel achat (voir [factures_achat.md](factures_achat.md)). Seul le trésorier est habilité à signer les chèques de Telecom Etude.

**Interlocuteurs impliqués**

- Trésorier : seul signataire du chèque, archivage, remise au bénéficiaire, mise à jour du TS
- Président / CA : validation préalable selon le montant (mêmes seuils que pour tout achat)
- VT : comptabilisation

**Outils utilisés**

- Chéquier Telecom Etude
- TS (Google Sheets) : mise à jour du suivi
- Google Drive : archivage (Drive Trésorerie > Chèques > Mandat 202X-202Y > Emis)

## Procédure pas à pas

### Etape 1 - Vérifier les conditions préalables

Avant d'émettre un chèque, s'assurer que les conditions de validation sont réunies, comme pour tout achat :

- Montant < 150 € : validation trésorier ou président
- Montant > 150 € : vote en CA, achat inscrit au budget

Se référer à [factures_achat.md](factures_achat.md) pour le détail de la procédure d'achat.

### Etape 2 - Rédiger le chèque

Remplir le chèque du carnet Telecom Etude :

- Bénéficiaire : raison sociale exacte du fournisseur
- Montant en chiffres et en lettres
- Date du jour
- Signature du trésorier

### Etape 3 - Photographier le chèque et le talon

Avant toute remise, prendre en photo :

1. Le **chèque** recto (recto complet, lisible)
2. Le **talon** correspondant dans le carnet

Ces deux photos constituent les pièces justificatives archivées.

### Etape 4 - Remettre le chèque en main propre

Le chèque est remis directement au bénéficiaire en main propre.

### Etape 5 - Nommer et archiver

Renommer les photos selon la nomenclature :

```
CHQ-NOMENCLATURE_PIECE_COMPTABLE
```

- `NOMENCLATURE_PIECE_COMPTABLE` : nomenclature de la facture d'achat associée, au format `ACH-XXX-AAMMJJ-FAC Fournisseur`

**Exemple :** `CHQ-ACH-012-260415-FAC Promocash` pour le chèque associé à la douzième facture d'achat de l'exercice, datée du 15 avril 2026.

Archiver dans Drive Trésorerie > Chèques > Mandat 202X-202Y > Emis

### Etape 6 - Mise à jour du TS

Une fois le chèque encaissé par le bénéficiaire, relever la **date comptable** figurant sur le relevé bancaire et mettre à jour le TS comme pour tout achat (voir [factures_achat.md](factures_achat.md) — Etape 6).

### Etape 7 - Transmission au VT

Informer le VT et lui transmettre les pièces archivées (facture + photos chèque et talon) pour comptabilisation.

## Points d'attention et pièges fréquents

- **Le chèque est un moyen de paiement de dernier recours.** Toujours privilégier la carte bancaire ou le virement. N'y recourir que si le fournisseur n'accepte aucun autre moyen.
- **Seul le trésorier peut signer.** Aucun autre membre n'est habilité à signer un chèque de Telecom Etude.
- **Photographier avant de remettre.** Une fois le chèque donné, il n'est plus disponible pour archivage.
- **Photographier aussi le talon.** Le talon du carnet est la seule trace physique restante une fois le chèque remis.
- **La date à saisir dans le TS est la date comptable du relevé bancaire**, pas la date d'émission ni de remise. Elle est disponible dans l'interface BNP une fois le chèque encaissé par le bénéficiaire.
- **Les conditions de validation s'appliquent comme pour tout achat.** Ne pas contourner la procédure sous prétexte que le moyen de paiement est différent.
