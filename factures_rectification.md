# Modification ou annulation d'une facture émise

## Vue d'ensemble

L'annulation ou la modification d'une facture émise doit respecter des règles précises pour préserver la continuité de la numérotation et la cohérence comptable. La procédure dépend de deux critères : la facture a-t-elle déjà été envoyée au tiers, et l'erreur porte-elle sur un montant ou sur une autre donnée ?

Cette fiche couvre toutes les factures émises par Telecom Etude : factures clients (études), factures partenaires et tout autre document de facturation.

> Pour l'émission de factures clients d'études, voir [factures_clients.md](factures_clients.md). Pour les factures partenaires, voir [factures_partenaires.md](factures_partenaires.md).

**Interlocuteurs impliqués**

- Trésorier : identifie le cas, réalise la correction ou émet la facture rectificative, effectue le remboursement si nécessaire
- VT : corrige les écritures dans Cegid Loop, archive
- Client / partenaire : destinataire de la facture rectificative si la facture a déjà été envoyée

## Identifier la situation

Avant d'agir, répondre à ces deux questions :

**1. La facture a-t-elle déjà été envoyée au tiers ?**

- Non : correction directe possible, sans document supplémentaire.
- Oui : un document rectificatif est obligatoire.

**2. L'erreur porte-t-elle sur un montant ?**

- Non : aucun impact comptable.
- Oui : une facture d'avoir est nécessaire.

## Cas 1 - La facture n'a pas encore été envoyée

Modifier directement le Google Docs de la facture. Corriger également l'écriture dans Cegid Loop si elle a déjà été saisie.

Aucun document supplémentaire n'est nécessaire.

## Cas 2 - La facture a été envoyée, erreur sans impact sur les montants

Si l'erreur porte sur une donnée non financière (raison sociale, adresse, code étude, période...) et n'a aucun impact sur les montants, aucune manipulation comptable n'est nécessaire.

Procédure :

1. Corriger la facture dans le Google Docs en conservant le même numéro d'incrément.
2. Mentionner dans le document qu'il **"annule et remplace"** la version précédente.
3. Envoyer la version corrigée au tiers en précisant que la modification ne concerne pas les montants.

## Cas 3 - La facture a été envoyée, erreur sur le montant

Si la facture émise ne correspond pas au montant prévu dans le BC ou la CE, il s'agit d'une erreur à corriger.

Procédure :

1. Emettre une **facture d'avoir** qui neutralise tout ou partie de la facture initiale.
2. Emettre une **nouvelle facture corrigée** avec le bon montant, au prochain numéro d'incrément disponible.
3. Envoyer les deux documents au tiers.
4. Si le tiers a déjà payé la facture initiale, rembourser la différence par virement sortant.
5. Le VT comptabilise la facture d'avoir et la nouvelle facture, et corrige les écritures dans Cegid Loop.

> Important : si une erreur porte sur le BC ou la CE elle-même (et non sur la facture), cela ne relève pas d'une rectification de facture. Le contrat signé fait foi. Une facture ne corrige pas un contrat.

## Contenu d'une facture d'avoir

La facture d'avoir reprend les mentions obligatoires d'une facture classique, avec les spécificités suivantes :

- Le titre doit comporter le terme **"avoir"**
- Elle doit mentionner le **numéro de la facture initiale** à laquelle elle se réfère
- La mention "net à payer" est remplacée par **"net à déduire"**
- Si Telecom Etude rembourse le tiers, les **modalités de remboursement** doivent figurer sur l'avoir
- Les montants sont présentés **en négatif**

La nomenclature de la facture d'avoir suit le format standard : `FAC-XXX-CODE_ETUDE-N` avec le prochain numéro d'incrément disponible. La nomenclature de la facture initiale est indiqué dans le corps du document.

## Points d'attention et pièges fréquents

- **Ne jamais supprimer une facture envoyée.** Une fois transmise au tiers, une facture doit être neutralisée par un avoir, jamais effacée. Cela préserve la continuité de la numérotation et la traçabilité comptable.
- **Une erreur dans le BC ou la CE ne se corrige pas par un avoir.** Le contrat signé fait foi. Si le montant contractuel est erroné, c'est un sujet juridique à traiter avec le VPO/CdP, pas une rectification de facture.
- **Après signature du PVRF, un avoir ne modifie pas les JEH.** Il ne porte que sur les montants en euros de la facture, et uniquement en cas d'erreur de facturation par rapport au contrat signé.
- **Le remboursement au tiers se fait par virement sortant classique**, après émission et envoi de l'avoir.

> Pour plus de détails sur la rectification de factures, voir le tutoriel CNJE sur Kiwi Légal : [Rectification de facture](https://legal.junior-entreprises.com/knowledge-base/annuler-ou-modifier-une-facture-emise/).
