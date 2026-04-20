# Déclaration de TVA

## Vue d'ensemble

La TVA (Taxe sur la Valeur Ajoutée) est un impôt indirect collecté par Telecom Etude sur ses ventes et reversé à l'État, déduction faite de la TVA payée sur ses achats. Telecom Etude suit le régime **réel normal** avec une déclaration **mensuelle**.

- **Fréquence** : mensuelle
- **Échéance** : avant le **24 du mois suivant** la période concernée (ex : TVA de mars à déposer avant le 24 avril)
- **Où** : sur impots.gouv.fr
- **Paiement** : prélèvement automatique B2B DGFIP, **déclenché uniquement après avoir cliqué sur le bouton "Payer"** lors de la validation sur impots.gouv

> **Attention critique** : la déclaration validée sur le site ne déclenche pas automatiquement le paiement. Il faut explicitement cliquer sur le bouton "Payer" à la fin. 

**Interlocuteurs impliqués**

- Trésorier : génération via AppScript, vérification, déclaration sur impots.gouv
- VT : double contrôle avec la comptabilité (comptes 44566, 44571, 44577)

**Outils utilisés**

- TS (Google Sheets) : onglet `Déclaratifs mensuels` (suivi et lien vers le sheet généré)
- AppScript du TS : génération du sheet TVA pré-rempli
- Drive Trésorerie > Déclaratifs > TVA > Mandat 202X-202Y > AAAA-MM : archivage
- impots.gouv.fr : dépôt de la déclaration

## Principe de la TVA sur les encaissements

Telecom Etude applique le principe de la **TVA sur les encaissements** : la TVA collectée n'est pas exigible à la date de facturation, mais **le jour où l'argent est reçu sur le compte**. C'est ce qui est déclaré chaque mois.

En pratique, cela signifie que le mois M-1 à déclarer correspond :
- **TVA collectée** : TVA sur tous les virements clients et partenaires **reçus** en M-1
- **TVA déductible** : TVA sur toutes les factures d'achat **émises** (datées) en M-1

## Ce qui est soumis à TVA

### TVA collectée (ventes)

| Opération | TVA ? |
|---|---|
| Encaissement d'une facture d'étude | Oui, 20 % |
| Encaissement d'une subvention partenaire | Oui, 20 % (prestation commerciale) |
| Refacturation | Oui, 20 % |
| Subvention non commerciale (sans contrepartie) | Non (n'apparaît pas sur la déclaration) |
| Vente à un client UE assujetti à la TVA | Non (exonération, case 05) |
| Vente à un client hors UE | Non (exonération, case 05) |

### TVA déductible (achats)

| Achat | TVA déductible ? |
|---|---|
| Facture fournisseur au nom de TE | Oui, si TVA détaillée sur la facture |
| Essence (véhicule tourisme, à partir de 2022) | Oui, à hauteur de **80 %** |
| Repas dans l'intérêt de la JE | Oui si facture au nom de TE |
| Tickets de péage (dos rempli obligatoirement) | Oui |
| Billets de train / RER / bus | **Non** |
| Billets d'avion | **Non** |
| Hébergements (nuitées) | **Non** |
| Alcool | **Non** |
| Timbres | **Non** |

> La TVA n'est déductible que si la facture est **au nom de Telecom Etude**. Une facture au nom d'un membre ne permet aucune déduction.

## Les cases de la déclaration 3310-CA3

| Case | Intitulé | Ce qu'on y met |
|---|---|---|
| 01 | Ventes et prestations de services | Montant **HT** des encaissements soumis à TVA du mois |
| 08 | Autres opérations imposables | Montant HT des ventes réalisées en France + achats UE imposables |
| 05 | Autres opérations non imposables | Montant HT des opérations exonérées (clients UE/hors UE assujettis) |
| 20 | TVA déductible sur autres biens et services | Montant de la TVA déductible sur les achats du mois |
| 25 | Report de crédit de TVA | Crédit de TVA restant de la période précédente (à ne pas oublier) |
| 28 | TVA nette due | Calculée automatiquement : TVA collectée - TVA déductible - crédit reporté |

## Procédure pas à pas

### Etape 1 - Générer le sheet TVA via l'AppScript

Dans le TS, lancer l'AppScript via le menu **Déclaratif > Générer TVA pour un mois**.

Il lit les données du TS (encaissements du mois, factures d'achat) et génère un sheet pré-rempli reproduisant les cases de la déclaration.

Le sheet généré est automatiquement :
- Stocké dans Drive Trésorerie > Déclaratifs > TVA
- Lié dans la colonne correspondante de l'onglet `Déclaratifs mensuels` du TS

**Action à faire manuellement** : déplacer le fichier généré dans le bon sous-dossier Drive Trésorerie > Déclaratifs > TVA > Mandat 202X-202Y > AAAA-MM.

### Etape 2 - Vérifier le sheet généré

Contrôler chaque case avant de reporter sur le site :

- **Case 01** : croiser avec les encaissements du relevé bancaire du mois. Tous les virements clients et partenaires reçus doivent être représentés en HT.
- **Case 20** : croiser avec la somme de la TVA des factures d'achat du mois (onglet `Déclaratifs mensuels` ou liste des ACH du mois). Vérifier les cas de non-déductibilité (transports, alcool...).
- **Case 25** : reporter le crédit de TVA de la déclaration du mois précédent si applicable. **Erreur fréquente : oublier ce report.**
- **Case 28** : vérifier que le calcul automatique est cohérent.

Double contrôle avec le VT sur les comptes de TVA :

| Compte | Intitulé |
|---|---|
| 44571 | TVA facturée |
| 44577 | TVA collectée (encaissée) |
| 44566 | TVA déductible |
| 44567 | Crédit de TVA à reporter |
| 4455 | TVA à décaisser |

### Etape 3 - Déclarer sur impots.gouv.fr

Se connecter sur impots.gouv.fr avec les identifiants de la structure (voir les accès trésorerie).

Retranscrire case par case les chiffres du sheet dans le formulaire 3310-CA3 en ligne.

### Etape 4 - Archiver la déclaration

- Télécharger le récapitulatif de la déclaration au format PDF depuis impots.gouv
- Le déposer dans Drive Trésorerie > Déclaratifs > TVA > Mandat 202X-202Y > AAAA-MM
- Le nommer selon la nomenclature :

```
TVA-AAAA-MM
```

- Télécharger l'accusé de réception de la déclaration au format PDF depuis impots.gouv
- Le déposer dans le même dossier que la déclaration, avec la nomenclature suivante :

```
Accuse TVA-AAAA-MM
```

### Etape 5 - Cliquer sur "Payer"

> **Étape critique à ne pas oublier.** Une fois la déclaration validée, un bouton "Payer" apparaît. Il faut impérativement cliquer dessus pour déclencher le prélèvement automatique. Sans cette action, **la TVA n'est pas payée** même si la déclaration est soumise.

## Etape 6 - Archiver le justificatif de paiement

Après avoir cliqué sur "Payer", télécharger le justificatif de paiement au format PDF depuis impots.gouv et le déposer dans le même dossier que la déclaration, avec la nomenclature suivante :

```
Paiement TVA-AAAA-MM
```

> Demander au VT de déposer une copie du grand livre des comptes de TVA (4452 et 44577) du mois concerné dans le même dossier.

### Etape 7 - Mettre à jour le TS

Dans l'onglet `Déclaratifs mensuels`, compléter la colonne `Date déclaration TVA` pour le mois concerné.

## En cas de crédit de TVA

Si la TVA déductible dépasse la TVA collectée sur un mois, le résultat de la case 28 est un **crédit de TVA**. Ce crédit n'est pas remboursé automatiquement : il doit être reporté à la case 25 de la déclaration du mois suivant. Vérifier systématiquement la déclaration du mois précédent pour ne pas oublier ce report.

## En cas d'erreur sur une déclaration passée

Une erreur sur une déclaration TVA passée se régularise via la déclaration du mois suivant, sans dépôt d'une déclaration rectificative séparée. La procédure détaillée selon le type d'erreur (trop de déductible, oubli de collectée, etc.) est disponible dans la fiche dédiée : [tva_rectification.md](tva_rectification.md).

## Points d'attention et pièges fréquents

- **Cliquer sur "Payer" après validation.** C'est l'étape la plus critique. Sans ce clic, la TVA n'est pas prélevée et Telecom Etude est en retard de paiement.
- **Respecter l'échéance du 24 du mois.** Un retard entraîne des pénalités fiscales.
- **Ne pas oublier le report de crédit de TVA (case 25).** C'est l'erreur la plus fréquente sur la TVA.
- **TVA sur les encaissements, pas sur les factures.** Une facture émise mais non encore payée en M-1 n'entre pas dans la TVA collectée de M-1. Elle entre dans la déclaration du mois où le virement est reçu.
- **La TVA déductible suit la date de la facture d'achat**, pas la date de paiement.
- **Vérifier les cas de non-déductibilité** (transports, hébergements, alcool) avant de saisir la case 20. Une TVA non déductible saisie à tort est une erreur comptable.
- **Conserver les déclarations archivées** : elles servent de référence pour les contrôles fiscaux et pour le report de crédit d'un mois sur l'autre.
- **En cas d'erreur sur une déclaration passée** : suivre la procédure de rectification dédiée — [tva_rectification.md](tva_rectification.md).