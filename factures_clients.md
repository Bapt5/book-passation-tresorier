# Emission de factures clients

## Vue d'ensemble

L'émission de factures clients est l'une des tâches les plus visibles du trésorier dans le cycle d'une étude. Elle est déclenchée par la signature de documents clés et nécessite une mise à jour rigoureuse du Tableau de Suivi (TS).

**Interlocuteurs impliqués**

- Chef de projet (CdP) : rédaction des documents contractuels, envoi de la facture au client
- Vice Président⸱e des Opérations (VPO) : dépose les documents à signer sur YouSign
- Vice trésorier⸱e (VT) : contrôle de la facture avant envoi, puis comptabilisation et archivage
- Client : destinataire final de la facture

**Outils utilisés**

- YouSign : réception des notifications de signature
- TS (Google Sheets) : onglets `Suivi des études`, `Factures ventes`
- Sheet de facturation de l'étude : généré automatiquement dans le TS à la création de l'étude, à compléter manuellement
- Modèle Google Docs de facture : s'auto-complète depuis le sheet de facturation

## Types de factures

| Type | Déclencheur | Particularité |
|---|---|---|
| Facture d'acompte | Signature de la CE ou du BC | Entre 30 et 50 % du total, fortement recommandée, ne permet pas de rétribuer un intervenant |
| Facture intermédiaire | Signature du PVRI | Facture les phases validées, permet de rétribuer les JEH correspondants |
| Facture de solde | Signature du PVRF | Obligatoire, solde le montant restant, permet de rétribuer tous les JEH |
| Facture d'avoir | Erreur ou rupture | Très rare, se référer à Kiwi Légal |
| Facture client non français | Cas spécifique | Se référer à Kiwi Légal |

> La facture Pro-Forma est un équivalent de devis sans valeur comptable. Si le client en réclame une, se référer à Kiwi Légal.

## Nomenclature

```
FAC-XXX-CODE_ETUDE-N
```

- `XXX` : numérotation globale incrémentée depuis toujours (on est autour de 580 en 2025-2026)
- `CODE_ETUDE` : numéro d'étude au format `22YYYY`
- `N` : numéro de la facture dans l'étude (1re, 2e, 3e facture...)

**Exemple :** `FAC-581-250012-1` pour la première facture de l'étude 250012, numéro global 581.

## Procédure pas à pas

### Etape 0 - Préparer le sheet de facturation à la mise en signature de la CE ou du BC

Dés la réception d'une notification de mise en signature d'une CE ou d'un BC, le trésorier doit préparer le sheet de facturation de l'étude concernée dans le TS.

1. Dans l'onglet `Suivi des études`, s'il elle n'existe pas déjà, créer une ligne pour l'étude concernée avec toutes les informations
2. Cocher la case `Générer sheet`, puis cliquer sur le menu Suivi d'étude > Générer sheets de facturation
3. Le sheet de facturation apparait dans la colonne `Sheet de facturation` : cliquer sur le lien pour l'ouvrir
4. Compléter les informations manquantes dans le sheet de facturation

**Ce qu'il faut renseigner :**

- Raison sociale et adresse du client
- SIRET (à vérifier sur [annuaire-entreprises.data.gouv.fr](https://annuaire-entreprises.data.gouv.fr))
- Adresse de facturation si différente de l'adresse du siège
- Montant HT, répartition par phases, frais de dossier

> Si des informations manquent, les chercher sur l'annuaire des entreprises. En cas de doute, demander au client via le CdP. Ne jamais émettre une facture avec des coordonnées incomplètes ou incertaines.

Ce sheet doit être mis à jour à chaque avenant (au minimum la nomenclature du dernier avenant si le budget n'est pas modifié)

### Etape 1 - Recevoir la notification YouSign

Le VPO dépose les documents à signer sur YouSign. Le trésorier reçoit une notification par mail à `tresorier@telecom-etude.fr` lorsque tous les signataires ont signé.

**Vérifier à réception :**

- Que le document est bien le bon (CE, BC, PVRI ou PVRF selon le type de facture attendu)
- Que toutes les signatures sont présentes
- Que le montant correspond à ce qui est renseigné dans le sheet de facturation

### Etape 2 - Editer la facture

1. Ouvrir l'onglet `Suivi des études` du TS
2. Ouvrir le sheet de facturation de l'étude concernée
3. Vérifier que toutes les informations dans le sheet de facturation correspondent à ce qui est indiqué dans le document signé
4. Dans l'onglet `Facture`, si besoin compléter la date de signature du PVR pour la facture concernée
5. Cliquer sur le bouton "Générer la facture d'acompte/intermédiaire/solde" selon le type de facture à émettre
6. Le numéro d'incrémentation globale et le dossier de destination de la facture sont demandés
7. Ouvrir la facture générée, vérifier que les informations sont correctement reportées et que les mentions légales sont présentes
8. Exporter la facture au format PDF pour l'envoi au client


**Vérifier les mentions légales obligatoires sur la facture :**

- En-tête : raison sociale de Telecom Etude, SIRET, code APE, numéro de TVA intracommunautaire
- Mention "TVA sur les encaissements"
- Modalités de paiement (virement bancaire)
- Conditions d'escompte pour paiement anticipé

**Vérifier les mentions variables :**

- Date d'émission et date d'échéance
- Numéro de facture au format `FAC-XXX-CODE_ETUDE-N`
- Référence à la CE/BC et les éventuels avenants
- Date de signature du PVR si facture intermédiaire ou de solde
- Raison sociale et adresse de facturation
- Prix HT par phase, frais de dossier HT, total HT
- TVA à 20 %
- Total TTC

**TVA : toujours 20 %, sans exception pour les clients français.**

**Délai de paiement :**

- 30 jours date de facture pour les clients standard
- parfois plus à vérifier dans les conditions générales d'étude dans le doute

La facture n'est pas signée : aucune signature n'est requise avant envoi.

### Etape 3 - Envoi au client

C'est le **CdP** qui envoie la facture au client, en mettant `tresorier@telecom-etude.fr` en copie pour permettre le suivi.

### Etape 4 - Mise à jour du TS

Après émission, mettre à jour le TS :

**Onglet `Factures ventes`** : renseigner 
* Le numéro
* Le client (à rajouter dans l'onglet `Clients` si nouveau)
* Le type de facture (acompte, intermédiaire, solde)
* La référence de l'étude : CODE_ETUDE
* Le lien vers la facture dans le drive
* La date d'émission
* Le budget associé : `Prestations (montant des JEH)`

**Pour les factures d'acompte :** 
* La colonne `HT acompte`

**Pour les factures intermédiaires et de solde :**
* La colonne `Nb JEH`
* La colonne `HT JEH`

**Pour les factures de solde :**
* La colonne `HT Dossier`
* La colonne `HT acompte` avec un montant négatif correspondant au montant HT de la facture d'acompte

Suivre le paiement depuis cet onglet. Lorsque le virement est reçu, noter la date et notifier les CdP.

### Etape 5 - Contrôle par le VT

Comme pour toute facture de vente, le VT contrôle, comptabilise et archive la facture. La déposer dans le Drive Trésorerie > Ventes (Factures) > Mandat 202X-202Y. 

Le VT la range ensuite dans le dossier du mois d'émission.

## Points d'attention et pièges fréquents

- **Ne pas émettre une facture avant que tous les signataires aient signé** le document déclencheur (CE, PVRI, PVRF). 
- **Remplir le sheet de facturation dès la mise en signature de la CE**, pas au moment de l'émission : si on attend, des informations peuvent manquer et bloquer la génération.
- **Mettre à jour le sheet à chaque avenant**
- **Vérifier le SIRET**
- **Toujours être en copie de l'envoi** pour assurer le suivi de réception.
- **Surveiller les créances activement** : ne pas attendre que le CdP signale un retard, c'est le trésorier qui pilote.
- Pour les **avoirs et les factures clients étrangers** : ne pas improviser, consulter Kiwi Légal ou contacter la CNJE.
- **En cas d'erreur sur une facture déjà émise** : suivre la procédure de rectification dédiée — [factures_rectification.md](factures_rectification.md).
