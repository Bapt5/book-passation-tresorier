# Notes de frais (NDF)

## Vue d'ensemble

Une note de frais permet à un membre de Telecom Etude de se faire rembourser une dépense avancée sur ses deniers personnels pour le compte de la JE. C'est une procédure **à éviter autant que possible** : elle est lourde en justificatifs, demande beaucoup de rigueur et présente un risque de requalification en salaire dissimulé si elle est mal documentée. La carte bancaire TE ou le paiement direct par Telecom Etude doit toujours être privilégié.

> La règle est simple : on évite les avances personnelles. Si quelqu'un envisage d'avancer une dépense, l'orienter vers le trésorier avant de payer.

**Le trésorier se réserve le droit de refuser une NDF** qui ne respecte pas les conditions (justificatifs manquants ou non conformes, dépense non validée préalablement, dépense non conforme à l'objet social...).

**Interlocuteurs impliqués**

- Membre bénéficiaire : sollicite la validation avant l'avance, puis remplit le Google Form
- Trésorier : valide la dépense, contrôle les justificatifs, émet la NDF, réalise le virement
- Président : cosigne la NDF (sauf s'il est lui-même bénéficiaire)
- VP Interne (VPI) : remplace le président ou le trésorier si l'un d'eux est bénéficiaire (voir procédure de surveillance des signataires)
- Vice trésorier⸱e (VT) : comptabilisation et archivage
- CA : validation obligatoire si la dépense dépasse 150 €

**Outils utilisés**

- Google Form NDF : réception de la demande et des justificatifs
- Template Google Docs NDF : Drive Trésorerie > Template GDocs
- YouSign : signature électronique de la NDF
- TS (Google Sheets) : mise à jour par le VT

## Nomenclature

```
NDF-XXX-AAMMJJ-Nom du fournisseur
```

- `XXX` : numérotation incrémentée depuis le 1er mai (repart à 1 chaque exercice)
- `AAMMJJ` : date de la NDF (pas du justificatif)
- `Nom du fournisseur` : le fournisseur ou la nature de la dépense

**Exemple :** `NDF-003-260315-SNCF` pour la troisième NDF de l'exercice, émise le 15 mars 2026, correspondant à un billet de train.

## Justificatifs valides

La note de frais doit impérativement être accompagnée de justificatifs conformes. Sans justificatif valide, pas de remboursement.

| Situation | Justificatif requis |
|---|---|
| Achat général | Facture au nom de Telecom Etude (pas de ticket de caisse) + capture d'écran du débit bancaire |
| Restaurant < 150 € | Ticket de caisse acceptable (exception) + capture d'écran du débit bancaire |
| Déplacement en voiture | Carte grise + capture d'écran du débit bancaire |
| Transport en commun (train, RER, bus...) | Justificatif de voyage avec date et heure + capture d'écran du débit bancaire |

**La facture doit être au nom de Telecom Etude :**
```
TELECOM ETUDE
19 place Marguerite Perey
91120 Palaiseau
N° TVA intracommunautaire (si demandé)
```

Si le membre obtient une facture à son nom ou un simple ticket, lui demander de contacter le fournisseur pour obtenir une facture rectifiée. 

> Si ce n'est pas possible, la NDF peut être acceptée mais la TVA ne sera pas déductible.

## Procédure pas à pas

### Etape 0 - Validation préalable avant l'avance

La dépense doit être validée **avant** que le membre l'avance. C'est le membre qui doit solliciter le trésorier en amont.

- **Dépense < 150 €** : validation par le trésorier ou le président
- **Dépense > 150 €** : validation en CA, avec présence obligatoire dans le budget

Si un membre se présente avec une NDF pour une dépense déjà engagée sans validation préalable, le trésorier **doit** refuser le remboursement. Rappeler systématiquement cette règle.

### Etape 1 - Réception de la demande via le Google Form

Le membre remplit le Google Form NDF. Le trésorier reçoit une notification par mail avec l'ensemble des informations et pièces jointes :

- Adresse mail du membre
- Prénom et nom
- Date de la dépense
- Objet de la dépense
- Facture conforme (PDF)
- Preuve du débit bancaire (capture d'écran en PDF)
- Carte grise si déplacement en voiture (optionnel)
- Justificatif de voyage si transport en commun (optionnel)
- RIB du membre

### Etape 2 - Contrôle des justificatifs

À réception, vérifier :

- Que la dépense a bien été validée préalablement (trésorier + président, ou CA si > 150 €)
- Que la facture est conforme : au nom de Telecom Etude, avec le détail des taux de TVA
- Que la preuve du débit bancaire est présente
- Que les justificatifs spécifiques sont fournis si applicable (carte grise, justificatif de voyage)
- Que le RIB est fourni

Si un justificatif est manquant ou non conforme, revenir vers le membre pour le corriger avant d'aller plus loin. Si la NDF ne peut pas être régularisée, la refuser et expliquer le motif.

### Etape 3 - Identifier la procédure de surveillance des signataires

Selon qui est le bénéficiaire de la NDF, les signataires changent :

| Bénéficiaire | Signataires |
|---|---|
| Membre classique | Trésorier + Président + Bénéficiaire |
| Le Président | VPI + Trésorier + Bénéficiaire (Président) |
| Le Trésorier | Président + VPI + Bénéficiaire (Trésorier) |

Cette règle existe pour éviter qu'un signataire en banque puisse valider sa propre NDF.

### Etape 4 - Editer la NDF

1. Ouvrir le template Google Docs NDF depuis Drive Trésorerie > Template GDocs
2. Dupliquer et renommer selon la nomenclature (`NDF-XXX-AAMMJJ-Nom fournisseur`)
3. Compléter toutes les informations : nom du bénéficiaire, date, objet, montant, détail des justificatifs
4. Exporter en PDF

### Etape 5 - Mise en signature sur YouSign

Déposer la NDF sur YouSign et inviter les signataires dans l'ordre approprié (cf. Etape 3).

Mettre les justificatifs en pièces jointes sur YouSign pour que les signataires puissent les consulter au moment de la signature.

### Etape 6 - Paiement et envoi de la NDF

Une fois la NDF signée par tous :

1. Réaliser le virement au bénéficiaire (montant TTC de la NDF)
2. Envoyer la NDF signée au bénéficiaire

> Si le trésorier est bénéficiaire, c'est le **président** qui réalise le virement.

### Etape 7 - Mise à jour du TS

Mettre à jour l'onglet `Factures d'achats` du TS :
* Nomenclature de la NDF
* Lien vers la NDF signée dans le Drive
* Fournisseur (à ajouter dans l'onglet `Fournisseurs` si nouveau)
* Type : `NDF`
* Libellé : objet de la dépense
* Date de pièce : date de la NDF **pas** date de la dépense
* Montant HT, taux TVA
* Budget concerné
* Date de paiement (date du virement)

### Etape 8 - Contrôle par le VT

Le VT contrôle, comptabilise et archive la NDF. La déposer dans le Drive Trésorerie > Achats-NDF > NDF 202X-202Y et déposer les justificatifs dans le dossier associé. 

Le VT la range ensuite dans le dossier du mois d'émission.

## Points d'attention et pièges fréquents

- **Toujours valider avant l'avance** : rappeler systématiquement cette règle aux membres. Une dépense engagée sans validation préalable peut légitimement être refusée.
- **Pas de ticket de caisse**, sauf exception restaurant < 150 €. Une facture au nom de Telecom Etude est la norme.
- **Détailler l'objet** de la NDF : "achat pizza" ne suffit pas, il faut "achat pizza pour team building du 15/03/2026 (photo de l'événement en justificatif)". L'objectif est de montrer que la dépense sert l'objet social de la JE.
- **Ne jamais rembourser sans NDF signée** : le virement intervient après la signature complète, pas avant.
- **Surveiller les signataires** : appliquer scrupuleusement la procédure de surveillance dès que le bénéficiaire est président ou trésorier.
- **La TVA est déductible** uniquement si la facture est au nom de Telecom Etude avec le détail des taux. Sans ça, pas de déduction possible.
- **En cas d'erreur sur une NDF déjà émise** : suivre la procédure de rectification dédiée — [ndf_rectificative.md](ndf_rectificative.md).
