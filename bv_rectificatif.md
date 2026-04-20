# Rectification d'un bulletin de versement

## Vue d'ensemble

Un BV erroné ne peut pas être simplement corrigé ou supprimé : il doit faire l'objet d'une procédure comptable précise qui neutralise l'écriture initiale et la remplace par les montants corrects. La procédure varie selon la nature de l'erreur (montant, informations personnelles, numéro de sécurité sociale) et selon le moment où l'erreur est détectée (avant ou après déclaration des cotisations, dans l'année civile ou non).

> Pour la procédure d'émission d'un BV standard, voir [bulletins_de_versement.md](bulletins_de_versement.md).

**Interlocuteurs impliqués**

- Trésorier : émet le BV rectificatif, régularise le net, coordonne la correction
- VT : comptabilise les écritures inverses et le BV rectificatif, archive
- Intervenant : informé de la rectification, rembourse ou reçoit le différentiel selon le cas

> Logigramme : [logigramme_bv_rectificatif.md](logigrammes/logigramme_bv_rectificatif.md)

## Identifier la nature de l'erreur

Avant toute chose, déterminer ce qui est erroné :

| Type d'erreur | Procédure |
|---|---|
| Erreur sur le montant ou le nombre de JEH | Procédure complète ci-dessous (étapes 1 à 5) |
| Erreur sur les informations personnelles (hors numéro de sécu) | Rien à faire sur le plan comptable |
| Erreur sur le numéro de sécurité sociale | Emettre un nouveau BV avec la mention **"annule et remplace"** uniquement |

La suite de cette fiche concerne exclusivement les erreurs sur les montants.

## Procédure pas à pas (erreur sur le montant)

### Etape 1 - Emettre le BV rectificatif

Générer un nouveau BV depuis le TS avec les montants corrects. Ce BV doit porter la mention **"Rectificatif"** de manière explicite dans le document.

La nomenclature suit le format standard des BV : `BV-XXX-CODE_ETUDE-N`, avec le prochain numéro d'incrément disponible. Le lien entre le BV rectificatif et le BV initial doit être clairement documenté (dans le TS).

Envoyer ce BV rectificatif à l'intervenant comme pour un BV classique (document RGPD : uniquement à l'intervenant).

### Etape 2 - Comptabiliser l'écriture inverse du BV erroné

Le VT passe une écriture qui neutralise entièrement le BV initial, à la manière d'un avoir : reprendre l'écriture de base du BV en inversant crédit et débit.

### Etape 3 - Comptabiliser le BV rectificatif

Le VT comptabilise le BV rectificatif comme une comptabilisation normale de BV, avec les montants corrects.

### Etape 4 - Régulariser le différentiel de net payé

Calculer la différence entre le net effectivement versé lors du premier BV et le net qui aurait dû être versé selon le BV rectificatif.

**Si le différentiel est significatif :**

- Telecom Etude doit de l'argent à l'intervenant : effectuer un virement complémentaire et comptabiliser l'encaissement/décaissement dans le compte de banque 512.
- L'intervenant doit de l'argent à Telecom Etude : lui demander de rembourser le trop-perçu et comptabiliser la réception.

**Si le différentiel est de l'ordre de quelques euros (montant faible) :**

Il n'est pas obligatoire de demander le remboursement ou d'effectuer un virement complémentaire. Deux cas :

- Telecom Etude a trop payé et renonce au remboursement : passer en **perte** — compte 658 au débit, compte 468 de l'intervenant au crédit.
- L'intervenant renonce au montant qui lui est dû : passer en **gain** — compte 758 au crédit, compte 468 de l'intervenant au débit.

### Etape 5 - Gérer les cotisations sociales

Les cotisations sociales déclarées dans le BRC sont basées sur les BV émis. Une rectification a donc un impact sur les déclarations sociales.

**Si les cotisations du BV initial n'ont pas encore été déclarées** : déclarer uniquement le BV rectificatif, ne pas déclarer le BV initial.

**Si les cotisations du BV initial ont déjà été déclarées** : ne pas déclarer le BV rectificatif au BRC. Régulariser lors du **Tableau Récapitulatif (TR)** annuel.

**Si le BV initial date de l'année civile précédente** (le TR correspondant est donc déjà clôturé) : réaliser un **TR rectificatif** pour régulariser les cotisations de l'année concernée.

> Pour les procédures TR et TR rectificatif, consulter le [tutoriel CNJE sur Kiwi Légal](https://legal.junior-entreprises.com/knowledge-base/tableau-recapitulatif-tr/).

## Points d'attention et pièges fréquents

- **Bien identifier la nature de l'erreur avant d'agir.** Une erreur sur les informations personnelles (hors numéro de sécu) ne nécessite aucune action comptable, ce qui évite une procédure inutile.
- **Le BV rectificatif porte la mention "Rectificatif"**, pas "annule et remplace". Cette mention est réservée aux erreurs sur le numéro de sécurité sociale.
- **Ne pas déclarer le BV rectificatif au BRC si le BV initial a déjà été déclaré.** La régularisation se fait au TR, pas en redéclarant un BRC corrigé.
- **Si le BV initial est de l'année civile précédente**, le TR est clôturé : un TR rectificatif est alors indispensable. Ne pas ignorer ce point : une erreur de cotisations non régularisée peut entraîner des pénalités URSSAF.
- **Documenter le lien entre le BV erroné et le BV rectificatif** dans le TS et dans les noms de fichiers archivés, pour que le VT puisse retrouver le contexte facilement.
- **Les petits différentiels peuvent être passés en perte ou en gain**, mais cette décision doit être explicite et 