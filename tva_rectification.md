# Rectification d'une déclaration de TVA

## Vue d'ensemble

Une erreur sur une déclaration de TVA passée ne donne pas lieu à une déclaration rectificative séparée : elle se corrige directement dans la déclaration du **mois suivant**, en utilisant les lignes prévues à cet effet sur le formulaire 3310-CA3. Dans tous les cas, l'erreur doit être expliquée dans le champ réservé à la correspondance de cette déclaration corrective.

> Pour la procédure de déclaration mensuelle standard, voir [tva.md](tva.md).

**Interlocuteurs impliqués**

- Trésorier : identifie l'erreur, prépare la correction dans la déclaration suivante
- VT : vérifie les comptes de TVA (44566, 44571, 44577), double contrôle avant dépôt

## Identifier le type d'erreur

| Type d'erreur | Ligne à remplir sur la prochaine déclaration |
|---|---|
| Trop déclaré de TVA déductible | Ligne 15 — "TVA antérieurement déduite à reverser" |
| Oubli de TVA déductible | Ligne 21 — "Autre TVA à déduire" |
| Trop déclaré de TVA collectée | Ligne 21 — "Autre TVA à déduire" |
| Oubli de TVA collectée | Ligne A1 + Ligne 8 — avec la TVA collectée du mois courant |

## Cas a - Trop déclaré de TVA déductible

Lors d'une déclaration passée, un montant de TVA déductible a été saisi en trop (TVA non déductible incluse par erreur, montant sur-évalué...).

**Correction lors de la prochaine déclaration :**

Remplir la **ligne 15 "TVA antérieurement déduite à reverser"** avec le montant de TVA déduit en trop. Ce montant vient augmenter la TVA nette due.

## Cas b - Oubli de TVA déductible

Lors d'une déclaration passée, une facture d'achat déductible n'a pas été prise en compte (facture reçue tardivement, oubli de saisie...).

**Correction lors de la prochaine déclaration :**

Inscrire le montant de TVA omis à la **ligne 21 "Autre TVA à déduire"**. Ce montant vient diminuer la TVA nette due.

## Cas c - Trop déclaré de TVA collectée

Lors d'une déclaration passée, un montant de TVA collectée a été saisi en trop (encaissement saisi deux fois, mauvais taux appliqué, opération exonérée incluse par erreur...).

**Correction lors de la prochaine déclaration :**

Inscrire le montant de TVA collectée en trop à la **ligne 21 "Autre TVA à déduire"**. Ce montant vient diminuer la TVA nette due.

## Cas d - Oubli de TVA collectée

Lors d'une déclaration passée, un encaissement soumis à TVA n'a pas été déclaré (virement reçu non comptabilisé dans le mois, oubli...).

**Correction lors de la prochaine déclaration :**

Ajouter le montant HT de l'opération omise à la **ligne A1** et à la **ligne 8**, avec la TVA collectée du mois courant. La TVA correspondante s'ajoute ainsi à la TVA collectée totale.

## Remplir le champ "Correspondance"

**Dans tous les cas**, il est obligatoire d'expliquer l'erreur dans le champ réservé à la correspondance de la déclaration corrective, avant de valider.

Ce champ sert à deux fins : rappeler le contexte pour le trésorier lui-même (notamment pour justifier l'écart lors d'un audit) et informer l'administration fiscale de la nature de la régularisation.

Exemple de formulation : "Régularisation d'une TVA déductible omise sur la déclaration de [mois/année] : facture ACH-XXX-AAMMJJ non incluse dans la déclaration initiale, montant de TVA déductible concerné : XX,XX €."

## Points d'attention et pièges fréquents

- **La correction se fait toujours sur la déclaration du mois suivant**, pas par dépôt d'une déclaration rectificative séparée.
- **Toujours remplir le champ correspondance.** Un écart inexpliqué sur une déclaration peut poser problème lors d'un contrôle fiscal. Même si la correction est mineure, expliquer le contexte prend moins d'une minute et peut éviter des complications.
- **Croiser avec le VT** avant de déposer la déclaration corrective : les comptes 44566, 44571 et 44577 doivent refléter la correction.
- **Ne pas attendre plusieurs mois** pour régulariser une erreur identifiée. Plus le délai est long, plus la justification est difficile à reconstituer.
- **Cas c et b partagent la même ligne (21)** : vérifier que le sens de la correction est bien pris en compte dans le calcul de la TVA nette due (case 28).
