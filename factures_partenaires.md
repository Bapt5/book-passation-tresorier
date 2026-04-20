# Emission de factures partenaires

## Vue d'ensemble

Les factures partenaires sont des factures de vente hors études, émises dans le cadre de contrats de partenariat signés avec des entreprises (KPMG, Bain, etc.). Elles correspondent à des subventions commerciales et suivent une logique différente des factures d'étude : elles ne sont pas liées à un PVR ou une CE, mais à un contrat de partenariat et à un accord sur une prestation (visibilité, accès à des événements, etc.).

**Interlocuteurs impliqués**

- responsable du partenariat : déclencheur de la procédure, fournit les informations nécessaires
- Trésorier : émet la facture et met à jour le TS
- Vice trésorier⸱e (VT) : contrôle, comptabilisation et archivage
- Partenaire : destinataire final de la facture

**Outils utilisés**

- TS (Google Sheets) : onglet `Factures ventes`
- Template Google Docs facture subvention : Drive Trésorerie > Template GDocs

> Logigramme : [logigramme_factures_partenaires.md](logigrammes/logigramme_factures_partenaires.md)

## Nomenclature

```
FAC-XXX-NOM_ENTREPRISE_PARTENAIRE
```

- `XXX` : numérotation globale incrémentée depuis toujours (partagée avec les factures d'étude, on est autour de 580 en 2025-2026)
- `NOM_ENTREPRISE_PARTENAIRE` : nom court et lisible du partenaire (ex : KPMG, Bain, BearingPoint, etc.)

**Exemple :** `FAC-582-KPMG` pour la facture KPMG qui porte le numéro global 582.

> Il n'y a pas de numéro interne à l'entreprise comme pour les études (pas de N en suffixe), puisqu'en général une seule facture est émise par exercice comptable et par partenaire.

## TVA et délai de paiement

- **TVA : 20 % systématiquement.** Les subventions partenaires sont des prestations commerciales soumises à TVA.
- **Délai de paiement : 60 jours** (contre 30 jours pour les clients d'études).

## Procédure pas à pas

### Etape 0 - Anticiper et relancer le responsable du partenariat

Le trésorier ne doit pas attendre passivement. Si une subvention est prévue et que la cloture comptable approche, que la facture n'est pas encore émise et que le responsable du partenariat n'a pas encore pris contact, **relancer proactivement**. 

### Etape 1 - Réception de la demande du responsable du partenariat

Le responsable du partenariat contacte le trésorier par message ou mail pour demander l'émission d'une facture. Il fournit :

- Le **contrat de partenariat** (ou sa référence), qui précise le montant et l'objet
- Le **montant à facturer** (HT)
- Les **coordonnées de facturation** du partenaire : raison sociale, adresse de facturation, SIRET

Si l'une de ces informations est manquante, la demander avant de procéder. Ne jamais émettre une facture avec des coordonnées incomplètes.

> Pour les partenaires récurrents (ex : KPMG), les coordonnées sont généralement déjà connues. Vérifier qu'elles n'ont pas changé d'une année sur l'autre.

### Etape 2 - Editer la facture

1. Ouvrir le template Google Docs **facture subvention** depuis Drive Trésorerie > Template GDocs
2. Dupliquer le template et le renommer selon la nomenclature (`FAC-XXX-NOM_PARTENAIRE`)
3. Compléter les informations :
   - Raison sociale et adresse du partenaire
   - SIRET du partenaire (à vérifier sur [annuaire-entreprises.data.gouv.fr](https://annuaire-entreprises.data.gouv.fr) en cas de doute)
   - Numéro de facture
   - Date d'émission et date d'échéance (J+60)
   - Objet de la facturation : reprendre la formulation du contrat de partenariat
   - Montant HT, TVA à 20 %, total TTC
   - Référence au contrat de partenariat

4. Vérifier les mentions légales obligatoires :
   - En-tête : raison sociale de Telecom Etude, SIRET, code APE, numéro de TVA intracommunautaire
   - Mention "TVA sur les encaissements"
   - Modalités de paiement (virement bancaire)
   - Conditions d'escompte pour paiement anticipé

5. Exporter la facture au format PDF

La facture n'est pas signée : aucune signature n'est requise avant envoi.

### Etape 3 - Envoi au partenaire

C'est le **responsable du partenariat** qui envoie la facture au partenaire, en mettant `tresorier@telecom-etude.fr` en copie pour permettre le suivi de réception et du paiement.

> Pour BearingPoint, la facture est à envoyer à l'adresse [supplierinvoice@bearingpoint.com](mailto:supplierinvoice@bearingpoint.com), pour plus d'informations [https://www.bearingpoint.com/fr-fr/facturation/](https://www.bearingpoint.com/fr-fr/facturation/)

### Etape 4 - Mise à jour du TS

Après émission, mettre à jour l'onglet `Factures ventes` du TS :

- Le numéro de facture
- Le partenaire (à ajouter dans l'onglet `Clients` si nouveau)
- Le type : `Subvention C`
- Le lien vers la facture dans le Drive
- La date d'émission et la date d'échéance (J+60)
- Le montant HT

Suivre le paiement depuis cet onglet. Lorsque le virement est reçu, noter la date et notifier le responsable du partenariat.

### Etape 5 - Contrôle par le VT

Comme pour toute facture de vente, le VT contrôle, comptabilise et archive la facture. La déposer dans le Drive Trésorerie > Ventes (Factures) > Mandat 202X-202Y. 

Le VT la range ensuite dans le dossier du mois d'émission.

## Points d'attention et pièges fréquents

- **Ne pas attendre que le responsable du partenariat prenne l'initiative** : si une subvention est prévue et que la cloture comptable approche, relancer proactivement pour éviter les retards d'émission.
- **Toujours vérifier les coordonnées** du partenaire, même pour les partenaires récurrents.
- **Ne pas oublier la TVA à 20 %** : les subventions partenaires sont des prestations commerciales, pas des dons. La TVA est obligatoire.
- **Le délai de paiement est de 60 jours**, pas 30 : ne pas paramétrer la mauvaise date d'échéance dans la facture.
- **Toujours être en copie de l'envoi** pour assurer le suivi de réception.
- **Surveiller les créances partenaires** comme les créances études : elles n'ont pas moins d'importance.
- **En cas d'erreur sur une facture déjà émise** : suivre la procédure de rectification dédiée — [factures_rectification.md](factures_rectification.md).
