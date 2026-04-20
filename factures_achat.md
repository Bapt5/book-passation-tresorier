# Réception et traitement des factures d'achat

## Vue d'ensemble

Les factures d'achat correspondent à toutes les dépenses engagées par Telecom Etude auprès de fournisseurs : abonnements logiciels, achats de matériel, frais de fonctionnement, etc. Le trésorier est le seul habilité à utiliser la carte bancaire TE. C'est lui qui reçoit, valide, paie (si nécessaire). Le VT prend ensuite en charge la comptabilisation et l'archivage.

**Interlocuteurs impliqués**

- Trésorier : réception, contrôle, paiement, renommage et archivage
- Président : peut valider pour les achats < 150 €
- CA : validation obligatoire pour les achats > 150 €
- Vice trésorier⸱e (VT) : comptabilisation

**Outils utilisés**

- Boite mail `tresorier@telecom-etude.fr` : réception des factures par mail
- TS (Google Sheets) : mise à jour du suivi
- Google Drive : archivage (Drive Trésorerie > Achats-NDF > Achats 202X-202Y)

> Logigramme : [logigramme_factures_achat.md](logigrammes/logigramme_factures_achat.md)

## Sources des factures d'achat

Les factures arrivent par trois canaux distincts.

### Factures reçues par mail

Mailchimp et Cegid envoient leurs factures directement par mail à `tresorier@telecom-etude.fr`. Les achats ponctuels (matériel, services...) peuvent également arriver par mail depuis le fournisseur.

### Factures à aller chercher sur une plateforme

Certains fournisseurs ne les envoient pas automatiquement : il faut les télécharger manuellement.

| Fournisseur | Plateforme | Moyen de paiement |
|---|---|---|
| Google | [console.cloud.google.com](https://console.cloud.google.com) → Transactions | Prélèvement automatique |
| Promocash | Site Promocash (identifiants : voir les accès trésorerie) | Variable |

> **Point d'attention Promocash :** ce que Promocash remet en magasin est un **bon de livraison**, pas une facture. Une vraie facture porte toujours la mention "facture". La facture Promocash est à télécharger sur le site Promocash avec les identifiants de Telecom Etude.

### Factures issues d'un achat direct

Le trésorier est le **seul membre autorisé** à utiliser la carte bancaire TE. Lorsqu'il réalise un achat (en ligne ou en magasin), la facture est obtenue directement à l'achat ou envoyée par mail peu après. Le paiement est déjà effectué dans ce cas.

## Conformité d'une facture d'achat

Avant de traiter une facture, vérifier qu'elle est conforme. Une facture non conforme ne peut pas être payée et ne permet pas de déduire la TVA.

**Mentions obligatoires :**

- Au nom de **Telecom Etude** (pas au nom d'un membre)
- À l'adresse **19 place Marguerite Perey, 91120 Palaiseau**
- Détail des **taux de TVA** appliqués
- Numéro de TVA intracommunautaire du fournisseur **si fournisseur étranger**

Si la facture ne respecte pas ces conditions, contacter le fournisseur pour obtenir une facture rectifiée avant de procéder au paiement.


## Nomenclature et archivage

**Nomenclature :**

```
ACH-XXX-AAMMJJ-FAC Nom du fournisseur
```

- `XXX` : numérotation incrémentée depuis le 1er mai (repart à 001 chaque exercice)
- `AAMMJJ` : date d'émission de la facture (inscrite sur la facture)
- `Nom du fournisseur` : nom court et lisible

**Exemple :** `ACH-005-260312-FAC Mailchimp` pour la cinquième facture d'achat de l'exercice, datée du 12 mars 2026.

**Archivage :** Drive Trésorerie > Achats-NDF > Achats 202X-202Y

## Validation des achats

La validation doit toujours intervenir **avant** le paiement.

| Montant | Validation requise |
|---|---|
| < 150 € | Trésorier + Président |
| > 150 € | CA (présence au budget obligatoire) |

En pratique, l'objectif est de **tout budgétiser en amont** lors de la construction du budget annuel. Le validation trésorier ou président est réservé aux urgences ou aux achats non anticipés. 

## Procédure pas à pas

### Etape 1 - Réception et identification de la facture

Selon le canal :

- **Mail** : la facture arrive directement dans la boite trésorier. La télécharger.
- **Plateforme (Google, Promocash)** : se connecter à la plateforme et télécharger la facture du mois ou de la période concernée.
- **Achat direct** : la facture est obtenue à l'achat ou reçue par mail peu après.

### Etape 2 - Contrôle de conformité

Vérifier que la facture est conforme aux mentions obligatoires listées ci-dessus. Si ce n'est pas le cas, contacter le fournisseur avant d'aller plus loin.

### Etape 3 - Validation

S'assurer que l'achat a bien été validé par le trésorier ou président (ou en CA si > 150 €) **avant** le paiement. Pour les prélèvements automatiques récurrents (Cegid, Google) déjà inscrits au budget, la validation a eu lieu lors de l'adoption du budget : pas de revalidation nécessaire à chaque échéance, mais vérifier que le montant prélevé correspond à ce qui était attendu.

### Etape 4 - Paiement (si non encore effectué)

Si le paiement n'a pas encore eu lieu (achat à régler par virement) :

1. Effectuer le virement depuis l'interface bancaire
2. Conserver la preuve du virement

Si le paiement a déjà eu lieu (achat par CB TE ou prélèvement automatique), passer directement à l'étape suivante.

### Etape 5 - Renommage et archivage

1. Renommer la facture selon la nomenclature `ACH-XXX-AAMMJJ-FAC Nom du fournisseur`
2. Déposer dans Drive Trésorerie > Achats-NDF > Achats 202X-202Y

### Etape 6 - Mise à jour du TS

Mettre à jour l'onglet `Factures d'achats` du TS :
* Nomenclature de la facture
* Lien vers la facture dans le Drive
* Fournisseur (à ajouter dans l'onglet `Fournisseurs` si nouveau)
* Type : `Facture fournisseur` ou `Facture de subvention` selon le cas
* Type d'achats : `Service` ou `Bien` (sert pour la déclaration de TVA, `Service` par défaut, `Bien` pour les achats de matériel)
* Libellé : description courte de la dépense
* Date de pièce : date d'émission de la facture
* Montant HT, taux de TVA
* Budget concerné
* Date de paiement (date du virement ou date de prélèvement ou date de paiement par CB)

### Etape 7 - Transmission au VT

Le VT contrôle, comptabilise et archive la facture. La déposer dans le Drive Trésorerie > Achats-NDF > Achats 202X-202Y.

Le VT la range ensuite dans le dossier du mois d'émission.

## Points d'attention et pièges fréquents

- **Seul le trésorier est autorisé à utiliser la carte bancaire TE.** Si un membre souhaite faire un achat, il doit en informer le trésorier qui paie directement en venant pour l'achat. 
- **Bon de livraison ≠ facture.** Chez Promocash notamment, le document remis en magasin n'est pas une facture. Toujours aller chercher la vraie facture sur le site.
- **La date à retenir est celle d'émission**, pas de réception ni de paiement. C'est cette date qui sert pour la mise à jour du TS et la comptabilisation.
- **Ne pas payer une facture non conforme.** Demander une facture rectifiée même si cela prend du temps.
- **Surveiller les montants des prélèvements automatiques.** Un changement de tarif (Cegid, Google) peut passer inaperçu si on ne compare pas le montant prélevé avec ce qui était prévu au budget.
- **Ne pas accumuler les factures à traiter.** Traiter chaque facture dès réception pour éviter les retards de comptabilisation et les oublis de paiement.
