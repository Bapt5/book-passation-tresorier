# Nomenclatures de fichiers

Ce document centralise toutes les conventions de nommage utilisées par le trésorier. Tout fichier produit ou archivé doit respecter ces nomenclatures pour garantir la cohérence du Drive et du TS.

## Légende des variables

| Variable | Signification | Exemple |
|---|---|---|
| `AAAA` | Année sur 4 chiffres | `2026` |
| `AA` | Année sur 2 chiffres | `26` |
| `MM` | Mois sur 2 chiffres | `04` |
| `DD` | Jour sur 2 chiffres | `15` |
| `XXX` | Numéro d'incrément sur 3 chiffres | `001`, `012` |
| `N` | Numéro court (1 ou 2 chiffres) | `1`, `2` |
| `CODE_ETUDE` | Code alphanumérique de l'étude dans le TS | `2026-042` |
| `Tiers` | Nom court lisible du tiers (client, fournisseur, intervenant...) | `BNP`, `Mailchimp` |
| `Motif` | Description courte de l'objet | `Don BDE` |

## Achats

| Document | Nomenclature | Notes |
|---|---|---|
| Facture d'achat | `ACH-XXX-AAMMDD-FAC Tiers` | XXX repart à 001 le 1er mai (exercice fiscal) |
| Reçu de don versé | `AAMMDD-DON Motif` | AAMMDD = date de versement du don |

**Exemple :** `ACH-005-260312-FAC Mailchimp`

## Notes de frais

| Document | Nomenclature | Notes |
|---|---|---|
| Note de frais (non signée) | `NDF-XXX-AAMMDD Tiers` | XXX repart à 001 le 1er mai (exercice fiscal) |
| Note de frais (signée) | `NDF-XXX-AAMMDD Tiers (signed)` | Version après signature YouSign |
| Justificatif de note de frais | `Justif-NDF-XXX-AAMMDD-N Tiers` | N = numéro du justificatif au sein de la NDF |

**Exemple :** `NDF-003-260318 Dupont` → `NDF-003-260318 Dupont (signed)` et ses justificatifs `Justif-NDF-003-260318-1 Dupont`, `Justif-NDF-003-260318-2 Dupont`...

## Bulletins de versement

| Document | Nomenclature | Notes |
|---|---|---|
| Bulletin de versement | `BV-XXX-CODE_ETUDE-N` | XXX repart à 001 le 1er janvier (année civile) |

**Exemple :** `BV-007-2026-042-1`

## Factures de vente

| Document | Nomenclature | Notes |
|---|---|---|
| Facture de vente | `FAC-XXX-CODE_ETUDE-N` | XXX ne repart jamais à 001, il est incrémental sur toute la durée de vie de l'association. |
| Facture de subvention | `FAC-XXX-ENTREPRISE` | Pour les factures émises à des entreprises dans le cadre de subventions ou partenariats. |
| Facture de refacturation | `FAC-XXX-NOM_PERSONNE_OU_ENTREPRISE` | Pour les factures émises à des individus ou entreprises identifiées dans le cadre de refacturations. |

**Exemple :** `FAC-585-225AE-01-1`

## Chèques

| Document | Nomenclature | Notes |
|---|---|---|
| Chèque reçu (photo + bordereau) | `CHQ-AAMMDD Tiers` | AAMMDD = date de dépôt en agence |
| Chèque émis (photo chèque + talon) | `CHQ-NOMENCLATURE_PIECE_COMPTABLE` | Reprend la nomenclature de la facture d'achat associée |

**Exemple réception :** `CHQ-260415 BDE Telecom Paris`

**Exemple émission :** `CHQ-ACH-012-260415-FAC Promocash`

## Déclarations fiscales et sociales

| Document | Nomenclature | Notes |
|---|---|---|
| BRC | `BRC-AAAA-MM` | Un fichier par mois |
| CARSAT (taux AT) | `CARSAT AAAA` | Lettre annuelle du taux accident du travail |
| CFE (avis) | `CFE-AAAA` | Avis de cotisation foncière |
| CFE (preuve de paiement) | `CFE-AAAA-Paiement` | |
| IS | `IS-AAAA` | Déclaration d'impôt sur les sociétés |
| TVA (déclaration) | `TVA MM-AAAA` | Ex : `TVA 03-2025` |
| TVA (accusé de réception) | `Accuse TVA MM-AAAA` | Ex : `Accuse TVA 03-2025` |
| TVA (preuve de paiement) | `Paiement TVA MM-AAAA` | Ex : `Paiement TVA 03-2025` |

## Banque

| Document | Nomenclature | Notes |
|---|---|---|
| Relevé bancaire | `RB AAAA-MM` | Un relevé par mois |
| ERB (non signé) | `ERB-AAAA-MM` | Envoyé par le VT en début de mois |
| ERB (signé) | `ERB-AAAA-MM (signed)` | Version après signature YouSign |

**Exemple :** `ERB-2026-03` → `ERB-2026-03 (signed)`
