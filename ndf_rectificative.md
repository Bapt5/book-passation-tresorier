# Rectification d'une note de frais

## Vue d'ensemble

Toute erreur sur une note de frais déjà émise, qu'elle porte sur un montant ou sur les informations du bénéficiaire, se corrige de la même façon : émettre une nouvelle NDF portant la mention **"annule et remplace"**. Si l'erreur porte sur un montant, il faut en plus régulariser la différence avec le bénéficiaire.

> Pour la procédure d'émission d'une NDF standard, voir [notes_de_frais.md](notes_de_frais.md).

**Interlocuteurs impliqués**

- Trésorier : émet la NDF rectificative, gère le différentiel de remboursement si nécessaire
- Bénéficiaire : informé, rembourse ou reçoit la différence selon le cas
- Président / VPI : cosignataires de la NDF rectificative (mêmes règles de surveillance des signataires que pour une NDF classique)
- VT : comptabilise les écritures correctives, archive

> Logigramme : [logigramme_ndf_rectificative.md](logigrammes/logigramme_ndf_rectificative.md)

## Procédure pas à pas

### Etape 1 - Emettre la NDF "annule et remplace"

Générer une nouvelle NDF depuis le template, en reprenant les informations correctes. Elle doit porter la mention **"annule et remplace"** et indiquer le numéro de la NDF initiale qu'elle remplace.

La nomenclature suit le format standard : `NDF-XXX-AAMMJJ-Nom fournisseur`, avec le prochain numéro d'incrément disponible.

La NDF rectificative suit le même circuit de signature que toute NDF : trésorier + président + bénéficiaire (ou procédure de surveillance des signataires si le bénéficiaire est président ou trésorier).

### Etape 2 - Régulariser le différentiel (si erreur sur le montant)

Calculer la différence entre le montant effectivement versé lors de la NDF initiale et le montant correct figurant sur la NDF rectificative.

**Si le différentiel est significatif :**

- Telecom Etude doit de l'argent au membre : effectuer un virement complémentaire et comptabiliser l'encaissement/décaissement dans le compte de banque 512.
- Le membre doit de l'argent à Telecom Etude : lui demander de rembourser le trop-perçu et comptabiliser la réception dans le compte 512.

**Si le différentiel est de l'ordre de quelques euros (montant faible) :**

Il n'est pas obligatoire de demander le remboursement ou d'effectuer un virement complémentaire. Deux cas :

- Telecom Etude a trop payé et renonce au remboursement : passer en **charge de gestion courante** — compte 658 au débit, compte 4681 du membre au crédit.
- Le membre renonce au montant qui lui est dû : passer en **produit de gestion courante** — compte 758 au crédit, compte 4681 du membre au débit.

### Etape 3 - Mise à jour du TS

Mettre à jour l'onglet `Factures d'achats` du TS avec la NDF rectificative, comme pour toute NDF. Documenter le lien avec la NDF initiale dans le libellé.

### Etape 4 - Transmission au VT

Le VT comptabilise la NDF rectificative et les éventuelles écritures de régularisation, et archive les deux NDF (initiale et rectificative) dans le même dossier.

## Points d'attention et pièges fréquents

- **"Annule et remplace" couvre tous les types d'erreurs**, qu'il s'agisse d'un montant, d'un nom, d'une date ou d'un objet. Il n'y a pas de distinction de procédure selon la nature de l'erreur.
- **Les mêmes règles de surveillance des signataires s'appliquent** à la NDF rectificative qu'à la NDF initiale. Ne pas les contourner sous prétexte que c'est une correction.
- **Le compte du membre est le 4681**, à ne pas confondre avec le 468 utilisé pour les intervenants (BV).
- **Ne pas oublier de virer ou récupérer la différence** si l'erreur porte sur un montant. Même petite, une différence doit être traitée explicitement — soit régularisée, soit passée en perte/gain avec les bonnes écritures.
- **Archiver les deux NDF ensemble** (initiale et rectificative) pour que le VT 